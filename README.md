# Free SQLite Encryption Extension (FSEE)

The Free SQLite Encryption Extension (FSEE) is an add-on to the public domain version of SQLite that allows an application to read and write encrypted database files. Four different encryption algorithms are supported:

	AES-128 in OFB mode
	AES-128 in CCM mode
	AES-256 in OFB mode

## COMPILE

1. Download [SQLite 3.7.14.1](http://www.sqlite.org/sqlite-amalgamation-3071401.zip). Unzip it to the "sqlite3" folder.

2. Download [Wxsqlite3-3.0.0.1](http://sourceforge.net/projects/wxcode/files/Components/wxSQLite3/). Unzip the “wxsqlite3-3.0.0.1\wxsqlite3-3.0.0.1\sqlite3\secure\src” folder to "sqlite3".

3. Use [visual studio](http://download.microsoft.com/download/B/4/8/B4870509-05CB-447C-878F-2F80E4CB464C/vs_community.exe) to compile the solution.

4. In the bin folder, you will find the "sqlite.dll" and "sqlite.lib"

5. use the "sqlite3_key" and "sqlite3_rekey" api

## API

```c
int sqlite3_key( sqlite3 *db, const void *pKey, int nKey)

int sqlite3_rekey( sqlite3 *db, const void *pKey, int nKey)
```

## USAGE

```c
#include<stdio.h>
#include<sqlite3.h>
#include<stdlib.h>

int main(int argc, char** args)
{
    // Create an int variable for storing the return code for each call
    int retval;
    
    // The number of queries to be handled,size of each query and pointer
    int q_cnt = 5, q_size = 150, ind = 0;
    char **queries = malloc(sizeof(char) * q_cnt * q_size);
        
    // A prepered statement for fetching tables
    sqlite3_stmt *stmt;
    
    // Create a handle for database connection, create a pointer to sqlite3
    sqlite3 *handle;
    
    // try to create the database. If it doesnt exist, it would be created
    // pass a pointer to the pointer to sqlite3, in short sqlite3**
    retval = sqlite3_open("sampledb.sqlite3", &handle);
    retval = sqlite3_key(handle, "password", 3);
    // If connection failed, handle returns NULL
    if(retval)
    {
        printf("Database connection failed\n");
        return -1;
    }
    printf("Connection successful\n");
    
    // Create the SQL query for creating a table
    char create_table[100] = "CREATE TABLE IF NOT EXISTS users (uname TEXT PRIMARY KEY,pass TEXT NOT NULL,activated INTEGER)";
    
    // Execute the query for creating the table
    retval = sqlite3_exec(handle,create_table, 0, 0, 0);
    
    // Insert first row and second row
    queries[ind++] = "INSERT INTO users VALUES('manish', 'mani', 1)";
    retval = sqlite3_exec(handle,queries[ind-1], 0, 0, 0);

    queries[ind++] = "INSERT INTO users VALUES('mehul','pulsar',0)";
    retval = sqlite3_exec(handle,queries[ind-1], 0, 0, 0);
    
    // select those rows from the table
    queries[ind++] = "SELECT * from users";
    retval = sqlite3_prepare_v2(handle,queries[ind-1], -1, &stmt, 0);
    if(retval)
    {
        printf("Selecting data from DB Failed\n");
        return -1;
    }
    
    // Read the number of rows fetched
    int cols = sqlite3_column_count(stmt);
        
    while(1)
    {
        // fetch a row's status
        retval = sqlite3_step(stmt);
        
        if(retval == SQLITE_ROW)
        {
            // SQLITE_ROW means fetched a row
            
            // sqlite3_column_text returns a const void* , typecast it to const char*
            for(int col=0; col < cols; col++)
            {
                const char *val = (const char*)sqlite3_column_text(stmt, col);
                printf("%s = %s\t",sqlite3_column_name(stmt,col),val);
            }
            printf("\n");
        }
        else if(retval == SQLITE_DONE)
        {
            // All rows finished
            printf("All rows fetched\n");
            break;
        }
        else
        {
            // Some error encountered
            printf("Some error encountered\n");
            return -1;
        }
    }
    
    // Close the handle to free memory
    sqlite3_close(handle);
    return 0;
}
```


## LICENSE

Copyright 2015 shenghe

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.