# How do I address errors when I run tests?

## What's happening

If you get Go errors after you issue the `make run-tests-local` command multiple times, you might have a corrupt Go cache.

## Why it's happening

Go caches the build outputs for reuse. Data is deleted periodically.

## How to fix it

Run `go clean -cache` to remove all cached data from the build process. Then run the tests again. The `-clean` option removes all cached packages, builds, and cached downloaded modules.

You can also run the command with these more specific options:
- The `-testcache` option removes the cached test results in the build cache.
- The `-modcache` option cleans the module download cache.

For more information, see [Build and test caching](https://pkg.go.dev/cmd/go#hdr-Build_and_test_caching) in the Go documentation.
