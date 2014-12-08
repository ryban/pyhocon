pyhocon
=======

[![Build Status](https://travis-ci.org/chimpler/pyhocon.svg)](https://travis-ci.org/chimpler/pyhocon)

HOCON parser for Python

## Specs

https://github.com/typesafehub/config/blob/master/HOCON.md

## Features
The parsed config can be seen as a nested dictionary (with types automatically inferred) where values can be accessed using normal
dictionary getter (e.g., `conf['a']['b']` or using paths like `conf['a.b']`) or via the methods `get`, `get_int` (throws an exception
if it is not an int), `get_string`, `get_list`, `get_double`, `get_bool`, `get_config`.

## Usage

    from pyhocon import ConfigFactory
    
    conf = ConfigFactory.parse_file('samples/database.conf')
    host = conf.get_string('databases.mysql.host')
    port = conf['databases.mysql.port']
    username = conf['databases']['mysql']['username']
    password = conf.get_config('databases')['mysql.password']

## Examples of file supported

    //
    // You can use # or // for comments
    //
    {
      databases {
        # MySQL
        mysql {
          host = "abc.com" # change it
          port = 3306 # default
          username: scott // can use : or =
          password = tiger, // can optionally use a comma
          // number of retries
          retries = 3
        }
      }
      // multi line support
      motd = """
            Hello "man"!
            How is it going?
             """
      ips = [
        192.168.0.1,
        "192.168.0.2", // optional quotes
        192.168.0.3, # can have a trailing , which is ok
      ]
    }
  
## TODO

Items                                  | Status
-------------------------------------- | :-----:
Comments                               | :white_check_mark:
Omit root braces                       | :white_check_mark:
Key-value separator                    | :white_check_mark:
Commas                                 | :white_check_mark:
Whitespace                             | :white_check_mark:
Duplicate keys and object merging      | :white_check_mark:
Unquoted strings                       | :white_check_mark:
Multi-line strings                     | :white_check_mark:
String value concatenation             | :white_check_mark:
Array concatenation                    | :x:
Object concatenation                   | :white_check_mark:
Arrays without commas                  | :x:
Path expressions                       | :x:
Paths as keys                          | :white_check_mark:
Substitutions                          | :x:
Self-referential substitutions         | :x:
The `+=` separator                     | :x:
Includes                               | :x:
Include semantics: merging             | :x:
Include semantics: substitution        | :x:
Include semantics: missing files       | :x:
Include semantics: file formats and extensions     | :x:
Include semantics: locating resources              | :x:
Conversion of numerically-index objects to arrays  | :x:

API Recommendations                                        | Status
---------------------------------------------------------- | :----:
Conversion of numerically-index objects to arrays          | :x:
Automatic type conversions                                 | :x:
Units format                                               | :x:
Duration format                                            | :x:
Size in bytes format                                       | :x:
Config object merging and file merging                     | :x:
Java properties mapping                                    | :x:
