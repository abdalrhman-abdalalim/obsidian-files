- CSS transitions allows you to change property values smoothly, over a given duration.

### Properties
-  `transition`
- `transition-delay` 
- `transition-duration`
- `transition-property`
- `transition-timing-function`

### How to use CSS Transition ?
- To create a transition effect, you must specify two things:
	- the CSS property you want to add an effect to
	- the duration of the effect
- ==Note== -> If the duration part is not specified, the transition will have no effect, because the default value is 0.

###  Change Several Property Values

```css
div {  transition: width 2s, height 4s;}
```

### Specify the Speed Curve of the Transition
- he `transition-timing-function` property specifies the speed curve of the transition effect.
- Can have following values : 
	- - `ease` - specifies a transition effect with a slow start, then fast, then end slowly (this is default)
	- - `linear` - specifies a transition effect with the same speed from start to end
	- - `ease-in` - specifies a transition effect with a slow start
	- - `ease-out` - specifies a transition effect with a slow end
	- - `ease-in-out` - specifies a transition effect with a slow start and end
	- - `cubic-bezier(n,n,n,n)` - lets you define your own values in a cubic-bezier function