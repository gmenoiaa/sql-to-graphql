# sql-to-graphql

Generate GraphQL schemas and server based on SQL table structure.

## :warning: Unmaintained

If you want to help maintain or develop this, let me know!

## What?

[GraphQL](https://facebook.github.io/graphql/) is pretty awesome, but getting started can be difficult - especially if you are unfamiliar with the concepts it introduces.

`sql-to-graphql` is a command-line utility that can help you get started. You give it the credentials to an SQL database (MySQL and PostgreSQL currently) and it will inspect the tables it finds and do the following:

- Generate GraphQL-types for each table (including resolvers)
- Generate an HTTP-server based on Hapi that accepts GraphQL queries
- Sets up a basic web-frontend that lets you query the server

## Disclaimer

This utility is intended to help people get started with GraphQL. It is **NOT** intended to be used in production.

## Installation

`yarn`

## Usage

`node cli`

### Options:
  
  - `--relay`, `-r` - Generate Relay-style schema *`(boolean [default: false])`*
  - `--output-dir`, `-o` - Directory to use when generating app *`(string [required])`*
  - `--es6` - Use ES6 for generated code *`(boolean [default: false])`*
  - `--database`, `--db` - Database name *`(string [required])`*
  - `--host`, `-h` - Hostname of database server *`(string [default: "localhost"])`*
  - `--port`, `-P` - Port number of database server *`(number)`*
  - `--user`, `-u` - Username to use when connecting *`(string [default: "root"])`*
  - `--password`, `-p` - Password to use when connecting *`(string [default: ""])`*
  - `--table`, `-t` - Tables to generate type schemas for *`(array [default: "*"])`*
  - `--backend`, `-b` - Type of database *`(string [default: "mysql"])`*
  - `--strip-suffix` - Remove a suffix from table names when generating types *`(array)`*
  - `--strip-prefix` - Remove a prefix from table names when generating types *`(array)`*
  - `--interactive`, `-i` - Interactive mode *`(boolean [default: false])`*
  - `--colors`, `-c` - Colorize the code output *`(boolean [default: false])`*
  - `--use-tabs` - Use tabs for indentation *`(boolean [default: false])`*
  - `--tab-width` - Width of tabs *`(number [default: 2])`*
  - `--quote` - Quote style (single/double) *`(string [default: "single"])`*
  - `--default-description` - The description to use for columns without a comment *`(string [default: "@TODO DESCRIBE ME"])`*
  - `--unaliased-primary-keys`  Disable aliasing of primary key fields to "id" for each type *`(boolean [default: false])`*
  - `--help` - Show help *`(boolean)`*
  
## Example

```
node cli \
  --host localhost \
  --user db_user \
  --password superSecretPassword \
  --database magento_testing \
  --table core_config_data \
  --output-dir ./generated/core_config_data
```

## A note about connections

At the moment, sql-to-graphql tries to guess connections between tables based on naming conventions. This is far from fool-proof, but here's how it works:

Given you have a table called `users` (or `user`) and a table called `posts` (or `post`) and the `posts` table have a column called `user_id`, it will create a connection called `user` on the `Post`-type, giving you the `User` this post belongs to. It will also create a connection on the `User`-type named `posts`, which will return all the posts belonging to this `User`.

How these connections look depends on the options used (namely, `--relay`).

## License

MIT-licensed. See LICENSE.
