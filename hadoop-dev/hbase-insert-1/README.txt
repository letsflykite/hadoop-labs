Lab : insert and query  customer data into Hbase
project dir : hbase-insert-1
you can also open the project in eclipse

STEP 1) edit the file : hbase-insert-1/src/hi/hbase/UserInsert.java


STEP 2) complete the TODO items


STEP 3) compile the code:
    $ cd hbase-insert-1
    $ ../compile.sh
this should create a jar file called 'a.jar'

STEP 4) create a users table on hbase
invoke hbase shell
    $ hbase shell
in hbase shell, create a '<your name>_users' table.  Replace <your name> with your username.
    hbase >  create 'users', 'info'


STEP 5) insert data into hbase
run the executable insert.sh
    $ ./insert.sh
or
    $ sh insert.sh

at the end of the run you should see something like:
    inserted 100 users  in 6 ms


STEP 6) verify 'users' table is populated
start hbase shell
    $ hbase shell

    hbase shell > count 'users'
    100 row(s) in 0.0440 seconds

    hbase shell > scan 'users'

the output should look like:
ROW                           COLUMN+CELL
 \x00\x00\x00\x00             column=info:email, timestamp=1365327357752, value=user-0@foo.com
 \x00\x00\x00\x00             column=info:phone, timestamp=1365327357752, value=555-1234
 \x00\x00\x00\x01             column=info:email, timestamp=1365327357757, value=user-1@foo.com
 \x00\x00\x00\x01             column=info:phone, timestamp=1365327357757, value=555-1234
 \x00\x00\x00\x02             column=info:email, timestamp=1365327357758, value=user-2@foo.com
 \x00\x00\x00\x02             column=info:phone, timestamp=1365327357758, value=555-1234



STEP 7) now that we have users table populated, lets run some query
run the file 'query.sh'
    $ ./query.sh
or
    $ sh query.sh
The output might look like:
    querying for userId : 191
         row user=191 : not found
         query time : 0.041 ms

    querying for userId : 39
         email=user-39@foo.com
         query time : 0.0060 ms

We try to query some random userIds.  Take a look at the query time, they are pretty good (in milli seconds or sub-ms range!)
