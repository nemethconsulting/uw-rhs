## Note on null fields

When setting up your database, you may not have data for all the fields.
You can handle this in a number of different ways depending on your personal
preferences and the field data type.

For Strings: Will accept "" or "TBD" for strings as well as null

For Integers: Won't accept an empty value for integer, but will accept "" & null

For Boolean: will accept null or ""

basically, null, "", or "TBD" will work for all fields. Just can't leave any empty.

If you pass a team id as null, json-server will automatically generate the id for you