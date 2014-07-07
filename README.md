go8337
======

This repo demonstrates https://code.google.com/p/go/issues/detail?id=8337

The package structure is:

    github.com/wadey/go8337
    ├── a
    │   ├── b
    │   │   └── b_test.go
    │   └── c
    │       └── c_test.go
    └── z
        └── z.go

If you run the following with go1.3:

    $ go get github.com/wadey/go8337
    $ go test github.com/wadey/go8337/a/...

you will get the error:

    # github.com/wadey/go8337/a/c
    a/c/c_test.go:6: can't find import: "github.com/wadey/go8337/z"
    ok      github.com/wadey/go8337/a/b 0.008s
    FAIL    github.com/wadey/go8337/a/c [build failed]

Even though that package exists. This is because go1.3 gets confused and
thinks it built the .a files for `z` as part of testing `a/b`. But the build
for `a/b` was actually skipped, thus `z` wasn't built.
