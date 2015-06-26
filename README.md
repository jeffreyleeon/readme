## DrawFish

### Drawing Type

 - There are two drawing types: BitDrawType and SmoothDrawType

  - BitDrawType uses CGContext method to draw pixelized points.

    In this project, drawing logic is in BitDrawImageView class.

    Respective IBOutlet is tempDrawImage.

  - SmoothDrawType uses UIBezierPath class to draw smooth lines.
 
    In this project, drawing logic is in LinearInterpView class.

    Respective IBOutlet is drawingView.

### Views Hierarchy
![alt tag](http://oi57.tinypic.com/30vlwyf.jpg)

 - Base View
  - Fish_demo.png
    - A fish image that the player sees
  - tempDrawImage
    - A UIImageView with class BitDrawImageView
  - Displaying View and Linear Interp View
    - Linear Interp View
      - A UIView with class LinearInterpView to capture ONE CYCLE of drawing line
      
        ONE CYCLE starts with touchesBegan, ends with touchesEnded

        After the cycle and screen capture, the new line doesn't exists in Linear Interp View. It exists in Displaying View
    - Displaying View
      - When Linear Interp View finishes its cycle, Linear Interp View will call the following delegate function
      ```
      @protocol LinearInterpViewDelegate

      - (void) setImageViewForDisplay;

      @end
      ```
      - Base View will run the delegate function to capture current drawings
      
        And then set the screen capture to Displaying View for 'remembering' previous drawn lines
        
 #### Views Precautions
 
  - All the above views must have same width and height
  - Base View must have Linear Interp View's delegate function
  - Base View's background color must not be [UIColor clearColor]
  - If it is now BitDrawType, Displaying View and Linear Interp View will be hidden
  - If it is now SmoothDrawType, tempDrawImage will be hidden
 
### Drawing Determination

- ValidPointsController is used to determine whether or not allowing user to draw on a particular point
```
+ (int) getBitmapValFromColumn: (int) col andRow: (int) row;

Example:
[ValidPointsController getBitmapValFromColumn: sectionPoint.x andRow: sectionPoint.y];
```
- The sectionPoint must be mapped to scale up to the dimension of the BITMAP, as Fish_demo.png may not be displaying as the same width and height of the BITMAP
