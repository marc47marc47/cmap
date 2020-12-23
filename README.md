# concurrent map [![Build Status](https://travis-ci.com/marc47marc47/cmap.svg?branch=master)](https://travis-ci.com/orcaman/cmap)

As explained [here](http://golang.org/doc/faq#atomic_maps) and [here](http://blog.golang.org/go-maps-in-action), the `map` type in Go doesn't support concurrent reads and writes. `cmap` provides a high-performance solution to this by sharding the map with minimal time spent waiting for locks.

Prior to Go 1.9, there was no concurrent map implementation in the stdlib. In Go 1.9, `sync.Map` was introduced. The new `sync.Map` has a few key differences from this map. The stdlib `sync.Map` is designed for append-only scenarios. So if you want to use the map for something more like in-memory db, you might benefit from using our version. You can read more about it in the golang repo, for example [here](https://github.com/golang/go/issues/21035) and [here](https://stackoverflow.com/questions/11063473/map-with-concurrent-access)

for [pkg go doc](https://pkg.go.dev/github.com/marc47marc47/cmap)
The [original source code](https://github.com/orcaman/concurrent-map)

## usage

Import the package:

```go
import (
	"github.com/marc47marc47/cmap"
)

```

```bash
go get "github.com/marc47marc47/cmap"
```

The package is now imported under the "cmap" namespace.

## example

```go

	// Create a new map.
	m := cmap.NewCmap()

	// Sets item within map, sets "bar" under key "foo"
	m.Set("foo", "bar")

	// Retrieve item from map.
	if tmp, ok := m.Get("foo"); ok {
		bar := tmp.(string)
	}

	// Removes item under key "foo"
	m.Remove("foo")

```

For more examples have a look at cmap_test.go.

Running tests:

```bash
go test "github.com/marc47marc47/cmap"
```

## guidelines for contributing

Contributions are highly welcome. In order for a contribution to be merged, please follow these guidelines:
- Open an issue and describe what you are after (fixing a bug, adding an enhancement, etc.).
- According to the core team's feedback on the above mentioned issue, submit a pull request, describing the changes and linking to the issue.
- New code must have test coverage.
- If the code is about performance issues, you must include benchmarks in the process (either in the issue or in the PR).
- In general, we would like to keep `cmap` as simple as possible and as similar to the native `map`. Please keep this in mind when opening issues.

## language
- [中文说明](./README-zh.md)

## license
MIT (see [LICENSE](https://github.com/marc47marc47/cmap/blob/master/LICENSE) file)
