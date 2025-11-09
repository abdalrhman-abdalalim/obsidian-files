- The CSS `@keyframes` rule is used to control the steps in an animation sequence by defining CSS styles for points along the animation sequence.
- Specify when the style change will happen in percent, or with the keywords "from" and "to", which is the same as 0% and 100%. 0% is the beginning of the animation, 100% is when the animation is complete.


### CSS Syntax
- @keyframes _name_ {  _keyframes-selector_ {_css-styles;}  
  keyframes-selector {css-styles;}  
  ...  
_}

### Animation property 
- `@keyframes`
- `animation-name`
- `animation-duration`
- `animation-play-state`
	- show animation status 
	- take 2 values (running , pause)
- `animation-delay`
	- specifies a delay for the start of an animation.
- `animation-iteration-count`
	- Specifies the number of times an animation should be played
	- could take infinite
- `animation-direction`
	- The `animation-direction` property specifies whether an animation should be played forwards, backwards or in alternate cycles.
	- The animation-direction property can have the following values:
		- `normal` - The animation is played as normal (forwards). This is default
		- `reverse` - The animation is played in reverse direction (backwards)
		- `alternate` - The animation is played forwards first, then backwards
		- `alternate-reverse` - The animation is played backwards first, then forwards
- `animation-timing-function`
	-  specifies the speed curve of the animation
	- he animation-timing-function property can have the following values:
		- `ease` - Specifies an animation with a slow start, then fast, then end slowly (this is default)
		- `linear` - Specifies an animation with the same speed from start to end
		- `ease-in` - Specifies an animation with a slow start
		- `ease-out` - Specifies an animation with a slow end
		- `ease-in-out` - Specifies an animation with a slow start and end
		- `cubic-bezier(n,n,n,n)` - Lets you define your own values in a cubic-bezier function
- `animation-fill-mode`
	- CSS animations do not affect an element before the first keyframe is played or after the last keyframe is played. The animation-fill-mode property can override this behavior.
	- The `animation-fill-mode` property specifies a style for the target element when the animation is not playing (before it starts, after it ends, or both).
	- The animation-fill-mode property can have the following values:
		- `none` - Default value. Animation will not apply any styles to the element before or after it is executing
		- `forwards` - The element will retain the style values that is set by the last keyframe (depends on animation-direction and animation-iteration-count)
		- `backwards` - The element will get the style values that is set by the first keyframe (depends on animation-direction), and retain this during the animation-delay period
		- `both` - The animation will follow the rules for both forwards and backwards, extending the animation properties in both directions
- `animation`
	- short hand of all properties div {  animation: example 5s linear 2s infinite alternate;}

###  The @keyframes Rule

When you specify CSS styles inside the `@keyframes` rule, the animation will gradually change from the current style to the new style at certain times.

To get an animation to work, you must bind the animation to an element.

### Example 
``` css
@keyframes mymove {  0%   {top: 0px;}  
  25%  {top: 200px;}  
  50%  {top: 100px;}  
  75%  {top: 200px;}  
  100% {top: 0px;}}
```