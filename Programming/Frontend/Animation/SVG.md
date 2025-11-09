### what is svg ?
- It is scalable vector graphics
- Defines graphics in XML format
- each element and attribute in SVG files can be animated

### SVG formatting :
- svg is a container of SVG graphics
``` html
<svg>

        <symbol id="text">

            <text text-anchor="middle" x="50%" y="50%">SVG Text</text>

        </symbol>

        <use xlink:href="#text"></use>

    </svg>
```
### SVG elements 
- Circle
- Ellipse
- Line
- Path
- Polygon
- Polyline
- Rectangle
- Text
- TextPath
- Tref
- Tspan

### some SVG styles 
- #### stroke-dasharray
	- presentation attribute defining the pattern of dashes and gaps used to paint the outline of the shape.
	- stroke-dasharray: 100, 500 -> `100` is the length of a visible dash, and `500` is the length of the gap that follows it.
- ##### stroke-width
	- attribute is a presentation attribute defining the width of the stroke to be applied to the shape
- ##### stroke-linejoin
	-  attribute defining the shape to be used at the corners of paths when they are stroked
- ##### stroke-dashoffset
	-  presentation attribute defining an offset on the rendering of the associated dash array
	- This shifts the starting point of the dash pattern along the stroke path by N units.
``` css
svg{

    position: absolute;

    top: 50%;

    transform: translateY(-50%);

    width: 100%;

    height: 350px;

}

svg text{

    fill: rgba(0, 0, 0,.1);

    font-size: 200px;

    stroke-width: 1px;

    stroke: white;

    stroke-linejoin: round;

    stroke-dasharray: 100;

    animation: animate-svg 1s linear infinite;

}

@keyframes animate-svg {

    100%{

        stroke-dashoffset: 160;

    }

}
```