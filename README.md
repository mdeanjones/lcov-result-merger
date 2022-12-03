# LCOV Result Merger

[![npm version](https://badge.fury.io/js/lcov-result-merger.svg)](https://badge.fury.io/js/lcov-result-merger)
![Build Status](https://github.com/mweibel/lcov-result-merger/actions/workflows/ci.yml/badge.svg?branch=master)
[![Coverage Status](https://coveralls.io/repos/github/mweibel/lcov-result-merger/badge.svg?branch=master)](https://coveralls.io/github/mweibel/lcov-result-merger?branch=master)

When you have multiple test suites for the same application you still want to
have the code coverage across all test suites.

This tool will handle this for you.

# Usage

```bash
./node_modules/.bin/lcov-result-merger 'FILE_PATTERN' ['OUTPUT_FILE']
```

# Examples

## Use stdout
1. Generate LCOV Code Coverage into different files, e.g. `build/coverage/coverage_X.log`
2. Run `./node_modules/.bin/lcov-result-merger 'build/coverage/coverage_*.log'`
3. Use the stdout to pipe it to e.g. [Coveralls](http://coveralls.io)
4. Done.

## Use merged output file
1. Generate LCOV Code Coverage into different files, e.g. `build/coverage/coverage_X.log`
2. Run `./node_modules/.bin/lcov-result-merger 'build/coverage/coverage_*.log' 'target/coverage/coverage_merged.log'`
3. Done. Enjoy your merged file.

## Prepend source file paths
Modify source file paths to be relative to the working directory that the merge operation was run in. Useful in
monorepos where each child package gathers its own metrics.

```bash
./node_modules/.bin/lcov-result-merger 'FILE_PATTERN' ['OUTPUT_FILE'] --prepend-source-files
```

Since coverage output is rarely written directly into the project root, use `--prepend-path-fix` to describe the
relative path between the lcov file and the project root. The default simply points to one directory up, "..", which
works well for common tools such as [NYC](https://github.com/istanbuljs/nyc) that write to a `/coverage` directory.

```bash
./node_modules/.bin/lcov-result-merger 'FILE_PATTERN' ['OUTPUT_FILE'] --prepend-source-files --prepend-path-fix "../src"
```
