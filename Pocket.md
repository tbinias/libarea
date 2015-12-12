![http://libarea.googlecode.com/svn/wiki/pocket.png](http://libarea.googlecode.com/svn/wiki/pocket.png)

# Pocket #

This command takes a DXF file and creates a pocketing tool path.
The output is a simplified G-code text file.

I have built a Windows executable, see the downloads page http://code.google.com/p/libarea/downloads/list
This takes various parameters:

-f input file, defaults to input.dxf

-o output file, defaults to output.txt ( simplified gcode text file )

-r round corner value, default 1.0 ( 1.0 for round corners, 1.5 for square corners )

-m material allowance, default 0.0

-s step over, default half of tool diameter

-c clearance height, default 5

-t start depth ( top of material ), default 0

-i step down, default 1

-z final depth, default -3

-q rapid down to height, default 2

-d tool diameter, default 3

-n from center, default center ( can be "center" or "outside" )

-p output style, 0 is like "3.141529", 1 is like "+00003.141"

## Islands ##

You must draw the islands with a different direction than the outside shape; if the outside shape is clockwise the islands must be drawn anti-clockwise, if the ouside is anti-clockwise the islands must be clockwise. ( I plan to be able to automatically sort these out one day ).

## Limitations ##

The cutter plunges directly down into the material.
Also, it rapids up and down between each step over to be sure not to cut through part of the shape. This is fine for cutting one-off shapes with a slot cutter, but is not optimised, and is no good for an endmill tool which can't plunge down into the material.

![http://libarea.googlecode.com/svn/wiki/pocket2.png](http://libarea.googlecode.com/svn/wiki/pocket2.png)