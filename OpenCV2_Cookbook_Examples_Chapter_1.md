

# Introduction #

To work with OpenCV from a Java platform you need to install OpenCV and the JavaCV.
The examples use a bit different setup than default.
It is described below.

The example code can be used in any IDE or from command line.
Description here focused on using IntelliJ IDEA, and show how it can be setup run each example with minimum effort.
If you have experience with Eclipse, NetBeans, or other, you should be able to use them too.

The idea is that once you are setup you can run any JavaCV example, or you own JavaCV code,
by simply right clicking on a code file and selecting 'Run'. Please go through a couple of steps below to get it ready.
If you have some suggestions how to make this process simpler please comment at the bottom of the page or send an email.

Examples here are written in Scala.
IntelliJ IDEA as it has an excellent support for Scala, and it is also an excellent Java IDE.
The setup works with both the free IDEA Community and the paid IDEA Ultimate editions.

## Installing IDE for work with JavaCV ##
You will need to download and install the development environment components:

  * [Java SE SDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
  * [IntelliJ IDEA](http://www.jetbrains.com/idea/)
  * [Scala](http://www.scala-lang.org/downloads), optional but recommended for Scala development.

Once you have IDEA installed you can install IDEA's Scala plugin.

  1. Startup IDEA and
  1. Select from the menu Settings > Plugins > Available.
  1. Click on the "Available" tab and wait for IDEA to download list of plugins from its website
  1. Find Scala plugin on the list, then right-click and select "Download and Install"
  1. After the plugin installs you will need to restart IDEA

## Getting the OpenCV Cookbook Examples for JavaCV ##
The OpenCV Cookbook Examples for JavaCV are available through Subversion code repository.
You can download it isung IDEA, described in next section, or you can also use your favorite Subversion client follwing information on the examples [Source](https://code.google.com/p/javacv-examples/source/checkout) page.

## Downloading Examples using IDEA ##

  1. Start IDEA
  1. Select from menu: `Version Control` > `Checkout from Version Control` > `Subversion` <br> <img src='http://javacv-examples.googlecode.com/svn/wiki/images/Ch1_Checkout_from_Subversion_1.png' />
<ol><li>Click on the "+" next to <code>Repositories</code> and add location of the <code>OpenCV2_Cookbook</code> examples: <code>http://javacv-examples.googlecode.com/svn/trunk/</code> <br> <img src='http://javacv-examples.googlecode.com/svn/wiki/images/Ch1_New_Repository_Location_1.png' />
</li><li>Click <code>OK</code> to add return to <code>Checkout from Subversion</code> dialog.<br>
</li><li>Select <code>http://javacv-examples.googlecode.com/svn/trunk/</code>  <br>  <img src='http://javacv-examples.googlecode.com/svn/wiki/images/Ch1_Checkout_from_Subversion_2.png' />  <br> And click on <code>Checkout</code>
</li><li>Select location for the example code (you may have to create a new folder, call it <code>javacv-examples</code>)<br>
</li><li>Confirm checkout options (default should be fine)<br>
</li><li>Confirm repository format version (default should be fine)<br>
</li><li>Wait for IDEA to download the examples<br>
</li><li>Once download is finished, IDEA will ask you whether to create a project for the examples. Select <code>No</code> since the checkout already has project definintion.<br>
</li><li>Select from manu <code>File</code> > <code>Open Project...</code> and select the folder where you have checked out the code.</li></ol>

<h2>...</h2>
...<br>
<br>
<h2>Installing OpenCV and JavaCV Libraries</h2>
Now you need to get OpenCV and JavaCV libraries.<br>
The recommended way is to use  pre-configured combined OpenCV+JavaCV binaries that can be downloaded with the examples.<br>
The archive contains all the needed native dependencies for OpenCV and JavaCV in a single directory.<br>
It is intended to be extracted into a <code>sandbox</code> subdirectory under the <code>OpenCV2_Cookbook</code> directory<br>
Make sure that they the binaries are in <code>sandbox</code> not in its subdirectory.<br>
You project structure should look like this <code>[image]</code>.<br>
<br>
<h2>Setup Working Directory</h2>

And the very last step of setup, configure default startup directory.<br>
<ol><li>Select <code>Run</code> > <code>Edit Configurations</code>
</li><li>Expand the <code>Defaults</code> node and select <code>Application</code>
</li><li>Under working directory type <code>$MODULE_DIR$\sandbox</code></li></ol>

<h2>Run the Examples</h2>
Now you are ready to test the examples. For instance, to run the first example from chapter 1:<br>
<ol><li>in project window select Ex1MyFirstOpenCVApp<br>
</li><li>Right click on it and select <code>Run</code></li></ol>

If everything goes fine the example will be compiled and run. It should open the image and display it on the screen. <br> [Ch1_My_Image_1.png]<br>
<br>
<h2>Troubleshooting</h2>
<h3>UnsatisfiedLinkError</h3>
If you get an error message that looks like this<br>
<pre><code>Exception in thread "main" java.lang.UnsatisfiedLinkError: no jniopencv_core in java.library.path<br>
	at java.lang.ClassLoader.loadLibrary(ClassLoader.java:...<br>
</code></pre>
This means that you native binaries are not setup correctly. Make sure that you follow instructions in section<br>
[OpenCV2_Cookbook_Examples_Chapter_1.wiki#Installing_OpenCV_and_JavaCV_Libraries Installing OpenCV and JavaCV Libraries] and<br>
in [OpenCV2_Cookbook_Examples_Chapter_1.wiki#Setup_Working_Directory Setup_Working_Directory]<br>
<br>
<h3>NullPointerException in CanvasFrame.showImage()</h3>
If you get an error message that looks like this<br>
<pre><code>Exception in thread "main" java.lang.NullPointerException<br>
	at com.googlecode.javacv.CanvasFrame.showImage(CanvasFrame.java:331)<br>
	at opencv2_cookbook.chapter01.Ex01MyFirstOpenCVApp$delayedInit$body.apply(Ex01MyFirstOpenCVApp.scala:31)<br>
	...<br>
</code></pre>
Congratulations, your first JavaCV application actually started but had trouble loading an image.<br>
The <code>Ex01MyFirstOpenCVApp</code> is very simple and does not check if image was actually loaded.<br>
If it was not the <code>image</code> variable is set to <code>null</code>.<br>
It is then passed to CanvasFrame and is causing an exception.<br>
You may need to check if the image is in the right place in the relation to the startup directory.<br>
<br>
<h1>Loading, Displaying, and Saving Images with JavaCV</h1>

A simple example of loading and displaying an image using JavaCV is in class <code>opencv2_cookbook.chapter01.Ex01MyFirstOpenCVApp</code>:<br>
<pre><code>import com.googlecode.javacv.CanvasFrame<br>
import com.googlecode.javacv.cpp.opencv_highgui._<br>
import javax.swing.JFrame._<br>
<br>
object Ex01MyFirstOpenCVApp extends App {<br>
<br>
    // read an image<br>
    val image = cvLoadImage("boldt.jpg")<br>
<br>
    // create image window named "My Image"<br>
    val canvas = new CanvasFrame("My Image")<br>
<br>
    // request closing of the application when the image window is closed<br>
    canvas.setDefaultCloseOperation(EXIT_ON_CLOSE)<br>
<br>
    // show image on window<br>
    canvas.showImage(image)<br>
}<br>
</code></pre>
It is based on the example on page 18 of the cookbook. Note how <code>CanvasFrame</code> from JavaCV API is used to display the image.<br>
<br>
<h2>Loading Images</h2>

JavaCV methods for loading images and saving images are based on based on OpenCV. They are in the class <code>com.googlecode.javacv.cpp.opencv_highgui</code>.<br>
Note that class is in named starting with small letter to look similar to the C++ module <code>opencv_highgui</code> where OpenCV method for reading and writing images are located.<br>
Images can be loaded in two formats <code>IplImage</code> using <code>cvLoadImage</code> and <code>CvMat</code> using <code>cvLoadImageM</code>.<br>
<code>cvLoadImage</code> takes one or two parameters.<br>
The first parameter is a file name, the second is a conversion parameter, frequently used to use color images area gray scale.<br>
Here are some examples.<br>
<pre><code>import com.googlecode.javacv.cpp.opencv_highgui._<br>
import com.googlecode.javacv.cpp.opencv_core.IplImage<br>
<br>
val image1: IplImage = cvLoadImage("../data/boldt.jpg")<br>
val image2: IplImage = cvLoadImage("../data/boldt.jpg", CV_LOAD_IMAGE_COLOR)<br>
val image3: IplImage = cvLoadImage("../data/boldt.jpg", CV_LOAD_IMAGE_GRAYSCALE)<br>
</code></pre>
The default value for the conversion parameter is <code>CV_LOAD_IMAGE_COLOR</code>.<br>
<br>
To load image in <code>CvMat</code> format use <code>cvLoadImageM</code>, parameter are the same as for <code>cvLoadImage</code>:<br>
<pre><code>import com.googlecode.javacv.cpp.opencv_core.CvMat<br>
<br>
val image4: CvMat = cvLoadImageM("../data/boldt.jpg")<br>
val image5: CvMat = cvLoadImageM("../data/boldt.jpg", CV_LOAD_IMAGE_COLOR)<br>
val image6: CvMat = cvLoadImageM("../data/boldt.jpg", CV_LOAD_IMAGE_GRAYSCALE)<br>
</code></pre>

If image cannot be loaded both <code>cvLoadImage</code> and <code>cvLoadImageM</code> return <code>null</code>. They do not throw exceptions.<br>
You may want to wrap a call to <code>cvLoadImage</code> (or <code>cvLoadImageM</code>) in a method that throws an exception if an image cannot be loaded.<br>
<pre><code>def load(file: File, flags: Int = CV_LOAD_IMAGE_GRAYSCALE): IplImage = {<br>
    // Verify file<br>
    if (!file.exists()) {<br>
        throw new FileNotFoundException("Image file does not exist: " + file.getAbsolutePath)<br>
    }<br>
    // Read input image<br>
    val image = cvLoadImage(file.getAbsolutePath, flags)<br>
    if (image == null) {<br>
        throw new IOException("Couldn't load image: " + file.getAbsolutePath)<br>
    }<br>
    // Return loaded image<br>
    image<br>
}<br>
</code></pre>

<h2>Saving Images</h2>

The method <code>cvSaveImage(filename, image)</code> saves the image to the specified file.<br>
The image format is chosen based on the filename extension.<br>
The method returns an error code.<br>
<pre><code> val err : Int = cvSaveImage("my_image.png", image1)<br>
</code></pre>

<h2>Displaying Images</h2>

The easy way to display image using JavaCV is to use <code>CanvasFrame</code> as in the example <code>Ex01MyFirstOpenCVApp</code>, see above or <a href='https://code.google.com/p/javacv-examples/source/browse/trunk/OpenCV2_Cookbook/src/opencv2_cookbook/chapter01/Ex01MyFirstOpenCVApp.scala'>here</a>.<br>
It shows the image in a new window.<br>
<br>
JavaCV also add to  <code>IplImage</code> a method <code>getBufferedImage</code> to convert OpenCV data to Java's <code>java.awt.image.BufferedImage</code> that can be displayed using standard Java approach.<br>
You can see example of that in <code>Ex2MyFirstGUIApp</code>, see next section.<br>
<br>
<br>
<h1>Creating a GUI application using Scala Swing</h1>

It is not an intention of this module to describe how to create GUI applications in Scala or Java.<br>
However for the sake of completeness an equivalent of a Qt GUI application presented in the Cookbook is provided.<br>
As the original, it is a simple frame with two buttons "Open Image" and "Process" on the left.<br>
Loaded image is displayed in the middle of the frame. The example is using Scala Swing framework, which may be interesting in its own right.<br>
<br>
<img src='http://javacv-examples.googlecode.com/svn/wiki/images/Ex01MyFirstOpenCVApp.png' />

You can find code for the <code>Ex2MyFirstGUIApp</code> example <a href='https://code.google.com/p/javacv-examples/source/browse/trunk/OpenCV2_Cookbook/src/opencv2_cookbook/chapter01/Ex2MyFirstGUIApp.scala'>here</a>.