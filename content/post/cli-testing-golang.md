+++
type = "post"
author = "Justin Zimmerman"
keywords = ["CLI", "testing", "Go", "Golang"]
date = "2016-10-18T08:19:39-04:00"
title = "CLI Testing in Go"
description = "Writing tests in Go is a simple process. This tutorial walks through a simple Go CLI and writes a test for loading a file from the operating system."
topics = ["Go", "Testing", "CLI"]
tags = ["Go", "Testing", "CLI"]

+++

# Writing unit tests for Go (Golang) CLIs

A majority of my background has been developing web applications. I've recently changed teams at work to a team that is primarily focused on building a CLI.

Writing tests in Go is a relatively simple process, especially coming from JavaScript where you need multiple modules, and lots of code before you even begin writing tests.

The testing package has most everything you need for writing unit tests. Below is an example CLI test to get started:

```go
package main

import (
  "encoding/json"
	"io/ioutil"
	"os"
	"testing"
)

// a dummy config file to pass in as a slice of bytes
var jsonConfig = []byte(`
  {
    "site-name": "example.com",
    "cache-control": "max-age=86400",
    "publish-dir": "public/"
  }
`)

// Config struct to handle config unmarshalling
type Config struct {
  SiteName string `json:"site-name"`
  CacheControl string `json:"cache-control"`
  PublishDir string `json:"publish-dir"`
}

// LoadConfig will read the given file for the site
// and then load that file into the Config struct for internal usage.
func LoadConfig(path string) (Config, error) {
	config := Config{}
	contents, err := ioutil.ReadFile(path)
	if err != nil {
		return config, err
	}

  err = json.Unmarshal(contents, &config)
  if err != nil {
    return config, err
  }

	return config, nil
}

// TestLoadConfig tests the LoadConfig function to load a config.json file
func TestLoadConfig(t *testing.T) {
	// write config to current folder (0664 denotes the permissions in octal notation)
	ioutil.WriteFile("config.json", jsonConfig, os.FileMode(int(0664)))
	// clean up config.json after tests are completed
	defer os.Remove("config.json")

	config, err := LoadConfig("config.json")
	if err != nil {
		t.Error("Loading  config failed")
	}
	t.Logf("config successfully created: \n %v", config)
}
```

As we can see, writing tests for a CLI doesn't have to be crazy. We create our file, defer the removal of that file, and test the LoadConfig function.

I hope this shows just how simple CLI testing with Go can be.
