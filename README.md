Lua Query Builder
=================

LuaQuB is a small query builder module for Lua. I am building this because I'm tired of typing similar queries over and over as strings.

## Usage

Save the `qublua.lua` file (in `src` directory) to a folder listed under Lua's `package.path` or `package.cpath` variable. Call the module in your program by using `require` as follows:

    local Builder = require "qublua"
Create an object by using `.new()` method of Builder module. This object will be used for bulding the query.

    local object = Builder.new()
    object:select( "id, date, time, message, t2.col1, t2.col2" )
    object:from( "tbl1, tbl2 AS t2" )
    object:where( "tbl1.id = t2.remote_id" )
    object:where( "LENGTH(message) < 255" )
    object:limit( 30, 10 )		-- The second argument is offset
To get the compiled query in string format, just call `tostring` passing the `object` as parameter.

    print( tostring(object) )
which will give you the following output

    SELECT id,
    	date,
    	time,
    	message,
    	t2.col1,
    	t2.col2
    FROM tbl1,
    	tbl2 AS t2
    WHERE tbl1.id = t2.remote_id
    	AND LENGTH(message) < 255
    LIMIT 30
    OFFSET 10

## Examples

A few examples will be saved under the `tests` directory.