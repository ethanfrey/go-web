# Testing

Good test coverage is important.  Not just to make sure that your code has no bugs (I know, it never does), but also to make sure that *other* programmer doesn't make a bug in your code with his refactoring.  Think of test cases not just as checks for you, but watchmen for the future, to make sure nothing breaks.

## Packages

Here are some useful packages to try out:
	
	* https://golang.org/pkg/testing/ (The basis for everything in "go test")
	* https://github.com/stretchr/testify (Nice assert library)
	* https://golang.org/pkg/net/http/httptest/  (Utils for testing http request/responses)


## Techniques:

  * https://elithrar.github.io/article/testing-http-handlers-go/
  * 
  * 


## Running tests

Nice trick with inotify wait to auto-run locally on save:
  http://dave.cheney.net/2016/06/21/automatically-run-your-packages-tests-with-inotifywait