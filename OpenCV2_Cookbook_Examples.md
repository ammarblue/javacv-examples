

# Overview #

[OpenCV](http://opencv.willowgarage.com/) (Open Source Computer Vision) is a library of several hundred algorithms for computer vision and video analysis.
It started in the late 90’s as a C library; in version 2 a C++ API was added.

[JavaCV](https://code.google.com/p/javacv/) is a wrapper that allows accessing the OpenCV library directly from within Java Virtual Machine (JVM) and Android platform.
JavaCV wraps C API wherever possible, and C++ API when necessary.

The OpenCV\_Cookbok example module is intended as a companion to the book “[OpenCV 2 Computer Vision Application Programming Cookbook](http://www.laganiere.name/opencvCookbook/)” by Robert Laganière.
In what follows we will refer to them as the (JVM) example module and the Cookbook, respectively.
The original examples in the Cookbook are written in C++, sometimes using parts of OpenCV that are not accessible from JavaCV.
This example module shows how to use OpenCV C API, available through JavaCV, to perform the same tasks.

The code in the example module is written in [Scala](http://www.scala-lang.org), one of the leading JVM languages.
It can be easily converted to Java and other languages running on JVM, for instance, [Groovy](http://groovy.codehaus.org/).

# Quick Sample #
Here is a quick preview that compares an original C++ example in the Cookbook (p. 18)
with code in Scala and Java using JavaCV wrapper.

Here is the original C++ example that opens an image (without error cheking), creates a window,
displays image in the window, and waits for 5 seconds before exiting.

```
#include <opencv2/core/core.hpp>
#include <opencv2/highgui/highgui.hpp>

int main() {

    // read an image
    cv::Mat image = cv::imread("boldt.jpg");
    
    // create image window named "My Image"
    cv::namedWindow("My Image");
    
    // show image on window
    cv::imshow("My Image", image);
    
    // wait kwy for 5000 ms
    cv::waitKey(5000);

    return 1;
}
```

The above C++ example translated to Scala using JavaCV wrapper:
```
import com.googlecode.javacv.CanvasFrame
import com.googlecode.javacv.cpp.opencv_highgui._

object MyFirstOpenCVApp extends App {
    
    // read an image
    val image = cvLoadImage("boldt.jpg")

    // create image window named "My Image"
    val canvas = new CanvasFrame("My Image")

    // request closing of the application when the image window is closed
    canvas.setDefaultCloseOperation(javax.swing.JFrame.EXIT_ON_CLOSE)

    // show image on window
   canvas.showImage(image)
}
```

Now the same example expressed in a Java. Note that use of JavaCV API is exactly the same in Scala and Java code.
```
import com.googlecode.javacv.CanvasFrame;
import static com.googlecode.javacv.cpp.opencv_core.IplImage;
import static com.googlecode.javacv.cpp.opencv_highgui.cvLoadImage;

public class MyFirstOpenCVApp {

    public static void main(String[] args) {
        
        // read an image
        final IplImage image = cvLoadImage("boldt.jpg");
        
        // create image window named "My Image"
        final CanvasFrame canvas = new CanvasFrame("My Image");
        
        // request closing of the application when the image window is closed
        canvas.setDefaultCloseOperation(javax.swing.JFrame.EXIT_ON_CLOSE);
                
        // show image on window
        canvas.showImage(image);
    }
}
```

# How to use JavaCV Examples #
This example module is intended as a companion to the Cookbook. The recommended way is to read the Cookbook and refer to JavaCV examples when in doubt how to translate the Cookbook’s C++ code to JavaCV. The Cookbook provides explanation how the algorithms work. The JavaCV examples provide only very brief comments.

Simplest way to use the JavaCV examples is to browse the code [on-line](https://code.google.com/p/javacv-examples/source/browse/#svn%2Ftrunk%2FOpenCV2_Cookbook%2Fsrc%2Fopencv2_cookbook) or use SVN to check them out to your computer https://code.google.com/p/javacv-examples/source/checkout

With a little bit of setup you can execute the examples on you own computer.
The benefit is that you can start modifying the examples and build your own algorithms.
The setup is explained in this module comments for [Chapter 1](OpenCV2_Cookbook_Examples_Chapter_1.md).

# Organization of the Example Code #
The code is organized into packages that correspond to chapters in the Cookbook, for instance [opencv2\_cookbook.chpater8](https://code.google.com/p/javacv-examples/source/browse/#svn%2Ftrunk%2FOpenCV2_Cookbook%2Fsrc%2Fopencv2_cookbook%2Fchapter08).
Individual examples roughly correspond to sections within each chapter.

  * [Chapter 1](OpenCV2_Cookbook_Examples_Chapter_1.md) describes IDE setup to run the examples, gives a basic example of loading and displaying an image, and an example of a basic GUI example that does basic image processing.

# List of Examples #

  * Chapter 1
    1. `Ex01MyFirstOpenCVApp` - load an image and show it in a window (CanvasFrame)
    1. `Ex2MyFirstGUIApp` - Simple GUI application build using Scala Swing. The application has two buttons on the left
> > > "Open Image" and "Process". The opened image is displayed in the middle. When "Process" button
> > > is pressed the image is flipped upside down and its red and blue channels are swapped.
  * Chapter 2
    1. `Ex01Salt` - Set individual, randomly selected, pixels to a fixed value. Use ImageJ's ImageProcessor to access pixels.
    1. `Ex02ColorReduce` - Reduce colors in the image by modifying color values in all bands the same way.
    1. `Ex03Sharpen` - Use kernel convolution to sharpen an image: `filter2D()`.
    1. `Ex04BlendImages` - Blend two images using weighted addition: `cvAddWeighted()`.
    1. `Ex05ROILogo` - Paste small image into a larger one using a region of interest: `IplROI` and `cvCopy()`.
  * ...
  * Chapter 5
    1. `Ex1ErodingAndDilating` - Morphological erosion and dilation: `cvErode()` and `cvDilate()`.
    1. `Ex2OpeningAndClosing` - Morphological opening and closing: `cvMorphologyEx()`.
    1. `Ex3EdgesAndCorners` - Detection of edges and corners using morphological filters.
    1. `Ex4WatershedSegmentation` - Image segmentation using watershed algorithm.
  * ...
  * Chapter 8
    1. `SIFT` - Extraction SIFT features using C++ API: `SiftFeatureDetector`
    1. `SURF` - Extraction SURF features using C++ API: `SurfFeatureDetector`
    1. `SURF_c` - Extraction SURF features using C API: `cvExtractSURF`
  * ...
  * Utilities
    1. `OpenCVUtils` - reading and writing of image files, display of images, drawing of features on images, conversions between OpenCV image representations.
    1. `OpenCVImageJUtils` - conversion between OpenCV and ImageJ image representations.

# Why Scala? #
[Scala](http://www.scala-lang.org) was chosen since it is more expressive than Java. You can achieve the same result with smaller amount of code. Smaller boilerplate code makes examples easier to read and understand. Unlike many other JVM languages, compiled Scala code is fast, on par with Java. Custom image processing code may require loops over image pixels. Specialized Scala compiler plugins, like [ScalaCL](https://code.google.com/p/scalacl/wiki/ScalaCLPlugin), can optimize and significantly speed up execution of loops.
Scala supports writing of scripts, code that can be executed without explicit compiling. Scala also has a console, called REPL, where single lines of code can be typed in and executed on a spot. Both of those features make prototyping of OpenCV-based programs easier in Scala than in Java.
Last but not least, IDE support for Scala reached level of maturity allowing easy creation, modification, and execution of Scala code. In particular, the Scala plugin for JetBrains IDEA works very well. Scala plugins Eclipse and NetBeans are also improving.
