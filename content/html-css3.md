---
title: Html Css3
image: /images/css3.png
imageMeta:
  attribution:
  attributionLink:
featured: true
author: carlos
date: Tue Jul 17 2018 16:49:29 GMT+0100 (IST)
tags:
  - programming
  - html
  - css3
---
Notes taken from [HTML5 and CSS3 Transition, Transformation, and Animation](https://www.goodreads.com/book/show/19457332-html5-and-css3-transition-transformation-and-animation)
### Flexbox
`display` property can be set to `flex` or `inline-flex`  
`flex`: The flex container functions at the block level  
`inline-flex`: considered inline withing the defined boundaries  

##### Flex Container  
`flex-direction`:  
 * `flex-direction: row-reverse;` - swaps direction to right-left
 * `flex-direction: column;` - swaps direction to top-bottom
 * `flex-direction: column-reverse;` - swaps direction to bottom-top  


`justify-content`:  (align items along rows)
 * `justify-content: center;` - position flex itmes at center along main axis  
 * `justify-content: flex-start;` - position flex items at start (left)    
 * `justify-content: flex-end;` - position flex items at end (right)  
 * `justify-content: space-between;` - equal space between items  
 * `justify-content: space-around;` - equal space around items  


`align-items`:  (align items along columns)
 * `align-items: center;` - position flex itmes at center along cross axis  
 * `align-items: flex-start;` - position flex items at start (top)    
 * `align-items: flex-end;` - position flex items at end (bottom)  
 * `align-items: baseline;` - align items along baseline
 * `align-items: stretch;` - stretch items from top to bottom 


`flex-wrap`:  
 * `wrap`:  
   > At times, there are too many Flex Items and they will not fit in on a single Flex Line. Here the wrap feature comes into play. Using this property, additional Flex Lines are created on the Cross axis to accommodate these Flex Items
 * `wrap-reverse`:
   > wraps from bottom to top  

##### Flex Items  
`order`: 
 * This feature displays the items in a particular hierarchy determined by the order
value assigned to them


`flex`: 
 * This feature displays the items in a particular ratio determined by the ratio
value assigned to them


## HTML5 
#### forms
**Attributes**  
 - `placeholder`
 - `autofocus`  
 - `required`  
 - `datalist`  

**Input Types**  

 - `search`
 - `email`  
 - `url`  
 - `date`  
 - `week`    
 - `month`    
 - `color` 

#### Advanced Features

 - `audio`  
 - `video`  
 - `drag-and-drop`:
     * `drag`: - `dragstart`, `drag`, `dragend`   
     * `drop`: - `dragenter1`, `dragover`, `dragleave`, `drop`
 - `geolocation`  
 - `sessionStorage`:  
     * property is used to store data for any specific session  
     * data stored in key value pairs  
 - `localStorage`  
     * data can be stored with no time limit  
 - `offline web applications`  
 - `canvas`  
     * defined with `<canvas id="demo" width="" height=""></canvas>`  
     * Need to get a reference to the element: `let canvas = document.getElementById('demo');`    
     * Get a reference to the 2d context in the canvas element: `let ctxt = canvas.getContext('2d');`   
     * the only primative shape supported by canvas is the rectangle  
     * For other shapes we need to use `path`  
     * `beginPath()` - list of items that form a shape is reset and we can draw new ones  
     * `closePath()` - close the shape.  
     * `moveTo(x, y)` - move to point x, y  
     * `stroke` and `fill` - stroke draws outline, fill fills  
     * `arc(x, y, radius, startAngle, endAngle, anticlockwise)`:  
         * `x` and `y` are axis  
         * `radius` is radius of arc  
         * `startAngle` and `endAngle` define the angle, start, and end  
         * `anticlockwise` definies the direction of drawing the arc  
     * `lineTo(x, y)` - draw a line from starting point of wherever virtual pointer is to the passed params.  
     * `createLinearGradient(x1, y1, x2, y2)` - Gradient starts at x1, y1 and goes to x2, y2.  
     * `addColorStop(0, navy);` - first param is to be defined from 0 to 1 to indicate the extent to which the gradient color has to be applied. The second param is the color to be used.   
     * `save()` - saves the state of the canvas on the stack  
     * `restore()` - returns the last saved state from the stack  
 - `transformations`:  
     * `translate()` - move a drawn shape in some way. called before the shape and its dimensions are defined.   
     * `rotate()` - rotate a shape. Call before shape is defined.  
     * `scale()` - scale a shape. called beforehand  
 - `Animation`


#### CSS3 Animations.
  
##### Transitions
     
 - `transition`:  
     - `transition-property: background; transition-duration: 3s; transition-timing-function: linear;` 
     - the above sets the transition featires when the transition is executed.  The property to transition is the background. The duration of the transition is set and the kind of transition is set. If you then trigger this with a `hover` etc, then the transition will fire.  
     - `transition-property` includes:
         - `background-color`   
         - `border-spacing`  
         - `font-size`  
         - `border-radius`  
         - `color`   
         - `margin`  
         - `max-width`   
         - `max-height`  
         - `right`  
         - `top`  
         - `vertical-align`  
         - `padding`  
      - `transition-duration` - we can enter multilpe values if there are multiple changes  
      - `transition-timing-function` - define the speed of the transitions: `linear`, `ease-in`, etc   
      - `transition-delay` - used to postpone the transition  
 - It can all be combined like this:  
 - `transition: background 3s linear, border-radius 2s ease-in 1s;`  
 - The transition-property , transition-duration , transition-timing-function, and lastly, transition-delay properties are defined at once in the order respectively


##### Transforms

 - `rotate`:    
     - rotate any element clockwise or anti-clockwise   
     - `transform: rotate(45deg);`  
 - `scale`  
     - increase/decrease the size of the element. 
     - `transform: scale(2);` - apparent size twice the real size  
     - `transform: scaleX(value);` - change width on apparent x axis    
     - `transform: scaleY(value);` - change height along y axis  
     - `transform: scale(value1, value2);` - change width and height   
 - `translate`  
     - can change the apparent position of the element along the x and y axis. Whenever we draw an element, the default co-ords along the x and y axis are `(0,0)`. To change the co-ords we use `translate`
     - `transform: translateX(value);` - change initial value on x to the passed value    
     - `transform: translateY(value);` - change the initial position on y to passed value  
     - `transform: translate(x-axis value, y-axis value);` - change both  
     - values passed to translate can be defined as percentages or in pixels.  
 - `skew`  
     - can change the angle of the element along the x and y axis  
     - `transform: skewX(value);` - change on x-axis  
     - `transform: skewY(value);` - change on y-axis  
     - `transform: skew(xdeg, ydeg);` - change on both axis  
 - `perspective`  
     - `transform: perspective(value in pixels);`  
     - The value in pixels determins the proximity of the perspective. A higher value will make the element appear distant, whereas a low value will make it appear closer. Theres is a third axis in transforms; the `z-axis`.  

> we have to use a single `transform: property` and assign various properties to it on the same line. We cannot define multiple transform values, as the latest value will override the previous values.
> There is a 2D `translate` and a 3D `translate`.  

##### 3D  
Translate property in 3D is different from 2D because it also uses the `z axis`.  
`transform: translateZ(value);`  
This value decides the position of the element on the z axis. A positive value will bring the element closer to the z-axis while a negative value will push the element away from the z-axis.  
There is a limitation to the 3D transforms. The scale property can be used, but
since we define a perspective in it, it is not used widely. The skew property also
exists but it is applicable only to the x axis and y axis. The skew property cannot be
implemented on the z axis. We will now look at the preserve-3d feature.  
`rotate(3D)`:
    ```    
    transform: rotateX(value);    
    transform: rotateY(value);    
    transform: rotateZ(value);     
    ```  
      
---

`preserve-3d`:  
we use this so that parent transformations dont affect their children.  
`.parent class {transform-style: preserve-3d;}`  


### Animations
`@keyframes`  
The points at which the transition should take place can be defined using the `@keyframes` property. We can use percentage of `from` and `to` keywords to implement the change in state from one CSS style to another.  
  
`animation-name`  
The `animation-name` property enables us to apply an animation to an element.  
  
`animation-duration`  
Define the duration of the animation.  

`animation-delay`  
Delay the animation by the time passed.  

`animation-timing-function`  
Defines the speed of the transition. Behaves the same way as transition timing function  

`animation-iteration-count`    
Define number of iterations the animation will do. Setting to infinite mean that the animation will never stop.  
  
`animation-direction`  
Define the direction of the animation. Examples include `reverse`, `alternate`  

`animation-play-state`  
Define whether animation is running or paused accordingly.  

