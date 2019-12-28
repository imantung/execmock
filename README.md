# ExecMock

[![Project Status: Concept – Minimal or no implementation has been done yet, or the repository is only intended to be a limited example, demo, or proof-of-concept.](https://www.repostatus.org/badges/latest/concept.svg)](https://www.repostatus.org/#concept)

Mocking for go exec package using monkey patching

## Background

`exec.Command` and `exec.CommandContext` is frequently used and need mock for testing purpose. Using monkey-patching to replace the function and return modified `Command` struct.

Reference:
- https://github.com/bouk/monkey
- https://golang.org/src/os/exec/exec.go
- https://www.joeshaw.org/testing-with-os-exec-and-testmain/

## Usage Design

```go
func TestFunction(t *testing.T){
    mock := execmock.New()
    defer mock.Close() 

    mock.CommandContext("mkdir").Args("some-folder").Return(errors.New("some-error"))

    err = exec.Command("mkdir", "some-folder").Run() // return "some-error"

    // ....

}
```