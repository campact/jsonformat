`jsonformat` takes a stream ob [JSON](http://www.json.org) objects from stdin and
brings them into a (user) specified format.

## Installation
A simple `go get` should do the trick

## Usage
`jsonformat` supports two formats right now:

* *template* which is a thin wrapper around [Go's templating language](http://golang.org/pkg/text/template/) and allows great complexity
* *csv* which is actually just a generator for *template*, but hides most of the complexity to make generating CSV-style output easier.

### Examples
#### Testdata
`json.txt`:

```json
{
	"Name": {
		"FirstName": "John",
		"LastName": "Doe"
	},
	"Age": 25,
	"NetWorth": 22.23
}
{
	"Name": {
		"FirstName": "Jane",
		"LastName": "Doe"
	},
	"Age": 18,
	"NetWorth": 250123.2
}
```

#### template

    $ cat json.txt | jsonformat -format template '{{.Name.FirstName}} {{.Name.LastName}} - {{.NetWorth}}'
    John Doe - 22.23
    Jane Doe - 250123.2

#### csv

    $ cat json.txt | jsonformat -format csv 'Name.FirstName=First Name|str,Name.LastName=Last Name|str,NetWorth=Net Worth|dec'
    First Name,Last Name,Net Worth
    "John","Doe",22.23
    "Jane","Doe",250123.20

---
Version 0.1
