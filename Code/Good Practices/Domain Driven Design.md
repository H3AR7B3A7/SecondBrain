# Domain Driven Design (DDD)
By Eric Evans  
  
## The Challenge of Complexity  
- For most software projects, the primary focus should be on the domain and domain logic.  
- Complex domain design should be based on a model.  
  
## Design vs Development  
- Development is iterative.  
- Developers and domain experts have a close relationship.  
  
### Extreme Programming  
- Recognize importance of design decisions  
- Communication over upfront design  
- Rapid adaptability  
- Incremental (small) improvements  
  
## Domain Model  
  
### Model  
- Interpretation of reality  
- Abstraction of aspects relevant to solve a problem  
- Ignores detail  
- Should clear up domain complexity  
  
### Domain  
- Subject area to which the user applies the programming  
- Usually has little to do with computers  
- Requires varying knowledge / experience  
  
### Utility  
- The model and the heart of the design shape each other.  
- The model is the backbone of a language used by all team members.  
- The model is distilled knowledge.  
  
### The Heart of Software  
= The ability to solve domain related problems.  
  
- Gaining understanding of the domain is of importance to the development.  
- Complexity in the heart of software should be tackled head-on.  
- Design techniques and systematic approaches can help tackle this complexity,   
even in unfamiliar domains.  
  
## Effective Modeling  
- Binding the model and the implementation  
- Cultivating a language based on the model  
- Developing a knowledge-rich model  
- Distilling the model  
- Brainstorming and experimenting  
  
### Knowledge Crunching  
When an analyst just digests information and is solely responsible for the execution,   
the process completely lacks feedback from the users. A play between domain experts and   
developers ensures a deep connection to the domain experts way of thinking.  
  
## Continuous learning  
We should adopt continuous learning of:  
- Technical knowledge  
- Domain modeling skills  
- Domain specific knowhow  
  
## Knowledge-Rich Design  
Knowledge gained in a model can be:  
- Clarified  
- Fleshed out  
- Reconciled  
- Placed out of scope  
But will all contribute to a general understanding and help leverage knowledge in an application.  
Because the knowledge resides with domain experts, we can not assume the model. The model will grow  
from increasingly deeper understanding of the domain and what is significant.  
  
### Extract hidden concepts  
Making a domain particularity more prominent in the code:  
- Increases understanding of underlying concept by programmers  
- Makes code more intelligible by business experts  
  
## Ubiquitous language  
The domain model should be the backbone of a common language. It should not contain technical jargon.  
Domain experts should object to terms or structures that are awkward or inadequate.to convey domain understanding.  
Developers should watch for ambiguity or inconsistency that will trip up design.  
Using the model to communicate will force area's that aren't fleshed out or clear enough to the front.  
  
### One language  
We should not think there is a need for a separate language when talking to business specialists.  
They understand the domain well enough to deal with some level of abstraction.   
It is the use of one common language that ensures a deeper connection between the code and the domain.  
  
## Diagrams  
Diagrams should be a means of facilitating communication. Having a UML schema represent the whole program is not a model.  
Names we use can hint to a deeper complexity, but the diagrams complexity shouldn't distract from the conversation.  
We should explain complexity in text or talk about it and illustrate it with simple diagrams. The vital detail about  
the design should be captured and visible in the code, not the models.  
  
## Documents  
Documents should complement code and speech. The code should be the primary source of documentation and   
a 'document' should only be used where the complexity of the code could harm the understanding,  
much like with an all encompassing diagram.  
If documents are used they should be involved in project activities and reflect the ubiquitous language that is  
**currently** used. Illustrating documents with casual diagrams increases readability and generally helps   
understanding about decisions that were made.  
  
## Explanatory Model  
Unlike language there can be multiple models.  
- Model strictly containing bare necessities for development  
- Model containing more detail for educative purposes and conveying understanding  
The first will contain object-diagrams, where the second can make use of more illustrative representations  
and has the freedom to adopt more communicative styles.  
  
## Binding Model and Implementation  
- The design should map to the domain model for the model to add value  
- Mappings between model and design shouldn't be too complex, for it not to be too hard to understand and maintain  
- The model should work well as both analysis and as design    
We can manage this by revisiting the model and adjusting it where needed to reflect both design and domain analysis.    
Any technical person working on the model must spend some time touching code, likewise every developer must be involved  
in some level of discussion about the model and have contact with domain experts.  
  
## Isolating the Domain  
Separation of concerns between layers is important:  
- UI / DB and Services do not belong in business logic    
- Business logic does not belong in UI / DB or Services    
However, intricate connections within the system must be maintained.    
The software constructs of the 'domain layer' mirror the domain model, therefor they have no place in the other layers.  
  
## Layered Architecture vs Smart UI  
Not all projects are complex and not all teams master the more complex technologies and patterns to fully realize this  
separation of concerns, which has in itself quite some added complexity. Therefor, smart UI does have business logic embedded  
in the user interface, chopped up in small functions. In the context of domain driven development, we can see this as an  
anti-pattern. But this shows that in some cases a team might not benefit from domain driven development. But in general, when  
the domain is more complex, the smart UI approach will not be the right fit for long lived applications with growing complexity.    
Pros:  
- High productivity  
- Little skill required  
- Quick to adapt  
- Predictable time schedules  
- 4GL tools are efficient  
- Easy to 'redo' because of modularity    
Cons:  
- Difficult to integrate  
- A lot of duplication because of a lack of abstraction  
- Limit to rapid prototyping and iteration because of limited refactoring possibilities  
- No graceful path to richer behavior because complexity can bury us quickly  
  
  
  
## Hexagonal / Onion Architecture  
  
We can find an interesting article about the Hexagonal / Onion Domain Driven architecture  
[here](https://herbertograca.com/2017/11/16/explicit-architecture-01-ddd-hexagonal-onion-clean-cqrs-how-i-put-it-all-together/).   
  
---  
*Work in progress...*