# My First GWT App

## Google Web Toolkit
Google Web Toolkit is an open-source set of tools that allows web developers to create and maintain JavaScript front-end applications in [[Java]]. Other than a few native libraries, everything is Java source that can be built on any supported platform with the included GWT Ant build files. It is licensed under the Apache License 2.0.

GWT emphasizes reusable approaches to common web development tasks, namely asynchronous remote procedure calls, history management, bookmarking, UI abstraction, internationalization, and cross-browser portability.

## Installing GWT
[Download](http://www.gwtproject.org/download.html), and unzip GWT to your hard drive.

_Check your IDE for popular plugins. Or download the eclipse version of GWT, if for some reason you use Eclipse IDE._

## Running This Project
While you should be able to run this project in devmode, you will need to add gwt-users.jar to the classpath to recognize the symbols from gwt libraries. In Intellij just go to 'project structure' > 'libraries' and press '+'. Now just navigate to the 'gwt-user.jar' in you GWT installation directory and press 'ok'.

## Generating An App
> .\gwt-2.9.0\webAppCreator -out "C:\Users\Admin\Idea Projects\MyFirstGwtApp" "be.steven.d.dog.MyFirstGwtApp"

## Tutorial
We can find a tutorial on the official webpages [here](http://www.gwtproject.org/doc/latest/tutorial/gettingstarted.html).

## Super Dev Mode
Super Dev Mode replaces the internals of Dev Mode (since v2.7) with a different approach that works better in modern browsers. Like its predecessor, Super Dev Mode allows GWT developers to quickly recompile their code and see the results in a browser. It also allows developers to use a debugger to inspect a running GWT application.

-   With an ANT build we can use it by running:
> ant devmode

-   With a Maven build we can run it by running:
> mvn gwt:devmode

## Debugging in IntelliJ
-   Add a new Run/Debug Configuration of type 'JavaScript Debug'
-   Give it a name and enter the URL of your GWT application, for example: '[http://127.0.0.1:8888/MyFirstGwtApp.html](http://127.0.0.1:8888/MyFirstGwtApp.html)' (the one you get if you press 'Copy to Clipboard' in the 'GWT Development Mode' window running superDevMode)
-   Choose a browser
-   Add mapping(s) between your local files and remote URLs. e.g.: src/be/steven/d/dog/client -> '[http://127.0.0.1:8888/MyFirstGwtApp.html](http://127.0.0.1:8888/MyFirstGwtApp.html)'
-   While running superDevMode, use the newly created configuration to start debug mode in IntelliJ.

## Styling
For relatively simple AI we can use widgets for styling our app programmatically.

### UIBuilder
However, GWT also has a powerful tool called [UiBinder](http://www.gwtproject.org/doc/latest/DevGuideUiBinder.html) that allows you to create complex interfaces using declarative XML files, which can reduce code size and complexity.

### Elemento
GWT Elemento is a library which tries to make working with GWT Elemental as easy as possible. In a nutshell Elemento brings the following features to the table:

Builder like API to easily create arbitrary large element hierarchies HTML templates, declarative event handling and support for handlebar-like expressions Support for dependency injection with GIN Helper methods to mix and match GWT Elemental and GWT Widgets In this blog post I will give a short introduction to some of Element’s features.

[GitHub](https://github.com/hal/elemento) [Notes on Elemento](http://hpehl.info/gwt-elemento.html)

## Compiling Java to JavaScript
After using ant 'ant build' or 'mvn build' we can find all the files needed to deploy our web application to a public web server.

## Internationalization
Different techniques:

-   Static String Internationalization
-   Dynamic String Internationalization
-   Localizable Interface

### Static String Internationalization
-   Create an interface depending on your needs:
    -   Extending com.google.gwt.i18n.client.Constants
    -   Extending com.google.gwt.i18n.client.Messages
-   Create unimplemented methods for each String we want to internationalize (with a @DefaultStringValue annotation for a default)
-   Create properties files with properties matching the function names
-   Add instance fields to the class, e.g.:
    
    ```
    private final MyFirstGwtAppConstants constants = GWT.create(MyFirstGwtAppConstants.class);
    ```
    
-   Use the constants functions everywhere instead of hardcoded strings
-   Add the locales to the .gwt.xml, e.g.:
    
    ```
    <extend-property name="locale" values="nl"/>
    ```
    
-   Set the locale
    -   Add an HTML tag to the of the application host page, containing the property name and value:
        
        ```
        <meta name="gwt:property" content="locale=nl">
        ```
        
    -   Append the client property value to the query string of the URL:
        
        ```
        http://127.0.0.1:8888/MyFirstGwtApp.html?&locale=nl
        ```
        

If you specify a client property (such as locale) in both a tag and the URL, the URL value takes precedence.

[More documentation](http://www.gwtproject.org/doc/latest/DevGuideI18n.html#DevGuideDynamicStringInternationalization)

## GWT RPC
A Google Web Toolkit Remote Procedure Call makes it easy for the client and server components of your web application to exchange Java objects over HTTP. We often refer to the server-side code that gets invoked as a service. Google based the implementation of a GWT RPC service on the well-known Java servlet architecture. Within the client code, you’ll use an automatically-generated proxy class to make calls to the service. GWT will handle serialization of the Java objects passing back and forth the arguments in the method calls and the return value.



---
#Java #Library 