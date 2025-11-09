## Description

The requestAnimationFrame() method tells the browser that you wish to perform an animation and requests that the browser call a specified function to update an animation before the next repaint.

**Note:** Your callback routine must itself call requestAnimationFrame() if you want to animate another frame at the next repaint.

**Tip:** You should call this method whenever you are ready to update your animation onscreen because:

- The browser can optimize it, so animations will be smoother
- Animations in inactive tabs will stop, allowing the CPU to chill
- More battery-friendly



### Example

Use of the requestAnimationFrame() method:
```js
const div = document.getElementById('mydiv');  
let leftpos = 0;  
  
function movediv(timestamp){  
  leftpos += 5;  
  adiv.style.left = leftpos + 'px';  
  requestAnimationFrame(movediv);  
}  
  
requestAnimationFrame(movediv);

```