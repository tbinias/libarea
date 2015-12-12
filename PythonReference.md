# Introduction #

Area.so Python function cheatsheet


# Functions #


```
Point

    p = Point()     -- return point at (0,0)
    p.x = 10
    p.y = 34
    
    q = Point(2,3)  -- set x,y
    
    r = q * 3       -- scale - r = (6,9)
    r.length()      -- length of vector from (0,0)
    r.dist(q)       -- distance of r from q
    r.normalize()   -- make unit vector
    r - q           -- subtract points
    r + q           -- add points
    
Vertex - a polyline segment

    v = Vertex(p,q)  -- line from point p to point q, user_data =0
    v = Vertex(p,q)  -- line from p to q, set user_data
    v = Vertex(type, point1,point2, user_data)
        type: 0=line,1=ccw arc,-1=cw arc,
        user_data = int
        
    v.p = Point(2,3)
    v.q = Point(4,7)
    v.type = 0
    v.user_data = 4711
    

Curve - a polyline

    c = Curve() -- create empty Polyline
    c.append(Vertex(<params>)) -- append polyline segment
        example:     c.append(area.Vertex(-1, area.Point(1,2), area.Point(3,4)))

    c.getVertices() -- return list of polyline segments
        example:
            for vertex in curve.getVertices():
                ....
                
    c.text() -- return string representation
        example:
        >>> c.text()
        number of vertices = 2
        vertex 1 type = 0, x = 13, y = 29.6158
        vertex 2 type = -1, x = 20.6158, y = 22, xc = 13, yc = 22

    c.NearestPoint(p)  -- return the point in c which is closest to Point p
    c.Reverse()  -- reverse polyline segments in c
    c.getNumVertices() - return number of polyline segments in c
    c.FirstVertex() - return first polyline segment
    c.LastVertex() - return last polyline segment
    c.IsClockwise() - return True if c is clockwise, else false
    c.GetArea()     - return the area covered by c
    c.GetBox(b) -- update Box b with the bounding box of curve

Box - Bounding box 

    b = Box()   -- init a bb object
    b.MinX, b.MaxX,b.MinY,b.MaxY - bb extent
        see Curve and Area GetBox() methods

Area - set of polylines  

    a = Area()  -- init area object
    a.append(c) -- append a polyline to a
    a.getCurves() -- return list of polylines in a
    a.num_curves() -- return number of polylines in a
    a.text() -- return string representation of a

    np = a.NearestPoint(p) - set np to point in a which is nearest to p
    a.GetBox(b) -- update b with the bounding box of a

    a.Offset(distance) -- substitute each polyline in a by its offset polyline 
    a.Subtract(b)   - cut out b from a
    a.Intersect(b)  - set a to intersection of a and b
    a.Union()       - merge polylines in a and b
    
    mystery functions:
    
    a.Reorder() - reorder polylines in an area ?
      an area object must have it's Curve objects correctly oriented; outside curves 
      must be anti-clockwise, inside curves must be clockwise. However, you can add 
      them in any order you want, oriented however you want, and then call a.Reorder(). 
      This will recursively check which curves are inside which and reverse them, 
      if necessary, and put them in them in the right order.
    
    a.FitArcs()  
      internal -  you shouldn't need to worry about this, as it is called 
      automatically after every a.Offset(), a.Subtract(), a.Union(), a.Intersect() 
    a.MakePocketToolpath() 
      this is not finished yet. It is probably only going to be any good for 
      the version of libarea that is build using Clipper. It will create a list
       of curves that are the centre-line of a milling toolpath
    
    a.set_units()
     this should be set to 1.0 for mm and 25.4 for inches. It ensures that 
     internal tolerances are of the right order of magnitude for the values being used.
    
    a.get_units()  - returns that value
    
    a.holes_linked() - with the version of libarea that is built by default, using 
     the GPL Boolean library, an resulting area ( from Subtract, Intersect, Union, 
     Offset ) with islands will actually only have one curve, where one of the spans
     of the curve is a line linking the outside to the island. a.holes_linked() will
     return True. For the version built with Clipper, this will return False, 
     the islands will be separate curves.
 
```
