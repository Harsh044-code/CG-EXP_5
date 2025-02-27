# Computer Graphics Experiment 5: Triangle Rotation

## Experiment Overview

This experiment demonstrates how to implement two types of triangle rotations:
1. Clockwise rotation (5a)
2. Anticlockwise rotation (5b)

Both rotations are performed around the triangle's centroid.

## Core Concept: 2D Rotation

The fundamental concept here is 2D rotation transformation. When rotating a point (x,y) around a pivot point (xc,yc) by angle θ:

1. For clockwise rotation:
   ```
   x' = xc + (x-xc)·cos(θ) - (y-yc)·sin(θ)
   y' = yc + (x-xc)·sin(θ) + (y-yc)·cos(θ)
   ```

2. For anticlockwise rotation:
   ```
   x' = xc + (x-xc)·cos(θ) - (y-yc)·sin(θ)
   y' = yc + (x-xc)·sin(θ) + (y-yc)·cos(θ)
   ```

The difference between clockwise and anticlockwise rotation is achieved by negating the angle value.

## Algorithm Explanation

Both algorithms follow similar steps:

1. **Initialize graphics mode** using the graphics.h library
2. **Input triangle coordinates** for the three vertices
3. **Draw the original triangle** in white color
4. **Calculate the centroid** using the formula: (x1+x2+x3)/3, (y1+y2+y3)/3
5. **Get rotation angle** from user and convert to radians
6. **Apply rotation formula** to each vertex
7. **Draw the rotated triangle** in a different color
8. **Wait for user input and close** the graphics mode

## Executable C++ Code

```cpp
#include <iostream>
#include <conio.h>
#include <graphics.h>
#include <math.h>
using namespace std;

void rotateTriangleClockwise() {
    int gd = DETECT, gm;
    initgraph(&gd, &gm, "C:\\Turboc3\\BGI"); // Use the correct BGI path
    
    int x1, y1, x2, y2, x3, y3;
    cout << "Enter (x1, y1), (x2, y2), (x3, y3) for the triangle: ";
    cin >> x1 >> y1 >> x2 >> y2 >> x3 >> y3;
    
    int tri[] = {x1, y1, x2, y2, x3, y3, x1, y1};
    setcolor(WHITE);
    drawpoly(4, tri);
    
    int xc = (x1 + x2 + x3) / 3;
    int yc = (y1 + y2 + y3) / 3;
    
    float angle;
    cout << "Enter the rotation angle: ";
    cin >> angle;
    float rad = angle * M_PI / 180.0;
    
    int X1 = xc + (int)((x1 - xc) * cos(rad) - (y1 - yc) * sin(rad));
    int Y1 = yc + (int)((x1 - xc) * sin(rad) + (y1 - yc) * cos(rad));
    int X2 = xc + (int)((x2 - xc) * cos(rad) - (y2 - yc) * sin(rad));
    int Y2 = yc + (int)((x2 - xc) * sin(rad) + (y2 - yc) * cos(rad));
    int X3 = xc + (int)((x3 - xc) * cos(rad) - (y3 - yc) * sin(rad));
    int Y3 = yc + (int)((x3 - xc) * sin(rad) + (y3 - yc) * cos(rad));
    
    setcolor(RED);
    int rotatedTri[] = {X1, Y1, X2, Y2, X3, Y3, X1, Y1};
    drawpoly(4, rotatedTri);
    
    cout << "Clockwise rotation completed. Press any key to continue...";
    getch();
    closegraph();
}

void rotateTriangleAntiClockwise() {
    int gd = DETECT, gm;
    initgraph(&gd, &gm, "C:\\Turboc3\\BGI"); // Use the correct BGI path
    
    int x1, y1, x2, y2, x3, y3;
    cout << "Enter (x1, y1), (x2, y2), (x3, y3) for the triangle: ";
    cin >> x1 >> y1 >> x2 >> y2 >> x3 >> y3;
    
    int tri[] = {x1, y1, x2, y2, x3, y3, x1, y1};
    setcolor(WHITE);
    drawpoly(4, tri);
    
    int xc = (x1 + x2 + x3) / 3;
    int yc = (y1 + y2 + y3) / 3;
    
    float angle;
    cout << "Enter the rotation angle: ";
    cin >> angle;
    float rad = angle * M_PI / 180.0;
    
    // For anticlockwise, we negate the angle (or equivalently, swap the signs of sin terms)
    int X1 = xc + (int)((x1 - xc) * cos(-rad) - (y1 - yc) * sin(-rad));
    int Y1 = yc + (int)((x1 - xc) * sin(-rad) + (y1 - yc) * cos(-rad));
    int X2 = xc + (int)((x2 - xc) * cos(-rad) - (y2 - yc) * sin(-rad));
    int Y2 = yc + (int)((x2 - xc) * sin(-rad) + (y2 - yc) * cos(-rad));
    int X3 = xc + (int)((x3 - xc) * cos(-rad) - (y3 - yc) * sin(-rad));
    int Y3 = yc + (int)((x3 - xc) * sin(-rad) + (y3 - yc) * cos(-rad));
    
    setcolor(BLUE);
    int rotatedTri[] = {X1, Y1, X2, Y2, X3, Y3, X1, Y1};
    drawpoly(4, rotatedTri);
    
    cout << "Anti-clockwise rotation completed. Press any key to exit...";
    getch();
    closegraph();
}

int main() {
    int choice;
    cout << "Triangle Rotation\n";
    cout << "1. Clockwise Rotation\n";
    cout << "2. Anti-clockwise Rotation\n";
    cout << "Enter your choice (1/2): ";
    cin >> choice;
    
    if (choice == 1)
        rotateTriangleClockwise();
    else if (choice == 2)
        rotateTriangleAntiClockwise();
    else
        cout << "Invalid choice!";
    
    return 0;
}
```

## Code Explanation (Line by Line)

### Header Files
```cpp
#include <iostream>      // For input/output
#include <conio.h>       // For getch() function
#include <graphics.h>    // For graphics functions
#include <math.h>        // For sin(), cos() and M_PI
```

### Graphics Initialization
```cpp
int gd = DETECT, gm;
initgraph(&gd, &gm, "C:\\Turboc3\\BGI");
```
- `DETECT` automatically detects the graphics driver
- `initgraph()` initializes the graphics system

### Triangle Input and Drawing
```cpp
int x1, y1, x2, y2, x3, y3;
cin >> x1 >> y1 >> x2 >> y2 >> x3 >> y3;
    
int tri[] = {x1, y1, x2, y2, x3, y3, x1, y1};
setcolor(WHITE);
drawpoly(4, tri);
```
- Gets the coordinates of three vertices
- Creates an array with coordinates (repeating the first point to close the triangle)
- `drawpoly(4, tri)` draws the polygon with 4 points (including the repeated first point)

### Centroid Calculation
```cpp
int xc = (x1 + x2 + x3) / 3;
int yc = (y1 + y2 + y3) / 3;
```
- The centroid is the average of all vertices

### Angle Conversion
```cpp
float angle;
cin >> angle;
float rad = angle * M_PI / 180.0;
```
- Converts degrees to radians (necessary for math functions)

### Rotation Calculation
For clockwise rotation:
```cpp
int X1 = xc + (int)((x1 - xc) * cos(rad) - (y1 - yc) * sin(rad));
int Y1 = yc + (int)((x1 - xc) * sin(rad) + (y1 - yc) * cos(rad));
```

For anticlockwise rotation:
```cpp
int X1 = xc + (int)((x1 - xc) * cos(-rad) - (y1 - yc) * sin(-rad));
int Y1 = yc + (int)((x1 - xc) * sin(-rad) + (y1 - yc) * cos(-rad));
```

- The formula translates each point relative to the centroid
- Applies rotation using trigonometric functions
- Translates back to original coordinate system

### Drawing the Rotated Triangle
```cpp
setcolor(RED); // or BLUE for anticlockwise
int rotatedTri[] = {X1, Y1, X2, Y2, X3, Y3, X1, Y1};
drawpoly(4, rotatedTri);
```
- Sets a different color to distinguish the rotated triangle
- Creates a new array with rotated coordinates
- Draws the rotated triangle

## Key Observations and Clarifications

1. **Clockwise vs. Anticlockwise**: The difference between clockwise and anticlockwise rotation is the direction of angle measurement. Mathematically, this is achieved by negating the angle value.

2. **Formula Correction**: The correct 2D rotation formulas are:
   ```
   x' = xc + (x-xc)·cos(θ) - (y-yc)·sin(θ)
   y' = yc + (x-xc)·sin(θ) + (y-yc)·cos(θ)
   ```
   For anticlockwise rotation, use θ as the angle; for clockwise, use -θ (or equivalently, swap the signs of the sin terms).

3. **Centroid**: The centroid is used as the pivot point. If you want to rotate around a different point, you can replace the centroid calculation with any arbitrary point.

## Important Concepts and Potential Questions

### Basic Understanding

**Q: What is the mathematical difference between clockwise and anticlockwise rotation?**

A: The key difference is the sign of the angle. For anticlockwise rotation, we use a positive angle, while for clockwise rotation, we use a negative angle (or equivalently, swap the signs of the sine terms in the rotation formula).

**Q: Why do we need to convert degrees to radians in the code?**

A: C++ trigonometric functions (sin, cos) require angles in radians, not degrees. The conversion formula is: radians = degrees × π/180.

### Mathematical Foundation

**Q: Write the general formula for rotating a point (x,y) around a pivot point (xc,yc) by angle θ.**

A: For rotation by angle θ:
- x' = xc + (x-xc)·cos(θ) - (y-yc)·sin(θ)
- y' = yc + (x-xc)·sin(θ) + (y-yc)·cos(θ)

**Q: What happens if we rotate a point by 360°? By 180°?**

A: Rotation by 360° returns the point to its original position. Rotation by 180° reflects the point through the pivot point.

### Implementation Details

**Q: What would change in the code if we wanted to rotate around the origin instead of the centroid?**

A: We would set xc=0 and yc=0, simplifying the formula to:
- x' = x·cos(θ) - y·sin(θ)
- y' = x·sin(θ) + y·cos(θ)

**Q: Why are we using the drawpoly() function with 4 points for a triangle?**

A: The drawpoly() function draws a polygon by connecting points in sequence. We use 4 points because we repeat the first point (x1,y1) at the end to close the triangle.

### Graphics Concepts

**Q: Why do we initialize the graphics mode at the beginning of the program?**

A: The graphics mode initialization (initgraph function) is necessary to enable graphical output on the screen. It sets up the graphics driver and establishes the coordinate system.

**Q: What are the limitations of the centroid-based rotation implemented in this experiment?**

A: The current implementation only allows rotation around the centroid of the triangle. It doesn't allow for rotation around arbitrary points or interactive rotations.

### Error Analysis

**Q: What causes the rounding errors in the rotation, and how might they affect the shape after multiple rotations?**

A: The rounding errors occur because we convert floating-point calculations to integers for pixel coordinates. After multiple rotations, these errors can accumulate, causing the triangle to drift or deform slightly.

**Q: What would happen if we applied multiple rotations sequentially? Would the result be the same as applying a single rotation of the sum of angles?**

A: Mathematically, sequential rotations should be equivalent to a single rotation by the sum of angles. However, due to rounding errors in computer implementations, there might be slight differences after multiple rotations.

### Algorithm Improvements

**Q: How would you modify the code to rotate around a user-specified point rather than the centroid?**

A: We would prompt the user to input the coordinates of the pivot point (xc,yc) instead of calculating the centroid.

**Q: How could this rotation algorithm be extended to handle any polygon, not just triangles?**

A: We would need to create a loop that applies the rotation formula to each vertex of the polygon. The code would accept an array of points and the number of vertices as input.

### Theoretical Extensions

**Q: How is rotation related to other transformations like scaling and translation?**

A: Rotation, scaling, and translation are all affine transformations that can be combined using matrix multiplication. Together they form the foundation of computer graphics transformations.

**Q: What is a transformation matrix, and how would you express the rotation operation as a matrix?**

A: A 2D rotation by angle θ can be represented by the matrix:
```
[cos(θ) -sin(θ)]
[sin(θ)  cos(θ)]
```

When rotating around a point other than the origin, we combine this with translation matrices.

## Learning Outcomes

- Learned how rotation transformation works in computer graphics using trigonometric functions (sin, cos)
- Explored the difference between clockwise and anti-clockwise rotation by modifying angle signs
- Understood the importance of centroid (xc, yc) in rotating a shape around its center rather than the origin
- Gained hands-on experience in using C++ graphics.h library functions like initgraph(), drawpoly(), and setcolor() for visual representation
- Learned the necessity of converting degrees to radians for mathematical operations
