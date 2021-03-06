# gosqlbencher

[![Build Status](https://travis-ci.org/iwanbk/gosqlbencher.svg?branch=master)](https://travis-ci.org/iwanbk/gosqlbencher)
[![Go Report Card](https://goreportcard.com/badge/github.com/iwanbk/gosqlbencher)](https://goreportcard.com/report/github.com/iwanbk/gosqlbencher)
[![codecov](https://codecov.io/gh/iwanbk/gosqlbencher/branch/master/graph/badge.svg)](https://codecov.io/gh/iwanbk/gosqlbencher)

Tool to benchmark your Go SQL ecosystem: query, driver, and the server.

## Why using this tool 

Why using this tool instead of existing tools like pgbench and SysBench?

Go's [database/sql](https://golang.org/pkg/database/sql/) package has it's own behaviour that different with 
both `pgbench` and `SysBench`. It already has it's own connection pool and also has it's own way to manage
the database connection and prepared statements.

## Things to observe/benchmark

There are many things we could observe/benchmark with this tool

### Database server

Play with your DB server settings and benchmark it againts your query.

### Database query

#### Test various queries like exec, query, and query_row.

Supported DB queries:
- [x] Exec
- [x] ExecContext
- [x] Query
- [x] QueryContext
- [ ] QueryRow
- [ ] QueryRowContext
- [ ] Transaction

TODO : scan the result of `Query%` queries.

#### Test between using prepared statement, placeholder, and plain query.

Supported query modes:
- prepared statement:
  - create it once on the initialization
  - create it on each query
- using placeholder (e.g.: `$1` in postgresql)
- plain query (e.g. using Go's `%d` and `%s`)

### Driver

Easily switch between supported drivers and see the difference.

Supported drivers:
- [x] github.com/lib/pq
- [ ] github.com/jackc/pgx
- [ ] github.com/mattn/go-sqlite3
- [ ] github.com/ziutek/mymysql
- [ ] github.com/go-sql-driver/mysql

### Database Settings

TODO : Will [SetMaxOpenConns](golang.org/pkg/database/sql/#DB.SetMaxOpenConns) affect the performance?

### Set number of goroutines

`num_worker` option set the number of goroutines which execute the queries.
In web application, it simulates the number of concurrent requests you have at any given time.

## Quick Start

Build
```bash
go build -v
```

See the help

```bash
$ ./gosqlbencher -h
Usage of ./gosqlbencher:
  -plan string
        gosqlbencher plan file (default "plan.yaml")
```

Create test table and execute `insert` test
```bash
./gosqlbencher -plan=insert.plan.yaml
```

Execute various `select` tests
```bash
./gosqlbencher -plan=query.plan.yaml 
```

## Configuration

TODO

## TODO

- profiling
- all `TODO` Above
- all unchecked mark above