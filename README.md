# tablecli

[![License: MIT](https://img.shields.io/badge/license-MIT-green&logo=OpenSourceInitiative)](https://opensource.org/licenses/MIT)
[![GoDoc](https://img.shields.io/badge/reference-GO-blue.svg?style=&logo=go&logoColor=white)](https://godoc.org/github.com/aziontech/tablecli)
[![Go Report Card](https://goreportcard.com/badge/github.com/aziontech/tablecli)](https://goreportcard.com/report/github.com/aziontech/tablecli)

Packages provide a convenient way to generate tabular output of any data, useful primarily for CLI tools.

<img src="https://raw.githubusercontent.com/maxwelbm/tablecli/main/example.gif?auto=compress&cs=tinysrgb&h=750&w=1260" alt="Girl in a jacket" width="100%" height="250px">

#### Install Package
```sh
go get github.com/aziontech/tablecli
```

#### Example of use:
```go 
package main

import (
    table "github.com/aziontech/tablecli"
    "github.com/fatih/color"
    "strings"
)


type list struct {
    ID string 
    Name string
}

func main() {
    tbl := table.New("ID", "NAME")
    headerFmt := color.New(color.FgBlue, color.Underline).SprintfFunc()
    columnFmt := color.New(color.FgGreen).SprintfFunc()
    tbl.WithHeaderFormatter(headerFmt).WithFirstColumnFormatter(columnFmt)

    var list = []list{
        { "123123", "Jonh"},
        { "123121", "Jeff"},
    }

    for _, i := range list {
	tbl.AddRow(i.ID, i.Name)
    }

    format := strings.Repeat("%s", len(tbl.GetHeader())) + "\n"
    tbl.CalculateWidths([]string{})

    tbl.PrintHeader(format)
	for _, r := range tbl.GetRows() {
	    tbl.PrintRow(format, r)
    }
}
```

#### Output: 
```sh
ID      NAME  
123123  Jonh  
123121  Jeff 
```

## License

This project is licensed under the terms of the [MIT](LICENSE) license.
