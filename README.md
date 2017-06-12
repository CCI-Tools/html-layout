## Browser Layout Process

The layout process performed by browsers usually has the following pattern:

1. Parent element renderer determines its own width.
2. Parent element goes over children and:
   1. Place the child element renderer (sets its x and y).
   2. Calls child layout if needed(they are dirty or we are in a global layout or some other reason) - 
      this calculates the child's height.
   3. Parent uses children accumulative heights and the heights of the margins and paddings to set it own height - 
      this will be used by the parent renderer's parent.
3. Sets its dirty bit to false.

The renderer's width is calculated using the container block's width , the renderer's style "width" property, the margins and borders. 
For example the width of the following div:

    <div style="width:30%"/>
    
Would be calculated by Webkit as following (class RenderBox method calcWidth):

1. The container width is the maximum of the containers availableWidth and 0. 
   The availableWidth in this case is the contentWidth which is calculated as:

       clientWidth() - paddingLeft() - paddingRight()
       
   `clientWidth` and `clientHeight` represent the interior of an object excluding border and scrollbar.
2. The elements width is the "width" style attribute. 
   It will be calculated as an absolute value by computing the percentage of the container width.
3. The horizontal borders and paddings are now added.

So far this was the calculation of the *preferred width*. 
Now the minimum and maximum widths will be calculated. 

4. If the preferred width is higher than the maximum width, then maximum width is used. 
5. If it is lower than the minimum width (the smallest unbreakable unit), then the minimum width is used.

## Examples - Holy Grail Layout

* [with calc()]()
* [with flex]()

## HTML/CSS Must-Reads

* [How browsers work - Layout](http://taligarsiel.com/Projects/howbrowserswork1.htm#Layout)
* [MDN: Cascade and Inheritance](https://developer.mozilla.org/en-US/docs/Learn/CSS/Introduction_to_CSS/Cascade_and_inheritance)
* [MDN: CSS Box Model](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model)
* [MDN: Determining the Dimensions of Elements](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Object_Model/Determining_the_dimensions_of_elements)
* [CSS Default Values Reference](https://www.w3schools.com/cssref/css_default_values.asp)

## Important CSS Layout Attributes

* [display](https://developer.mozilla.org/en-US/docs/Web/CSS/display?v=example)
* [overflow](https://developer.mozilla.org/en/docs/Web/CSS/overflow?v=example)
* [position](https://developer.mozilla.org/en-US/docs/Web/CSS/position?v=example)
* [width](https://developer.mozilla.org/en-US/docs/Web/CSS/width?v=example)
* [height](https://developer.mozilla.org/en-US/docs/Web/CSS/height?v=example)
* [box-sizing](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing?v=example)


