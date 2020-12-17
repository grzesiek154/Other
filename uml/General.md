https://www.visual-paradigm.com/guide/uml-unified-modeling-language/what-is-use-case-diagram/

# **Use Case Diagram at a Glance

A standard form of use case diagram is defined in the Unified Modeling Language as shown in the Use Case Diagram example below:

![Use Case Diagram at a glance](https://cdn-images.visual-paradigm.com/guide/uml/what-is-use-case-diagram/02-use-case-diagram-annotated.png)

**Actor** 									

- Someone interacts with use case (system function).

- Named by noun.

- Actor plays a role in the business

- Similar to the concept of user, but a user can play different roles

- For example: 											

  - A prof. can be instructor and also researcher
  - plays 2 roles with two systems

- Actor triggers use case(s).

- Actor has a responsibility toward the system (inputs), and Actor has expectations from the system (outputs).

  

  **Use Case** 									

  - System function (process - automated or manual)
  - Named by verb + Noun (or Noun Phrase).
  - i.e. Do something
  - Each Actor must be linked to a use case, while some use cases may not be linked to actors.

**Boundary of system** 									

- The system boundary is potentially the entire system as defined in the requirements document.
- For large and complex systems, each module may be the system boundary.
- For example, for an ERP system for an organization, each of the modules such as personnel, payroll, accounting, etc.
- can form a system boundary for use cases specific to each of these business functions.
- The entire system can span all of these modules depicting the overall system boundary



**Include** 									

- When a use case is depicted as using the functionality of another use case, the relationship between the use cases is named as  include or uses relationship.
- A use case includes the functionality described in another use case as a part of its business process flow.
- A uses relationship from base use case to child use case  indicates that an instance of the base use case will include the  behavior as specified in the child use case.
- An include relationship is depicted with a directed arrow having a dotted line. The tip of arrowhead points to the child use case and the parent use case connected at the base of the arrow.
- The stereotype "<<include>>" identifies the relationship as an include relationship.

**Extends** 									

- Indicates that an **"Invalid Password"** use case may include (subject to specified in the extension) the behavior specified by base use case **"Login Account"**. 										
- Depict with a directed arrow having a dotted line. The  tip of arrowhead points to the base use case and the child use case is  connected at the base of the arrow.
- The stereotype "<<extends>>" identifies as an extend relationship

**Generalization** 									

- A generalization relationship is a parent-child relationship between use cases.
- The child use case is an enhancement of the parent use case.
- Generalization is shown as a directed arrow with a triangle arrowhead.
- The child use case is connected at the base of the arrow. The tip of the arrow is connected to the parent use case.

![Use Case Diagram Notation - Generalization](https://cdn-images.visual-paradigm.com/guide/uml/what-is-use-case-diagram/08-use-case-diagram-notation-generalization.png)

# Activity Diagram

https://www.visual-paradigm.com/guide/uml-unified-modeling-language/what-is-activity-diagram/

<img src="http://www.newthinktank.com/wp-content/uploads/2012/11/UML-Activity-Diagram.png" alt="http://www.newthinktank.com/wp-content/uploads/2012/11/UML-Activity-Diagram.png" style="zoom:150%;" />

# Sequence Diagram

[UML](https://en.wikipedia.org/wiki/Unified_Modeling_Language) Sequence Diagrams are interaction diagrams that detail how operations  are carried out. They capture the interaction between objects in the  context of a collaboration. Sequence Diagrams are time focus and they  show the order of the interaction visually by using the vertical axis of the diagram to represent time what messages are sent and when. 					



![http://www.newthinktank.com/wp-content/uploads/2012/11/Sequence-Diagram-Cheat-Sheet.png](http://www.newthinktank.com/wp-content/uploads/2012/11/Sequence-Diagram-Cheat-Sheet.png)

## Lifeline Notation

They represent the different objects or parts that interact with each other in the system during the sequence.

![Image for post](https://miro.medium.com/max/133/1*ryjy78MbaXI1cKAM9UPucw.png)

A lifeline with an entity element represents system data. For an  example, in a customer service application, the Customer entity would  manage all data related to a customer.

![Image for post](https://miro.medium.com/max/205/1*QkauAuzvTG_uPFl6cGf0CQ.png)

A lifeline with a boundary element indicates a system boundary/ software element in a system; for example, user interface screens, database  gateways or menus that users interact with, are boundaries.

![Image for post](https://miro.medium.com/max/189/1*hilJeAAvVHBNmTSBpeGkNw.png)

And a lifeline with a control element indicates a controlling entity or  manager. It organizes and schedules the interactions between the  boundaries and entities and serves as the mediator between them.

![Image for post](https://miro.medium.com/max/178/1*z3s3HK5PrVLGTNd5gKYS9Q.png)

## **Activation Bars**

![Image for post](https://miro.medium.com/max/721/1*ju5gQcxSFYrt9jqV4Jfg8g.png)

 The use of the activation bar on the lifelines of the Message Caller  (the object that sends the message) and the Message Receiver (the object that receives the message) indicates that both are active/is  instantiated during the exchange of the message. The length of the rectangle indicates the duration of the objects staying active.

## **Message Arrows**

An arrow from the Message Caller to the Message Receiver specifies a  message in a sequence diagram. A message can flow in any direction; from left to right, right to left or back to the Message Caller itself. 

![Image for post](https://miro.medium.com/max/338/1*rr8aZzYrs3Ef8sfO0XSDxg.png)

- *Synchronous message*

As shown in the activation bars example, a synchronous message is used  when the sender waits for the receiver to process the message and return before carrying on with another message. 

- *Asynchronous message*

An asynchronous message is used when the message caller does not wait for  the receiver to process the message and return before sending other  messages to other objects within the system.

![Image for post](https://miro.medium.com/max/704/1*6li6Q-foQ_2EfT3q-0Gp1w.png)

- *Return message*

A return message is used to indicate that the message receiver is done  processing the message and is returning control over to the message  caller. Return messages are optional notation pieces, for an activation  bar that is triggered by a **synchronous** message always implies a return  message.

