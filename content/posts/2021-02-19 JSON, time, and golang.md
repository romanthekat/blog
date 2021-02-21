---
title: "[19/100] JSON, time, and golang"
date: 2021-02-19
published: true
---

Fun thing about JSON - it doesn't have dates or time support, as per RFC.
So whereas you see something like `2021-02-18T21:54:42.123Z` in JSON - it's still just a string.

Some languages firmly follow that, like [nim](https://nim-lang.org/docs/json.html) stdlib parser. 
Some try to parse as if it were [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) time. 
Which is actually nice - it's human readable, sortable, portable, well supported and precise. 
Though such support sometimes causes extra fun, like java's jackson lib and [JSR 310](https://jcp.org/en/jsr/detail?id=310) if currespondent parsing module is not added for java 8+ date/time classes. 

Golang supports ISO 8601, so it will work as you might expect:
```go
dateString := "2021-02-18T21:54:42.123Z"
date, err := time.Parse(time.RFC3339, dateString) //RFC 3339 is a profile for ISO 8601
```
`date` will have the `time.Time` value. (let's skip for a moment the difference between realtime and monotonic time)

Apart from such a detailed 'point of time' there is also 'calendar date', or 'civil time' - representation of a 'day', e.g. `2021-02-18`. A common thing to use.

Golang stdlib doesn't have special type for that, one should still rely on `time.Time` type.
And it actually works:
```go
dateString := "2021-02-18"
date, err := time.Parse("2006-01-02", dateString) //note the date layout YYYY-MM-DD
```
It prints into `2021-02-18 00:00:00 +0000 UTC`.

So if you want to parse a JSON with time field you might come up with that:
```go
type Entity struct {
    Name string    `json:"name"`
    Time time.Time `json:"time"`
}

func main() {
    jsonString := `{"name": "A name", "time": "2021-02-18T21:54:42.123Z"}`
    var entity Entity
    err := json.Unmarshal([]byte(jsonString), &entity)
}
```
Works nicely.

But if the time field has only 'date' part (`2021-02-18`), unmarshalling will fail with:
`parsing time ""2021-02-18"" as ""2006-01-02T15:04:05Z07:00"": cannot parse """ as "T"`

And in this moment you either have to fallback to using `string` type and parse the date manually, or introduce your own time type alias and provide custom (un)marshaller, for example:
```go
type Entity struct {
    Name string    `json:"name"`
    Time CivilTime `json:"time"`
}

type CivilTime time.Time

func (c *CivilTime) UnmarshalJSON(b []byte) error {
    value := strings.Trim(string(b), `"`) //get rid of "
    if value == "" || value == "null" {
        return nil
    }

    t, err := time.Parse("2006-01-02", value) //parse time
    if err != nil {
        return err
    }
    *c = CivilTime(t) //set result using the pointer
    return nil
}

func (c CivilTime) MarshalJSON() ([]byte, error) {
    return []byte(`"` + time.Time(c).Format("2006-01-02") + `"`), nil
}
```
Implementing (un)marshaller json interfaces is pretty straight forward.
Just a tad cumbersome :)

I hope [civil time proposal](https://github.com/golang/go/issues/19700) will be implemented.