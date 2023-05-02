Download Link: https://assignmentchef.com/product/solved-cop4600-p2-posix-standards-bindings
<br>
Overview

Modern operating systems are often built in layers with specific goals and limited privileges. Layering also facilitates the implementation of recognized standards by separating hardware and OS-specific implementations from generalized API calls. Often these layers are written in different languages and permit access via a binding layer to lower level functionality. In Android, POSIX functions can be called from Java applications via the Native Development Kit (NDK).




In this project, you will build a C++ language function that calls POSIX system library procedures to read a text file and return it as a C-style string (null-terminated character array). You will also build two programs that use your C++ functions – a simple program at the Android application layer that uses the NDK binding to call you C++ functions to read and display a text file in an application window, and another version that will print the text file to the screen in Ubuntu. We will provide a program that exercises new call and program on the command line. You’ll then create a short video to demonstrate your code. You’ll submit the project via Canvas.




<strong>NOTE: Take Snapshots in VirtualBox! You will most likely brick your machine at some point during this or other projects, and you will not want to start from scratch. <u>No, seriously – take snapshots!</u> </strong>

<h1>Structure</h1>

The project is broken into four main parts:




<ul>

 <li>Create a C++ function that reads a text file via POSIX calls and returns a pointer to its contents</li>

 <li>Create a short program that uses the function above to display a file via the command line</li>

 <li>Create a simple Android GUI application that accepts a text file name as input and has a text box</li>

 <li>Bind the function via the NDK to that the application to display the contents of the file in the text box</li>

</ul>




<strong>Figure 1: A function is called from a text program, and separately, bound to the GUI application. </strong>




While exact implementation may vary, the library functions must match the signatures laid out in this document, and the system calls must apply the security model properly.




<h2>Specification</h2>

Students will write several sections of code according the following specifications.

<strong> </strong>

<u>File Reader Library</u>

The file <strong>read_file.h</strong> and <strong>read_file.cpp</strong> will contain declaration and definition, respectively, of this function:




<em>char *read_file(const char *filename) </em>

Makes POSIX calls to read the contents of filename from disk to be stored in a null-terminated character array (C-style string). The array should be allocated dynamically. A pointer to the array will be returned. <strong><em>The caller will be expected to free the memory allocated for the array.</em></strong>




<u>Text Program</u>

The text program, once built, should have the name displayfile and should take exactly one command line argument – the filename of the file to be displayed on the screen. It should use the read_file() function:




<strong>$</strong><strong> displayfile /sdcard/example.txt </strong>

<strong>Hello world! </strong>

<strong>This is the last line of the file. </strong>

<strong>$  </strong>




<u>Contexts of /sdcard/example.txt:</u>

Hello world!

This is the last line of the file.




<u>GUI Program</u>

The GUI program skeleton <strong><u>provides</u></strong> three GUI elements (without functional code). Students must add code as necessary to elicit the following behavior:




<ul>

 <li>One-line text box where the file to be displayed will be typed by the user, named <strong>filenameBox</strong></li>

 <li>Button to submit the filename (which should trigger the read and display), named <strong>submitButton</strong></li>

 <li>Multi-line text box where the file will be displayed when the button is pressed, named <strong>displayBox</strong></li>

</ul>




Students should modify the Java source to invoke the C++ functions. A simple example of transmitting a string from C++ to Java is included in the project base code.




<strong>NOTE: </strong>You will need to add any new C++ source files to the <strong>CMakeLists.txt </strong>build file!

<h1>Submissions</h1>

You will submit the following at the end of this project:




<ul>

 <li>Report on Canvas</li>

 <li>Screencast on Canvas</li>

 <li>Compressed tar archive (<strong>tgz</strong>) containing source/build files for text program on Canvas</li>

 <li>Zip archive (<strong>zip</strong>) containing source/build files for the GUI program on Canvas</li>

</ul>

<strong> </strong>

<h2>Report</h2>

Your report will explain how you implemented the function and programs, including which POSIX calls were invoked and why.  It will include description of how testing was performed along with any known bugs. The report may be in Portable Document Format (pdf) or plain-text (txt). The report should be no more than a page and should cover all relevant aspects of the project.




<h2>Screencast</h2>

In addition to the written text report, you should submit a screencast (with audio) walking through the code you wrong to build the two applications and invoke the POSIX calls (~5 minutes).




<h2>Compressed Archive (displayfile.tgz)</h2>

Your compressed tar file should have the following directory/file structure:




displayfile.tgz

displayfile.tar    displayfile (directory)

read_file.h

read_file.cpp

displayfile.cpp







To build the text program, we will execute these commands:




<strong>tar zxvf displayfile.tgz cd displayfile </strong>

<strong>c++ displayfile.cpp read_file.cpp -o displayfile cd .. </strong>

<strong> </strong>

We’ll run commands like this to test the text program:




<strong>displayfile/displayfile example.txt </strong>

<strong>displayfile/displayfile /home/reptilian/example.txt </strong>




To include the read_file() function in our tests, we’ll using this directive in C:

<strong> </strong>

<strong>#include “displayfile/read_file.h” </strong>




To test the read_file() function in a program, we will execute this command:

<strong> </strong>

<strong>c++ program_name.cpp displayfile/read_file.cpp -o program_name </strong>




<h2>Zip Archive (nativeapp.zip)</h2>




To create a compact package from your Android project, select <strong>File </strong>à<strong> Export to Zip File</strong> from the Android Studio menu system. This will package your project for upload.




Please test your functions before submission! If your code does not compile it will result in <strong><u>zero credit</u></strong> (0, none, goose-egg) for that portion of the project.