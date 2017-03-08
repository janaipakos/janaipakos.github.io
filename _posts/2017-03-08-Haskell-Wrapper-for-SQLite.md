---
layout: post
title: Haskell Wrapper for SQLite
date: 2017-03-08
---

It's easy to create a SQLite/SQL wrapper with Haskell. Doing so can create an abstraction between the user and the database, which will limit the user's ability to directly interact with the database, and provide more safety with stricter data types and error handling. To create this wrapper, the user will just need to model CRUD commands in Haskell and link them to a database.

The general steps to hooking a database such as SQLite to Haskell are:

- Create DB and tables in SQL file
- Model data types in Main.hs after tables and fields
- Create instances of Show
- Recreate CRUD functions in Haskell
- Tie functions together in main IO action

## Create DB and tables in SQL file

I'm using SQLite 3 for this example, and below is when the user will interact with SQLite on the command line. To start, create a regular .sql file, and within that create and populate the SQL tables. This can be `users`, `todos`, `employees`, whatever. Verify that everything is working with the following commands:

```shell
$ sqlite3 <dbname> < <sqlfile.sql>
```

```sql
sqlite> select * from <tablename>
```

If a result gets returned, all good.

## Model data types in Main.hs after tables and fields

Compare the SQL table with the Haskell data type. In more complicated projects, the user could use more advanced types such as Date or Time. But this is the connection between the Haskell file and the SQL values.

```sql
CREATE TABLE todo
    (
    id INTEGER PRIMARY KEY,
    taskName TEXT,
    description TEXT,
    status TEXT
    );
```

```haskell
data Todo = Todo
    { taskId :: Int
    , taskName :: String
    , description :: String
    , status :: String
    }
```

## Create instances of Show

Next, create instances of Show to allow the CRUD function results to print to the terminal.

```haskell
instance Show Todo where
    show todo = mconcat [ show $ taskId todo
                        , ".) "
                        , taskName todo
                        , "\n description: "
                        , description todo
                        , "\n status: "
                        , status todo
                        , "\n"
                        ]
```

## Recreate CRUD functions in Haskell

Penultimately, link CRUD commands to Haskell functions. You'll notice that these functions provide the values that are in effect passed to the SQL tables, and the SQL commands to do so are within these functions. One example could be:

```haskell
addEmployee :: String -> String -> IO ()
addEmployee name description = withConn "employees.db" $
                \conn -> do
                  execute conn "INSERT INTO employee (name,description)
                                VALUES (?,?)"
                  (name, description)
                  print "employee added"
```

## Tie functions together in main IO action

As a last step, tie everything together in a main function, perhaps presenting the user with some CRUD choices that call each related function. A working example is in the GitHub repo here: [SQLite + Haskell Todo List](https://github.com/janaipakos/rc-checkins)

## Learn Haskell

Most of this project followed Will Kurt's book for Manning [*Learn Haskell*](https://www.manning.com/books/learn-haskell).
