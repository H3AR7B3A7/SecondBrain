# PlantUML  
  
PlantUML is an open-source tool allowing users to create **diagrams** from a plain text language.  
It also supports various other Software development related formats, as well as **visualisation** of JSON and YAML files.  
  
[Official Documentation](https://plantuml.com/)  
  
  
## Creating Diagrams  
  
We can use the online server provided by [plantuml.com](http://www.plantuml.com/plantuml/uml/SoWkIImgAStDuU9oICrB0J80).  
We can also download the [runnable JAR](https://sourceforge.net/projects/plantuml/files/plantuml.jar/download) to run locally  
using our preferred text editor while editing any file with a compatible extension,  
or use the command line.  
  
Example:  
>java -jar plantuml.jar sequenceDiagram.txt  
  
To create a diagram we use these start and end tags:  
```  
@startuml  
...  
@enduml  
```  
Following are rules specific to different diagrams and their use.  
  
## Sequence Diagram  
  
*Used to draw a message between two participants.*  
  
### Arrows  
  
```  
participant1 -> participant2: message  
```  
  
```  
-> Arrow
--> Dotted arrow
->> Thin arrow
-->> Thin dotted arrow
-\ Half top arrow
-/ Half bottom arrow
-\\ Thin half top arrow
-// Thin half bottom arrow
--\\ Thin dotted half top arrow
--// Thin dotted half bottom arrow
```  
  
Any of these arrows can go in either or both directions and can end or start with 'x' or 'o'.  
  
```  
->o  
->x  
```  
  
### Participants  
  
```  
(type) (name) as (alias) order (number) (hex color)  
(type) "(name)" as (alias) order (number) (hex color)  
(type) (alias) as "(name)" order (number) (hex color)  
```  
Types:  
- participant  
- actor  
- boundary  
- control  
- entity  
- database  
- collections  
- queue  
  
### Comments  
  
```  
' Single line  
/' Multiple lines '/  
```  
  
### Auto Numbering  
  
```  
autonumber (base) (increment) "(format)"  
```  
  
Auto numbering can be stopped or resumed (with another increment and/or format)  
```  
autonumber stop  
autonumber resume (increment) "(format)"  
```  
  
### Styling
  
  
---  
*Work in progress...*