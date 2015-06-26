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
