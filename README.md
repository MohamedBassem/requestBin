# RequestBin

[![Build Status](https://travis-ci.org/MohamedBassem/requestBin.svg?branch=master)](https://travis-ci.org/MohamedBassem/requestBin)
[![Coverage Status](https://coveralls.io/repos/github/MohamedBassem/requestBin/badge.svg?branch=master)](https://coveralls.io/github/MohamedBassem/requestBin?branch=master)
[![GoDoc](https://godoc.org/github.com/MohamedBassem/requestBin?status.svg)](https://godoc.org/github.com/MohamedBassem/requestBin)


RequestBin is a package for testing the outgoing http requests initiated from a function. The package creates a mock server and passes the URL to the function to be tested and then collects all the requests that the server received.

### Example

```go
func ExampleCaptureRequests() {
	reqs := NewRequestBin(MockServerConfig{RequestTimeout: 1}).CaptureRequests(func(url string) {
		http.Post(url, "text/plain", strings.NewReader("Hello"))
		http.Post(url, "text/plain", strings.NewReader("It's me"))
	})

	fmt.Println(reqs[0].Body) // Hello
	fmt.Println(reqs[1].Body) // It's me
}

```

The server can be stopped after a certain amount of seconds, after a certain amount of requests, whenever it doesn't receive any new requests for a certain amount of time or any combination of the three.


### API
The API is very simple and you can check it on [GoDoc](https://godoc.org/github.com/MohamedBassem/RequestBin). Reading the tests is also a good way for understanding the API.


### Usecase
For a usecase you can read my blog post about this package : [http://blog.mbassem.com/2016/02/09/requestbin2/](http://blog.mbassem.com/2016/02/09/requestbin2/).

### Notes
The name RequestBin is originally used in [http://requestb.in/](http://requestb.in/) which basically does the same thing but using a web interface.

### Contribution
Your contributions and ideas are welcomed through issues and pull requests.
