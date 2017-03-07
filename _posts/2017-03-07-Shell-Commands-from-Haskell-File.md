---
layout: post
title: Shell Commands from Haskell file
date: 2017-03-07
---
# Running shell commands from inside Haskell file

During development, the user may want to quickly reset their SQLite database with a "fresh start" SQL file. This could look like the following shell command:

`$ sqlite3 db_name < fresh_start.sql`

However, it is also possible to run this command from within a Haskell file so that the user does not need to switch environments. 

The package [System.Process](https://hackage.haskell.org/package/process-1.6.0.0/docs/System-Process.html) features operations for creating and interacting with sub-processes. One of its functions, `system`, can run a shell command as a String and return an exit code. 

Below is a snippet that pipes a SQL file, which drops all of the database tables, to sqlite3. Obviously being able to wipe a database with two words is insanely insecure (even with the helpful warning), but this package is perfect for quick development environments.

```sql
//reset_db.sql
DROP TABLE IF EXISTS employees

CREATE TABLE employee (
        id INTEGER PRIMARY KEY, 
        name TEXT
        );

INSERT INTO employees (name) VALUES ('employeeOne');
```

```haskell
--Main.hs
import Database.SQLite.Simple
import qualified System.Process as SP
import System.Exit

--Rebuild database!
build :: IO ExitCode
build = do
    print "This will reset the DB, type yes if you're sure"
    answer <- getLine
    if answer == "yes"
    then SP.system "sqlite3 tools.db < build_db.sql"
    else SP.system "Nothing changed"
```
