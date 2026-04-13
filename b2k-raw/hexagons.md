Mar 2013, updated in Mar 2015, Apr 2018, Feb 2019, May 2020, Oct 2021, Dec 2022, Feb 2023, Oct 2024, Mar 2025

  

    
      
      

        This guide will cover various ways to make hexagonal grids, the relationships between different approaches, and common formulas and algorithms.
        I've been [collecting hex grid resources](http://www-cs-students.stanford.edu/~amitp/gameprog.html#hex)[1] for 35 years. I wrote this guide to the most elegant approaches that lead to the simplest code, starting from the guides by [Charles Fu](http://www-cs-students.stanford.edu/~amitp/Articles/Hexagon2.html)[2] and [Clark Verbrugge](http://www-cs-students.stanford.edu/~amitp/Articles/HexLOS.html)[3]. Most parts of this page are interactive. To get an offline copy of this page, use your browser's File → Save As (preserves interactivity) or File → Print (loses interactivity).
      

    
      - [Geometry](#basics)

      - [Coordinate systems](#coordinates)

      - [Conversions](#conversions)

      - [Neighbors](#neighbors)

      - [Distances](#distances)

      - [Line drawing](#line-drawing)

      - [Range](#range)

      - [Rotation](#rotation)

      - [Reflection](#reflection)

      - [Rings and Spirals](#rings)

      - [Field of view](#field-of-view)

      - [Hex to pixel](#hex-to-pixel)

      - [Pixel to hex](#pixel-to-hex)

      - [Rounding](#rounding)

      - [Map storage](#map-storage)

      - [Wraparound maps](#wraparound)

      - [Pathfinding](#pathfinding)

      - [More reading](#references)

    

    

      The code samples on this page are written in pseudo-code;
      they're meant to be easy to read and understand. [The implementation guide](implementation.html) has code in C++, Javascript, C#, Python, Java, Typescript, and more.
    

    

    

    
    This page includes interactive diagrams that require
    your browser to have SVG and Javascript enabled.

  

  

  

    

      Now let's assemble hexagons into a grid. With square grids, there's one obvious way to do it. With hexagons, there are multiple approaches. I like cube coordinates for algorithms and axial or doubled for storage.
    

    ### 
Offset coordinates[#](#coordinates-offset)

    

      The most common approach is to offset every other column or row. Columns are named `col` (q). Rows are named `row` (r). You can either offset the odd or the even column/rows, so the horizontal and vertical hexagons each have two variants.
    
      
    

      
      
      
      
    
    
    

    ### 
Cube coordinates[#](#coordinates-cube)

    

      
        
        

          Another way to look at hexagonal grids is to see that there are *three* primary axes, unlike the *two* we have for square grids.
          There's an elegant symmetry with these.
        

        

          Let's take a cube grid and **slice** out a diagonal plane at `x + y + z = 0`.
          This is a *weird* idea but it helps us with hex grid algorithms:
        

        
          - 3D cartesian coordinates follow standard vector operations: we can add/subtract coordinates, multiply/divide by a scalar, etc. We can reuse these operations with hexagonal grids. Offset coordinates do not support these operations.

          - 3D cartesian coordinates have existing algorithms like distances, rotation, reflection, line drawing, conversion to/from screen coordinates, etc. We can adapt these algorithms to work on hexagonal grids.

        
            
      

      

    

    
    
    

      
        
        ### 
Axial coordinates[#](#coordinates-axial)

        

          The axial coordinate system, sometimes called “trapezoidal” or “oblique” or “skewed”, is **the same as the cube system** except we don't *store* the s coordinate. Since we have a constraint  `q + r + s = 0`, we can calculate `s = -q-r` when we need it.
        

      
      
      

      
        

          The axial/cube system allows us to add, subtract, multiply, and divide with hex coordinates. The offset coordinate systems do not allow this, and that's part of what makes algorithms simpler with axial/cube coordinates.
        

      
    

    ### 
Doubled coordinates[#](#coordinates-doubled)

    

      

        Consider doubled instead of offset coordinates. It makes many of the algorithms easier to implement. Instead of alternation, the doubled coordinates *double* either the horizontal or vertical step size. It has a constraint `(col + row) mod 2 == 0`. In the horizontal (pointy top hex) layout it increases the column by 2 each hex; in the vertical (flat top hex) layout it increases the row by 2 each hex. This allows the in-between values for the hexes that are halfway in between:
      

      

        

        

      

      

        I haven't found much information about this system — tri-bit.com called it [interlaced](https://web.archive.org/web/20090205120106/http://sc.tri-bit.com/Hex_Grids)[4], rot.js calls it [double width](https://ondras.github.io/rot.js/manual/#hex/indexing)[5], and [this paper](https://www.researchgate.net/publication/235779843_Storage_and_addressing_scheme_for_practical_hexagonal_image_processing?_sg=flKEA6rk1KmOpC4LBjQJN_-NBuiR1KJtJt-XeYRXnd0z_MNUrB2gjb2FKV3iBoKg988P2xHCpQ)[6] calls it rectangular. Other possible names: brick or checkerboard. I'm not sure what to call it. Tamás Kenéz sent me the core algorithms (neighbors, distances, etc.). If you have any references, please send them to me.
      

    

    ### 
Others[#](#coordinates-other)

    

      In [previous versions of this document](../hexagons-v2/), I used x z y for hexagonal coordinates and *also* for cartesian coordinates, and then I also used q r s for hexagonal coordinates. To avoid confusion in this document, I'll use the names q r s for hexagonal coordinates (with the constraint `q + r + s = 0`), and I'll use the names x y z for cartesian coordinates.
    
    
    

      There are *many* different valid cube hex coordinate systems. Some of them have constraints other than `q + r + s = 0`. I've shown only one of the many systems. There are also *many* different valid axial hex coordinate systems, found by using reflections and rotations. Some have the 120° axis separation as shown here and some have a 60° axis separation. 
    

    

      There are also cube systems that use `q-r, r-s, s-q`. One of the interesting properties of that system is that it reveals [hexagonal directions](directions.html).
    

    

      In addition to the [flat spiral coordinate systems](#rings-spiral-coordinates) shown later on this page, there are nested/recursive spiral systems. See [this question](https://gamedev.stackexchange.com/questions/71785/converting-between-spiral-honeycomb-mosaic-and-axial-hex-coordinates)[7] on stackoverflow, or this [Spiral Architecture for Machine Vision](https://opus.lib.uts.edu.au/bitstream/2100/280/11/02Whole.pdf)[8] (1996), or this [diagram about "generalized balanced ternary" coordinates](https://web.archive.org/web/20120303114550/http://www.pyxisinnovation.com/pyxwiki/index.php?title=Generalized_Balanced_Ternary)[9], or this [An isomorphism between the p-adic integers and a ring associated with a tiling of N-space by permutohedra](https://www.sciencedirect.com/science/article/pii/0166218X9200186P)[10] (1994) ([DOI](https://doi.org/10.1016/0166-218X(92)00186-P)[11]), or
      this [discussion on reddit](https://old.reddit.com/r/gamedev/comments/19wmvn/a_data_structure_for_a_game_board_with_hexagonal/c8s9qbe/)[12]. There's a [Clojure library](https://github.com/SimonWailand/hexwrench)[13] implementing Generalized Balanced Ternary. Also see the Gosper Curve, [here](https://patricksurry.github.io/posts/flowsnake/)[14] and [here](https://metacpan.org/pod/Math::PlanePath::FlowsnakeCentres)[15].
    

    ### 
Recommendations[#](#coordinates-comparison)

    

      What do I recommend?
    
    
    
      
        

Offset
Doubled
Axial
Cube

      
      
        
Pointy rotation
evenr, oddr
doublewidth
axial
cube

        
Flat rotation
evenq, oddq
doubleheight

        
Other rotations
no
yes

        
Vector operations (add, subtract, scale)
no
yes
yes
yes

        
Array storage
rectangular
no*

rhombus*

no*

        
Hash storage
any shape
any shape

        
Hexagonal symmetry
no
no
no
yes

        
Easy algorithms
few
some
most
most

      
    

    

      * rectangular maps require an adapter, shown in the [map storage section](#map-storage)
    
    
    

      My recommendation: if you are only going to use rectangular maps, consider the **Doubled** or **Offset** system that matches your map orientation. For maps with any other shaped maps, use **Axial**/**Cube**. Note that Axial (q,r) and Cube (q,r,s) are essentially the same system. Store coordinates as Axial, and calculate s in algorithms that need it.
    
    
  

  

    

      It is likely that you will use axial or offset coordinates in your project, but many algorithms are simpler to express in axial/cube coordinates. Therefore you need to be able to convert back and forth.
    

    ### 
Axial coordinates[#](#conversions-axial)

    

    ### 
Offset coordinates[#](#conversions-offset)

    
    
    ### 
Doubled coordinates[#](#conversions-doubled)

    

  

  
  
    
    

      Given a hex, which 6 hexes are neighboring it? As you might
      expect, the answer is simplest with cube coordinates, still
      pretty simple with axial coordinates, and slightly trickier with
      offset coordinates. We might also want to calculate the 6
      “diagonal” hexes.
    

    ### 
Cube coordinates[#](#neighbors-cube)

    

    ### 
Axial coordinates[#](#neighbors-axial)

    
    
    ### 
Offset coordinates[#](#neighbors-offset)

    

      As with cube and axial coordinates, we'll build a table of the numbers we need to add to `col` and `row`. However **offset coordinates can't be safely subtracted and added**. For example, moving southeast from (0, 0) takes us to (0, +1), so we might put (0, +1) into the table for moving southeast. But moving southeast from (0, +1) takes us to (+1, +2), so we would need to put (+1, +1) into that table. *The amount we need to add depends on where in the grid we are*.
    
    
    

       Since the movement vector is different for odd and even columns/rows, we will need two separate lists of neighbors. **Pick a grid type** to see the corresponding code.
    

    
    
    

      Using the above lookup tables is the easiest way to to calculate neighbors. It's also possible to [derive these numbers](derive-hex-neighbor-formula.html), for those of you who are curious.
    

    ### 
Doubled coordinates[#](#neighbors-doubled)

    

      Unlike offset coordinates, the neighbors for doubled coordinates do *not* depend on which column/row we're on. They're the same everywhere, like axial/cube coordinates. Also unlike offset coordinates, we can safely subtract and add doubled coordinates, which makes them easier to work with than offset coordinates.
    

    
    
    ### 
Diagonals[#](#neighbors-diagonal)

    

  

  

    ### 
Cube coordinates[#](#distances-cube)

    

      
        
        

          Since cube hexagonal coordinates are based on 3D cube coordinates, we can *adapt* the distance calculation to work on hexagonal grids. Each hexagon corresponds to a cube in 3D space. Adjacent hexagons are distance 1 apart in the hex grid but distance 2 apart in the cube grid. For every 2 steps in the cube grid, we need only 1 step in the hex grid. In the 3D cube grid, Manhattan distances are `abs(dx) + abs(dy) + abs(dz)`. The distance on a hex grid is half that:
        

        

function cube_subtract(a, b):
    return Cube(a.q - b.q, a.r - b.r, a.s - b.s)

function cube_distance(a, b):
    var vec = cube_subtract(a, b)
    return (abs(vec.q) + abs(vec.r) + abs(vec.s)) / 2
    // or: (abs(a.q - b.q) + abs(a.r - b.r) + abs(a.s - b.s)) / 2

        

          An equivalent way to write this is by noting that one of the
          three coordinates must be the sum of the other two, then picking
          that one as the distance. You may prefer the “divide by two”
          form above, or the “max” form here, but they give the same result:
        
    
        

function cube_subtract(a, b):
    return Cube(a.q - b.q, a.r - b.r, a.s - b.s)

function cube_distance(a, b):
    var vec = cube_subtract(a, b)
    return max(abs(vec.q), abs(vec.r), abs(vec.s))
    // or: max(abs(a.q - b.q), abs(a.r - b.r), abs(a.s - b.s))

        

          The maximum of the three coordinates is the distance. You
          can also use the max of `abs(vec.q-vec.r), abs(vec.r-vec.s),
          abs(vec.s-vec.q)` to figure out which of the 6 “wedges” a hex is in; see [diagrams here](directions.html).
        
    
      
      
      

      

        Xiangguo Li's 2013 paper [*Storage and addressing scheme for practical hexagonal image processing.*](https://scholar.google.com/scholar?q=Storage+and+addressing+scheme+for+practical+hexagonal+image+processing)[18] ([DOI](https://doi.org/10.1117/1.JEI.22.1.010502)[19]) gives a formula for Euclidean distance, which can be adapted to axial coordinates: `sqrt(dq² + dr² + dq*dr)`. 
      
      
    
    
    ### 
Axial coordinates[#](#distances-axial)

    
    

      In the axial system, the third coordinate is implicit. We can always [convert](#conversions) axial to cube to calculate distance:
    

    

function axial_distance(a, b):
    var ac = axial_to_cube(a)
    var bc = axial_to_cube(b)
    return cube_distance(ac, bc)

    

      Once we inline those functions it ends up as:
    

    

function axial_distance(a, b):
    return (abs(a.q - b.q) 
          + abs(a.q + a.r - b.q - b.r)
          + abs(a.r - b.r)) / 2

    

      which can also be written:
    
       
    

function axial_subtract(a, b):
    return Hex(a.q - b.q, a.r - b.r)

function axial_distance(a, b):
    var vec = axial_subtract(a, b)
    return (abs(vec.q)
          + abs(vec.q + vec.r)
          + abs(vec.r)) / 2

    

      There are lots of different ways to write hex distance in axial coordinates. No matter which way you write it, *axial hex distance is derived from the Mahattan distance on cubes*. For example, the [“difference of differences”](https://web.archive.org/web/20210302023226/http://3dmdesign.com/development/hexmap-coordinates-the-easy-way)[20] formula results from writing `a.q + a.r - b.q - b.r` as `a.q - b.q + a.r - b.r`, and using “max” form instead of the “divide by two” form of `cube_distance`. They're all equivalent once you see the connection to cube coordinates.
    

    ### 
Offset coordinates[#](#distances-offset)

    

      As with axial coordinates, we'll [convert](#conversions) offset coordinates to axial/cube coordinates, then use axial/cube distance.
    

    

function offset_distance(a, b):
    var ac = offset_to_axial(a)
    var bc = offset_to_axial(b)
    return axial_distance(ac, bc)

    

      We'll use the same pattern for many of the algorithms: convert offset to axial/cube, run the axial/cube version of the algorithm, and convert any axial/cube results back to offset coordinates. There are also more direct formulas for distances; see [the rot.js manual](https://ondras.github.io/rot.js/manual/#hex/indexing)[21] for a formula in the "Odd shift" section.
    

    ### 
Doubled coordinates[#](#distances-doubled)

    

      Although converting doubled coordinates to axial/cube coordinates works, there's also a direct formula for distances, from the [rot.js manual](https://ondras.github.io/rot.js/manual/#hex/indexing)[22]:
    

    

function doublewidth_distance(a, b):
    var dcol = abs(a.col - b.col)
    var drow = abs(a.row - b.row)
    return drow + max(0, (dcol-drow)/2)

function doubleheight_distance(a, b):
    var dcol = abs(a.col - b.col)
    var drow = abs(a.row - b.row)
    return dcol + max(0, (drow−dcol)/2)
    
  

  
  

  

    ### 
Coordinate range[#](#range-coordinate)

    
    
      
        

          Given a hex `center` and a range N, which hexes are within N steps from it?
        
        
        

          We can work backwards from the [hex distance](#distances) formula, `distance = max(abs(q), abs(r), abs(s))`. To find all hexes within N steps, we need `max(abs(q), abs(r), abs(s)) ≤ N`. This means we need *all* three to be true: `abs(q) ≤ N` and `abs(r) ≤ N` and `abs(s) ≤ N`. Removing absolute value, we get -N ≤ q ≤ +N and -N ≤ r ≤ +N and -N ≤ s ≤ +N. In code it's a nested loop:
        
        

var results = []
for each -N ≤ q ≤ +N:
    for each -N ≤ r ≤ +N:
        for each -N ≤ s ≤ +N:
            if q + r + s == 0:
                results.append(cube_add(center, Cube(q, r, s)))
        

          This loop will work but it's somewhat inefficient. Of all the values of `s` we loop over, only one of them actually satisfies the `q + r + s = 0` constraint on cubes. Instead, let's directly calculate the value of `s` that satisfies the constraint:
        
        

var results = []
for each -N ≤ q ≤ +N:
    for each max(-N, -q-N) ≤ r ≤ min(+N, -q+N):
        var s = -q-r
        results.append(cube_add(center, Cube(q, r, s)))
        

          This loop iterates over exactly the needed coordinates. In the diagram, each range is a pair of lines. Each line is an inequality (a [half-plane](http://devmag.org.za/2013/08/31/geometry-with-hex-coordinates/)[28]). We pick all the hexes that satisfy all six inequalities. This loop also works nicely with axial coordinates:
        
        

var results = []
for each -N ≤ q ≤ +N:
    for each max(-N, -q-N) ≤ r ≤ min(+N, -q+N):
        results.append(axial_add(center, Hex(q, r)))

      

      

    

    ### 
Intersecting ranges[#](#range-intersection)

    
    
      
        

          If you need to find hexes that are in more than one range,
          you can intersect the ranges before generating a list of
          hexes.
        
        

          You can either think of this problem algebraically or
          geometrically. Algebraically, each hexagonally-shaped region is expressed as
          inequality constraints of the form `-N ≤ dq ≤ +N`,
          and we're going to solve for the intersection of those
          constraints.  Geometrically, each region is a cube in 3D
          space, and we're going to intersect two cubes in 3D space to
          form a [cuboid](https://en.wikipedia.org/wiki/Cuboid)[29] in 3D
          space, then project back to the q + r + s = 0 plane to get
          hexes. I'm going to solve it algebraically:
        
        

          First, we rewrite constraint `-N ≤ dq ≤ +N` into a
          more general form, `qmin ≤ q ≤
          qmax`, and set `qmin = center.q
          - N` and `qmax = center.q + N`. We'll
          do the same for `r` and `s`, and end
          up with this generalization of the code from the previous
          section:
        
        

var results = []
for each qmin ≤ q ≤ qmax:
    for each max(rmin, -q-smax) ≤ r ≤ min(rmax, -q-smin):
        results.append(Hex(q, r))
        

          The intersection of two ranges `a ≤ q ≤ b` and
          `c ≤ q ≤ d` is `max(a, c) ≤ q ≤ min(b,
          d)`. Since a hex region is expressed as ranges over q,
          r, s, we can separately intersect each of the q, r, s ranges
          then use the nested loop to generate a list of hexes in the
          intersection. For one hex region we set
          `qmin = H.q - N` and
          `qmax = H.q + N` and likewise for
          `r` and `s`. For intersecting two hex
          regions we set `qmin = max(H1.q -
          N, H2.q - N)` and `qmax =
          min(H1.q + N, H2.q + N)`, and likewise
          for `r` and `s`. The same pattern
          works for intersecting three or more regions, and can generalize to [other shapes](http://devmag.org.za/2013/08/31/geometry-with-hex-coordinates/)[30] (triangles, trapezoids, rhombuses, non-regular hexagons).
        
      

      
    
    
    
    ### 
Obstacles[#](#range-obstacles)

    
    
      
        

          If there are obstacles, the simplest thing to do is a distance-limited flood fill ([breadth first search](/pathfinding/tower-defense/)). In the code, `fringes[k]` is an array of all hexes that can be reached in `k` steps. Each time through the main loop, we expand level `k-1` into level `k`. This works equally well with any of the hex coordinate systems (cube, axial, offset, doubled).
        

        

function hex_reachable(start, movement):
    var visited = set() # set of hexes
    add start to visited
    var fringes = [] # array of arrays of hexes
    fringes.append([start])

    for each 1 ≤ k ≤ movement:
        fringes.append([])
        for each hex in fringes[k-1]:
            for each 0 ≤ dir &lt; 6:
                var neighbor = hex_neighbor(hex, dir)
                if neighbor not in visited and not blocked:
                    add neighbor to visited
                    fringes[k].append(neighbor)

    return visited
      

      

    
    
  
  

  

    

      
        

          Given a hex vector (difference between one hex and another), we
          might want to rotate it to point to a different hex. This is
          simple with cube coordinates if we stick with rotations of 1/6th
          of a circle.
        

        

          A rotation 60° right (clockwise ↻) shoves each coordinate one slot to the left ←:
        
    
        

      [ q,  r,  s]
to        [-r, -s, -q]
to           [  s,  q,  r]

        

          A rotation 60° left (counter-clockwise ↺) shoves each coordinate one slot to the right →:
        
    
        

          [ q,  r,  s]
to    [-s, -q, -r]
to [r,  s,  q]

      
      
      

      
        

          As you play with diagram, notice that each 60° rotation *flips* the signs and also physically “rotates” the coordinates. Take a look at the axis legend on the bottom left to see how this works. After a 120° rotation the signs are flipped back to where they were. A 180° rotation flips the signs but the coordinates have rotated back to where they originally were.
        
        
        

          Here's the full recipe for rotating a position `hex` around a center position `center` to result in a new position `rotated`:
        

        
          - 
[Convert](#conversions) positions `hex` and `center` to cube coordinates.

          - Calculate a *vector* by subtracting the center: `vec = cube_subtract(hex, center) = Cube(hex.q - center.q, hex.r - center.r, hex.s - center.s)`.

          - Rotate the vector `vec` as described above, and call the resulting vector `rotated_vec`.

          - Convert the vector back to a position by adding the center: `rotated = cube_add(rotated_vec, center) = Cube(rotated_vec.q + center.q, rotated_vec.r + center.r, rotated_vec.s + center.s)`.

          - 
[Convert](#conversions) the cube position `rotated` back to to your preferred coordinate system.

        

        

          It's several conversion steps but each step is short. You can shortcut some of these steps by defining rotation directly on axial coordinates, but hex vectors don't work for offset coordinates and I don't know a shortcut for offset coordinates. Also see [this stackexchange discussion](https://gamedev.stackexchange.com/questions/15237/how-do-i-rotate-a-structure-of-hexagonal-tiles-on-a-hexagonal-grid/)[31] for other ways to calculate rotation.
        

      
      
    
    
  

  

    

      
        

          Given a hex, we might want to reflect it across one of the axes. With cube coordinates, we *swap* the coordinates that *aren't* the axis we're reflecting over. The axis we're reflecting over stays the same.
        
      
      
      

      

function reflectQ(h) { return Cube(h.q, h.s, h.r); }
function reflectR(h) { return Cube(h.s, h.r, h.q); }
function reflectS(h) { return Cube(h.r, h.q, h.s); }
      
      

        To reach the other two reflections, *negate* the coordinates of the original and the first reflection. These are shown as white arrows in the diagram.
      

      

        To reflect over a line that's not at 0, pick a reference point on that line. Subtract the reference point, perform the reflection, then add the reference point back.
      
      
    
    
  

  

    
      
        ### 
Single ring[#](#rings-single)

        
        

          To find out whether a given hex is on a ring of a given `radius`, calculate the distance from that hex to the center and see if it's `radius`. To get a list of all such hexes, take `radius` steps away from the center, then follow the rotated vectors in a path around the ring.
        

        

function cube_scale(hex, factor):
    return Cube(hex.q * factor, hex.r * factor, hex.s * factor)

function cube_ring(center, radius):
    var results = []
    # this code doesn't work for radius == 0; can you see why?
    var hex = cube_add(center,
                        cube_scale(cube_direction(4), radius))
    for each 0 ≤ i &lt; 6:
        for each 0 ≤ j &lt; radius:
            results.append(hex)
            hex = cube_neighbor(hex, i)
    return results

        

          In this code, `hex` starts out on the ring, shown by the large arrow from the center to the corner in the diagram. I chose corner 4 to start with because it lines up the way my direction numbers work but you may need a different starting corner. At each step of the inner loop, `hex` moves one hex along the ring. After a circumference of `6 * radius` steps it ends up back where it started.
        
      
      
      

      

        The scale, add, and neighbor operations also work on axial and doubled coordinates, so the same algorithm can be used. For offset coordinates, convert to one of the other formats, generate the ring, and convert back.
      
      
    

    
      
        ### 
Spiral rings[#](#rings-spiral)

        
        

          Traversing the `N` rings one by one in a spiral pattern, we can fill in the interior:
        
    
        

function cube_spiral(center, radius):
    var results = list(center)
    for each 1 ≤ k ≤ radius:
        results = list_append(results, cube_ring(center, k))
    return results
      

      

      

        Spirals also give us a way to *count* how many hexagon tiles are in the larger hexagon.
        The center is 1 hex. The circumference of the k-th ring is `6 * k` hexes.
        The sum for N rings is `1 + 6 * sum(1 to N)`.
        Using [this formula](https://en.wikipedia.org/wiki/1_%2B_2_%2B_3_%2B_4_%2B_%E2%8B%AF)[32],
        that simplifies to `1 + 3 * N * (N+1)`.

        For  rings, there will be
        `{{count}}` hexes.
      

      

        Visiting the hexes this way can also be used to calculate [movement range](#range).
      
    

    

  

  

    

      
        

          Given a location and a distance, what is visible from that location, not blocked by obstacles? The simplest way to do this is to draw a line to every hex that's in range. If the line doesn't hit any walls, then you can see the hex. Mouse over a hex to see the line being drawn to that hex, and which walls it hits.
        

        

          This algorithm can be slow for large areas but it's so easy to implement that it's what I recommend starting with.
        
      
      
      

      
      
      

        There are many different ways to define what's "visible". Do you want to be able to see the center of the other hex from the center of the starting hex? Do you want to see any part of the other hex from the center of the starting point? Maybe any part of the other hex from any part of the starting point? Are there obstacles that occupy less than a complete hex? Field of view turns out to be trickier and more varied than it might seem at first. Start with the simplest algorithm, but expect that it may not compute exactly the answer you want for your project. There are even situations where the simple algorithm produces results that are illogical.
      
      
      

        [Clark Verbrugge's guide](http://www-cs-students.stanford.edu/~amitp/Articles/HexLOS.html)[36] describes a “start at center and move outwards” algorithm to calculate field of view. Also see [my article on 2D visibility calculation](/articles/visibility/) for an algorithm that works on polygons, including hexagons. For grids, the roguelike community has a nice set of algorithms for square grids (see [Roguelike Vision Algorithms](https://www.adammil.net/blog/v125_Roguelike_Vision_Algorithms.html)[37] and [Pre-Computed Visibility Tries](https://www.roguebasin.com/index.php/Pre-Computed_Visibility_Tries)[38] and [Field of Vision](https://www.roguebasin.com/index.php/Field_of_Vision)[39]); some of them might be adapted for hex grids.
      
      
    
    
  

  
  

    

      For hex to pixel, it's useful to review the [size and spacing diagram](#basics) at the top of the page where we defined the `horiz` and `vert` spacing between adjacent hexagons.
    
    
    ### 
Axial coordinates[#](#hex-to-pixel-axial)

    
      
    ### 
Offset coordinates[#](#hex-to-pixel-offset)

    

    ### 
Doubled coordinates[#](#hex-to-pixel-doubled)

    

      Doubled makes many algorithms simpler than offset.
    

    

function doublewidth_to_pixel(hex):
    // hex to cartesian
    var x = sqrt(3)/2 * hex.col
    var y =      3./2 * hex.row
    // scale cartesian coordinates
    x = x * size
    y = y * size
    return Point(x, y)

function doubleheight_to_pixel(hex):
    // hex to cartesian
    var x =      3./2 * hex.col
    var y = sqrt(3)/2 * hex.row
    // scale cartesian coordinates
    x = x * size
    y = y * size
    return Point(x, y)

    ### 
Mod: non-zero origin[#](#hex-to-pixel-mod-origin)

    

      Some projects have grids that are not centered at 0,0. We can adapt any of the hex-to-pixel functions above by *chaining* one additional operation to the end:
    

    

function *_to_pixel(hex):
    // hex to cartesian
    …
    // scale cartesian coordinates
    …
    **// translate cartesian coordinates**
    x = x + origin.x
    y = y + origin.y
    return Point(x, y)

    

      Later, [when converting pixel to hex](#pixel-to-hex-mod-origin), we'll undo this by subtracting the origin at the beginning.
    

    ### 
Mod: pixel sizes[#](#hex-to-pixel-mod-pixelsize)

    

      Some projects need hexagons to fit a specific size.
      We can use the formulas from the [Geometry](#basics) section of this page
      to change the scaling for any of the hex-to-pixel functions to *separately* multiply by x and y scales.
    

    

  

  

    

      One of the most common questions is, how do I take a pixel location (such as a mouse click) and convert it into a hex grid coordinate? I'll show how to do this for axial/cube coordinates. For offset and doubled coordinates, I first convert pixel to axial/cube, and then axial/cube to offset/doubled, but there are more direct algorithms also.
    

    ### 
Axial coordinates[#](#pixel-to-hex-axial)

    

    ### 
Offset coordinates[#](#pixel-to-hex-offset)

    

      If you use offset coordinates, you can convert to pixel to axial, then axial to offset. There are also more direct algorithms that I need to study; browse [this list](more-pixel-to-hex.html#more). In one project I used [a pixel map](more-pixel-to-hex.html#pixel-map), an precomputed array of pixels that stores the hex coordinate at each.
    

    ### 
Doubled coordinates[#](#pixel-to-hex-doubled)

    

      The [hex-to-pixel](#hex-to-pixel-doubled) algorithm for doubled coordinates is a straight multiply, so the pixel-to-hex will divide by those same amounts. After that, we need to round to the nearest hex. I haven't worked that out yet for doubled coordinates.
    

    ### 
Mod: non-zero origin[#](#pixel-to-hex-mod-origin)

    

      For hex-to-pixel, we implemented [a non-zero origin](#hex-to-pixel-mod-origin) by inserting an addition at the *end* of the chain. To invert this operation, we need to insert a subtraction at the *beginning* of the chain:
    

    

function *_to_hex(point):
    **// invert the addition**
    x = x - origin.x
    y = y - origin.y
    // invert the scaling
    …
    // cartesian to hex
    …

    

      This pattern is not limited to hexagons. Any chain of operations p → A → B → C → q can be inverted by inverting each individual operation and performing them in reverse order: q → C⁻¹ → B⁻¹ → A⁻¹ → p.
    

    ### 
Mod: pixel sizes[#](#pixel-to-hex-mod-pixelsize)

    

      For hex-to-pixel, we implemented [non-uniform scaling](#hex-to-pixel-mod-pixelsize) by changing the multiplying by `size` to multiplying by a different scale for x and y. To invert this operation, we need to divide by those scaling values:
    

    
    
  

  
  

    

      Sometimes we'll end up with a *floating-point* cube coordinate, and we'll want to know which hex it should be in. This comes up in [line drawing](#line-drawing) and [pixel to hex](#pixel-to-hex). Converting a floating point value to an integer value is called *rounding* so I call this algorithm `cube_round`.
    

    

      Just as with integer cube coordinates, `frac.q + frac.r + frac.s = 0` with fractional (floating point) cube coordinates. We can round each component to the nearest integer, `q = round(frac.q); r = round(frac.r); s = round(frac.s)`. However, after rounding we do *not* have a guarantee that `q + r + s = 0`. We do have a way to correct the problem: *reset* the component with the largest change back to what the constraint `q + r + s = 0` requires. For example, if the r-change `abs(r-frac.r)` is larger than `abs(q-frac.q)` and `abs(s-frac.s)`, then we reset `r = -q-s`. This guarantees that `q + r + s = 0`. Here's the algorithm:
    

    

function cube_round(frac):
    var q = round(frac.q)
    var r = round(frac.r)
    var s = round(frac.s)

    var q_diff = abs(q - frac.q)
    var r_diff = abs(r - frac.r)
    var s_diff = abs(s - frac.s)

    if q_diff &gt; r_diff and q_diff &gt; s_diff:
        q = -r-s
    else if r_diff &gt; s_diff:
        r = -q-s
    else:
        s = -q-r

    return Cube(q, r, s)

    

      For non-cube coordinates, the simplest thing to do is to [convert to cube coordinates](#conversions), use the rounding algorithm, then convert back:
    

    

function axial_round(hex):
    return cube_to_axial(cube_round(axial_to_cube(hex)))

    

      The same would work if you have `oddr`, `evenr`, `oddq`, or `evenq` instead of `axial`. Jacob Rus has a [direct implementation of axial_round](https://observablehq.com/@jrus/hexround)[42] without converting to cube first.
    
    
    

      Implementation note: `cube_round` and `axial_round` take *float* coordinates instead of *int* coordinates. If you've written a Cube and Hex class, they'll work fine in dynamically typed languages where you can pass in floats instead of ints, and they'll also work fine in statically typed languages with a unified number type. However, in most statically typed languages, you'll need a separate class/struct type for float coordinates, and `cube_round` will have type `FloatCube → Cube`. If you also need `axial_round`, it will be `FloatHex → Hex`, using helper function `floatcube_to_floathex` instead of `cube_to_hex`. In languages with parameterized types (C++, Haskell, etc.) you might define `Cube&lt;T&gt;` where `T` is either `int` or `float`. Alternatively, you could write `cube_round` to take three floats as inputs instead of defining a new type just for this function.
    

    

      This algorithm is based on [Charles
      Fu's article from 1994](http://www-cs-students.stanford.edu/~amitp/Articles/Hexagon2.html)[43]. His code contains the additional optimization
      that if `rx + ry + rz = 0` there's no need to
      look at the error values and reset the largest component.
    

    

      Patrick Surry has a [visualization showing why the rounding algorithm works](https://blocks.roadtolarissa.com/patricksurry/0603b407fa0a0071b59366219c67abca)[44]. Martin R. Han has a [different visualization showing why the rounding algorithm works](https://www.desmos.com/3d/86szmiocif)[45].
    
    
  

  

    

      One of the common complaints about the axial coordinate system is that it leads to wasted space when using a rectangular map; that's one reason to favor an offset coordinate system. However all the hex coordinate systems lead to wasted space when using a triangular or hexagonal map. We can use the same strategies for storing all of them.
    
    
    

    

      Notice in the diagram that the wasted space is on the left and
      right sides of each row (except for rhombus maps) This gives us
      three strategies for storing the map:
    

    
      - Use a **2D Array**. Use nulls or some other sentinel at the unused spaces. Store `Hex(q, r)` at          `array[r][q]`. At most
        there's a factor of two for these common shapes; it may not be
        worth using a more complicated solution.

      
      - Use a **hash table** instead of dense
        array. This allows arbitrarily shaped maps, including ones with
        holes. Store `Hex(q, r)` in
        `hash_table(hash(q,r))`.

      - Use an **array of arrays** by sliding row to the left, and shrinking the rows to the minimum size.
        For pointy-top hexes, store `Hex(q, r)` in `array[r - first_row][q - first_column(r)]`. Some examples for the map shapes above:

        

          
            **Rectangle**. Store `Hex(q, r)` at `array[r][q + floor(r/2)]`. Each row has the same length. This is equivalent to odd-r offset.
          

          
          - 
            **Hexagon**. Store `Hex(q, r)` at `array[r][q - max(0, N-r)]`. Row r size is `2*N+1 - abs(N-r)`.
          

          - 
            **Rhombus**. Conveniently, `first_row` and `first_column(r)` are both 0. Store `Hex(q, r)` at `array[r][q]`. All rows are the same length.
          

          
          - 
            **Down-triangle**. Store `Hex(q, r)` at `array[r][q]`. Row r has size `N+1-r`.
          

          - 
            **Up-triangle**. Store `Hex(q, r)` at `array[r][q - N+1+r]`. Row r has size `1+r`.
          

        
        For flat-top hexes, swap the roles of the rows and columns, and use `array[q - first_column][r - first_row(q)]`.
      
    

    

      Encapsulate access into the getter/setter in a map class so that the
      rest of the game doesn't need to know about the map storage. Your
      maps may not look exactly like these, so you will have to adapt one
      of these approaches.
    

  

  

    
      

        

          Sometimes you may want the map to “wrap” around the edges. In a
          square map, you can either wrap around the x-axis only (roughly
          corresponding to a sphere) or both x- and y-axes (roughly
          corresponding to a torus). Wraparound depends on the map shape,
          not the tile shape. To wrap around a rectangular map is easy
          with offset coordinates. I'll show how to wrap around a
          hexagon-shaped map with cube coordinates.
        

        

          Corresponding to the center of the map, there are six
          “mirror” centers. When you go off the map, you subtract the
          mirror center closest to you until you are back on the main
          map. In the diagram, try exiting the center map, and watch
          one of the mirrors enter the map on the opposite side.
        

        

          The simplest implementation is to precompute the
          answers. Make a lookup table storing, for each hex just off
          the map, the corresponding cube on the other side. For each
          of the six mirror centers `M`, and each of the
          locations on the map `L`, store
          `mirror_table[cube_add(M, L)] = L`. Then any time you
          calculate a hex that's in the mirror table, replace it by
          the unmirrored version. See [stackoverflow](https://gamedev.stackexchange.com/a/137603/2472)[46] for another approach.
        

        

          For a hexagonal shaped map with radius `N`, the
          mirror centers will be `Cube(2*N+1, -N, -N-1)` and
          its [six rotations](#rotation).
        
        
      
      
      

      

        Related: Sander Evers has a [nice explanation of how to combine small hexagons into a grid of large hexagons](https://observablehq.com/@sanderevers/hexagon-tiling-of-an-hexagonal-grid)[47] and also a [coordinate system to represent small hexagons within a larger one](https://observablehq.com/@sanderevers/hexmod-representation)[48].
      
      
    
    
  

  

    
      
    

      If you're using graph-based pathfinding such as A* or Dijkstra's algorithm or Floyd-Warshall, pathfinding on hex grids isn't different from pathfinding on square grids. The explanations and code from [my pathfinding tutorial](https://www.redblobgames.com/pathfinding/a-star/introduction.html)[49] will work equally well on hexagonal grids.
    

    

    

      Mouse overTouch a hex in the diagram to see the path to it. Click or drag to toggle walls.
    
    
    
      - 
**Neighbors**. The sample code I provide in the pathfinding tutorial calls `graph.neighbors` to get the neighbors of a location. Use the function in the [neighbors](#neighbors) section for this. Filter out the neighbors that are impassable.

      - 
**Heuristic**. The sample code for A* uses a `heuristic` function that gives a distance between two locations. Use the [distance formula](#distances), scaled to match the movement costs. For example if your movement cost is 5 per hex, then multiply the distance by 5.

    

    
    
  
  
      
  

    

      I have an [**guide to implementing your own hex grid library**](implementation.html), including sample code in C++, Python, C#, Haxe, Java, Javascript, Typescript, Lua, and Rust. I also link to existing libraries for C# (including Unity), Java, Objective C, Swift, Python, Ruby, and other languages.
    
    
    
      - 
        The best early guide I saw to the axial coordinate system was [Clark Verbrugge's
        guide](http://www-cs-students.stanford.edu/~amitp/Articles/HexLOS.html)[50], written in 1996.
      

      - 
        The first time I saw the cube coordinate system was from [Charles
        Fu's posting to rec.games.programmer](http://www-cs-students.stanford.edu/~amitp/Articles/Hexagon2.html)[51] in 1994.
      

      
      - 
[DevMag
        has a nice visual overview of hex math](http://devmag.org.za/2013/08/31/geometry-with-hex-coordinates/)[52] including how to
        represent areas such as half-planes, triangles, and
        quadrangles. There's a [PDF article](https://www.gamelogic.co.za/downloads/HexMath2.pdf)[53] that goes into more detail. **Highly recommended**!  The [GameLogic Grids](https://gamelogic.co.za/grids/documentation-contents/quick-start-tutorial/gamelogics-hex-grids-for-unity-and-amit-patels-guide-for-hex-grids/)[54] library implements these and many other grid types in Unity.

      
      - 
        In my [Guide
        to Grids](/grids/parts/), I cover axial coordinate systems to address
        square, triangle, and hexagon sides and corners, and algorithms for the relationships
        among tiles, sides, and corners. I also show how square and hex grids are related.
      

      
      - 
[James
      McNeill has a nice visual explanation of grid
      transformations](https://playtechs.blogspot.com/2007/04/hex-grids.html)[55].

      - 
[Overview
        of hex coordinate types](https://web.archive.org/web/20090205120106/http://sc.tri-bit.com/Hex_Grids)[56]: staggered (offset), interlaced, 3D (cube), and trapezoidal (axial).

      - Hexnet explains how the [correspondence between hexagons and cubes](https://hexnet.org/content/permutohedron)[57] goes much deeper than what I described on this page, generalizing to higher dimensions.

      - 
[The
      Rot.js library](https://ondras.github.io/rot.js/manual/#hex/indexing)[58] has a list of hex coordinate systems:
      non-orthogonal (axial), odd shift (offset), double width
      (interlaced), cube.

      
      - 
[Range
      for cube coordinates](https://stackoverflow.com/questions/2049196/generating-triangular-hexagonal-coordinates-xyz)[59]: given a distance, which hexagons are
      that distance from the given one?

      
      - 
[Distances
        on hex grids](https://archive.ph/20141214082648/http://keekerdc.com/2011/03/hexagon-grids-coordinate-systems-and-distance-calculations/)[60] using cube coordinates, and reasons to use cube coordinates instead of offset.

      
      - 
[This
        guide](https://web.archive.org/web/20130608235236/https://www.br-gs.com/tutorial/hexagon-grid.html)[61] explains the basics of measuring and drawing hexagons,
        using an offset grid.

      - 
[Convert
      cube hex coordinates to pixel coordinates](https://stackoverflow.com/questions/2459402/hexagonal-grid-coordinates-to-pixel-coordinates)[62].

      - 
[This
      thread](https://gamedev.stackexchange.com/questions/51264/get-ring-of-tiles-in-hexagon-grid)[63] explains how to generate rings.

      - Are there [pros
      and cons of “pointy top” and “flat top” hexagons](https://gamedev.stackexchange.com/questions/49718/vertical-vs-horizontal-hex-grids-pros-and-cons)[64]?

      - 
[Line
      of sight in a hex grid](https://web.archive.org/web/20121113035227/http://arges-systems.com/blog/2011/01/10/hex-grid-line-of-sight-revisited/)[65] with offset coordinates, splitting
      hexes into triangles

      - I printed out the PDF hex grids from [this page](https://incompetech.com/graphpaper/hexagonal/)[66] while working out some of the algorithms.

      - 
[Hexagonal Image Processing](https://link.springer.com/book/10.1007/1-84628-203-9)[67] ([DOI](https://doi.org/10.1007/1-84628-203-9)[68]) is an entire book that uses a hierarchical hexagonal coordinate system.

      
      - 
        This is the oldest reference I can find for axial grids: Luczak, E. and Rosenfeld, A., *Distance on a Hexagonal Grid*. IEEE Transactions on Computers (1976) ([DOI](https://doi.org/10.1109/TC.1976.1674642)[69]) It calls the axial system *oblique coordinates* and the offset systems *pseudohexagonal grids*.
      

      - 
        Snyder, Qi, Sander's paper *Coordinate system for hexagonal pixels* ([DOI](https://doi.org/10.1117/12.348629)[70]) describes gradients, diffusion, and map storage for axial coordinates. Mersereau's paper *The processing of hexagonally sampled two-dimensional signals* ([DOI](https://doi.org/10.1109/PROC.1979.11356)[71]) describes signal processing on axial coordinates.
      

      - 
        There's a paper that calls cube coordinates **R3 coordinates*: Her, Innchyn, *Geometric Transformations on the Hexagonal Grid*, IEEE Transactions on Image Processing (1995) ([DOI](https://doi.org/10.1109/83.413166)[72]) It covers coordinates, correspondence to cube coordinates, rounding, reflections, scaling, shearing, and rotation. A paper from the same author ([DOI](https://doi.org/10.1115/1.2919210)[73]) covers distances.
      

      
      - 
        The [Reddit discussion](https://old.reddit.com/r/gamedev/comments/1dz1tr/)[74] and [Hacker News discussion](https://news.ycombinator.com/item?id=5809724)[75] and [MetaFilter discussion](https://www.metafilter.com/128649/Hexagonal-Grids)[76] have more comments and links.
      

      
    

    

      The code that powers this page is partially procedurally generated! The core algorithms are in [lib.js](/grids/hexagons/codegen/output/lib.js),  generated from [my guide to implementation](implementation.html). There are a few more algorithms in [hex-algorithms.js](hex-algorithms.js). The interactive diagrams are in [diagrams.js](diagrams.js) and [index.js](index.js), using Vue.js to inject into the templates in [index.bxml](index.bxml) (xhtml I feed into a preprocessor).
    
    
    

      There are more things I want to do for this guide. I'm [keeping a list on Notion](https://redblobgames.notion.site/Hexagonal-Grids-7d2d4d624bc5483dafbe615d75ab3902)[77]. Do you have suggestions for things to change or add? Comment below.