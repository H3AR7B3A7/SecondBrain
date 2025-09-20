# Analysis
Some [[Best Practice(s)]] tips when performing an analysis:

- You should be able to read the story in 6 months or a year and understand it.  
- **Out of scope** is important. This prevents you from dragging in extra stuff. It is your guardian when you are time constrained.  
- **Dependencies** can block the implementation. Think of: teams (incl ATG), other stories assumed implemented before.
  
## Goals
- What should the system be capable of when you finished this story that it was not capable of before?
- Why doesn't the system do this now? 
- Should be close to 'For QA'. 
  
## Tasks
- Clearing out (a good balance of) details:
	- What do we need to do to achieve this?
- The tasks lists is a guideline for the other developers to base their estimation on:
	- Are the tasks complex or not?  
	- Are there many tasks or not?  
	- Do the tasks need to be repeated multiple times (e.g. across multiple services)?  

### Do
- Explain which components are touched and why  
- Entry point in the system (how does data enter the system to achieve the goal)  
- Exit points from the system (where does data leave the system, or where is it stored to achieve the goal)  
- Take into account error scenarios (not only the happy path), except when error scenarios are stated explicitly in 'Out of scope' and are handled in a different story  

### Don't
- Just say: 'Implement this'
- Repeat goal  
- Change this line in this class (unless for really small stuff, to prevent that the person who implements it has to go looking for that line again)  

*Think of non functional implementations (resource usage, performance, logging, ...). They might also take a lot of time to implement.*
   
## For QA:  
- Simplest scenario to test. QA will come up with multiple variants themselves to break the code  
- What does QA need to test this? Branch, services, containers are known most of the times. This is more about the special stuff (HW, data) needed.  
  
## Questions and remarks:  
- Sketchbook for your thoughts. ideal place for brain dumps.  
- Archive for questions asked to PO and architect. And their answers: 'small decision' archive.  
- Answers: do not only write down yes/no. But also why. The fact that the answer is Yes can be always be retrieved from the code. The why usually not.



---
#BestPractice 