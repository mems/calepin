See [Constraint solver](Algorithm#Constraint solver)

Shapes: rect, circle, other (points)

- Input (one or many)
	* size (width, height)
	* margin (could be collapse, see CSS margin collapsing)
	* padding/border
	* allow rotation
	* order
- Output (multiple targets, like colomns for text)
	* shape(s) (rect, circle, points) (growing-binpacking vs binpacking)
	* size(s) w/h
	* orientation: left, right, center, justified, top, bottom, center (vertical), etc.
	* quality (like number of iteration) (100% = optimal = brut force, below?)
	* number of dimensions (2 and 3D, where 3D require 3D shapes and 2D requires 2D or 3D shapes)
	* Heuristics (for MaxRects)
		- Best: Tests all available placements and uses the result with the least used space
		- ShortSideFit: Short Side Fit
		- LongSideFit: Long Side Fit
		- AreaFit: Area Fit
		- BottomLeft: Bottom Left
		- ContactPoint: Contact Point

Use outlines to define available areas


VLSI floorplanning, Packing Lightmaps

- [Packing Lightmaps](http://blackpawn.com/texts/lightmaps/default.html)