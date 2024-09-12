---
layout: post
title: (WIP) Building a REST API in Go with Gin
---

![Image]({{ site.baseurl }}/images/gin-api-header.png)

Go (or Golang) is an open-source language originally developed by Google which has seen a rapid increase in popularity in recent years. Designed to help improve programming productivity, it has quickly established itself as a popular language for backend development thanks to its speed and efficiency.

In this tutorial, I'll showcase how to build a rudimentary REST API in Go using the robust Gin framework. The API will be for a 'record store', and allow users to view, add and and retrieve albums and records from/to a local JSON datafile.

## Prerequisites
Make sure you have the following installed before getting started:
- Go (I'm using version 1.22.6)
- A text editor (Visual Studio Code is a good choice)
- A way of testing the API (curl in a terminal or Postman, for example)
You can verify that you have Go successfully installed by running `go version` in your terminal.

## Project Setup
- Create a new directory for your project\
`mkdir go-album-api`\
`cd go-album-api/`
- Create a *main.go* file. This is where the application code will be located.\
`touch main.go`
- And also a *data.json* file to persistently store our albums.\
`touch data.json`

## Initial main.go Setup
In `main.go`, define `package main` at the top of the file, and declare the following imports:

{% highlight go %}
package main

import (
    "encoding/json"
    "log"
    "net/http"
    "os"
    
    "github.com/gin-gonic/gin"
)
{% endhighlight %}

For this project, the imports we'll be using are:
- **encoding/json**: used to encode/decode data between JSON structure and Go structs (which we'll look at in the next step)
- **log**: used to write output like errors and debug messages to the console
- **net/http**: provides HTTP client and server functionality, essential for this project
- **os**: allows interaction with the operating system, such as reading/writing from files
- **github.com/gin-gonic/gin**: Gin, the web framework we'll be using to build our API.
Don't worry if these import statements throw up errors, they'll resolve themselves when the code is complete.

## Defining a Structure
Next, an album *struct* must be defined. We need to decide what *fields* our albums will have. In this example, we'll do:
- **id**: an identifier for that album (usually unique)
- **title**: the name of the album/record
- **artist**: the name of the artist
- **price**: how much this album will "cost".
Feel free to add any additional fields you can think of!

{% highlight go %}
type album struct {
    ID     string  `json:"id"`
    Title  string  `json:"title"`
    Artist string  `json:"artist"`
    Price  float64 `json:"price"`
}
{% endhighlight %}

## Loading and Saving from JSON
We could simply hardcode our album data and store it in memory, however this would mean our data isn't *persistent*. Any changes made to the data would reset when the server is restarted. To resolve this, it's fairly straightforward to implement functionality to save and load album data to and from a JSON file.

Firstly, we must declare a *slice* of albums to hold the album data in memory. A slice is a dynamic, flexible view into the elements of an array, more powerful and convenient for sequences of data than traditional arrays.

{% highlight go %}
var albums []album
{% endhighlight %}

The below functions read and write JSON data from the *data.json* file. When the server starts, *loadAlbumsFromJSON()* will take the album data from *data.json*, while *saveAlbumsToJSON()* will overwrite the file when new albums are added.

{% highlight go %}
func loadAlbumsFromJSON(filename string) error {
    file, err := os.ReadFile(filename) // read file into memory
    if err != nil { 
        return err // if file cannot be read, return error
    }

    err = json.Unmarshal(file, &albums) // unmarshal data from file into slice
    if err != nil {
        return err
    }
    return nil // no errors, success
}

func saveAlbumsToFile(filename string) error {
    file, err := json.MarshalIndent(albums, "", "  ") // marshal into pretty, readable JSON format
    if err != nil {
        return err // if slice cannot be marshalled, return error
    }

    err = os.WriteFile(filename, file, 0644) // write to JSON file with r/w permissions
    if err != nil {
        return err // if file cannot be written, return error
    }
    return nil // save operation successful
}
{% endhighlight %}
