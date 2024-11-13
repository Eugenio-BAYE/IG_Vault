
# Frameworks

> [!important] Frameworks
> A **framework** is reusable *software* that implements
> a *generic solution to a generalized problem*.
>- It provides common facilities applicable to different application programs.
>- Principle: *applications* that do different, but related, things tend to have quite *similar designs*.
## Reusability

*Reuse* and *design for reusability* should be part of
the culture of software development organizations

> [!abstract]
> Types of reuse:
>- Reuse of expertise
>- Reuse of standard designs and algorithms
>- Reuse of libraries of classes or procedures
>- Reuse of powerful commands built into languages and operating systems
>- Reuse of frameworks
>- Reuse of complete applications

A framework is intrinsically *incomplete*:
- Some functionality is *optional*
- Developers use the *services* that the framework provides
- Certain *classes or methods* are used by the framework, but are *missing* (slots)
### Vicious cycle

> [!abstract] 
> Developers tend not develop high quality reusable components, so there is often little to reuse.

### Object-oriented Frameworks

In the *object oriented* paradigm, a framework is
composed of a *library of classes*.

> [!example]- Example:
>- A framework for payroll management
>- A framework for frequent buyer clubs
>- A framework for university registration
>- A framework for e-commerce web sites

A **horizontal framework** provides *general application* facilities that a large number of applications can use.

A **vertical framework** (application framework) is more ‘complete’ but still needs some slots to be filled to adapt it to specific application needs.
![[Design Principles - FIG1.png]]
### The Client-Server Architecture
> [!important] Client-Server Architecture (CSA)
> The **CSA** is a distributed system is a system in which:
>- Computations are performed by separate programs
>- Normally running on separate pieces of hardware
>- That co-operate to perform the task of the system.

**Server**: A program that provides a service for other programs that connect to it using a communication channel.

**Client**: A program that accesses a server (or several servers) to obtain services. A server may be accessed by many clients simultaneously

> [!abstract]- Sequence of activities in a client-server system
> 1. The server starts *running*
> 2. The server *waits* for *clients* to connect. (listening)
> 3. *Clients* start running and *perform operations*. Some operations involve requests to the server
> 4. When a *client* attempts to *connect*, the server accepts the connection (if it is willing)
> 5. The *server* waits for *messages* to arrive from *connected* *clients*
> 6. When a *message* from a client *arrives*, the server takes some action in *response*, then resumes *waiting*
> 7. Clients and servers continue functioning in this manner until they decide to shut down or *disconnect*

![[Design Principles - FIG2.png]]

> [!example]- Examples of client-server systems
>- The World Wide Web
>- Email
>- Network File System
>- Transaction Processing System
>- Remote Display System
>- Communication System
>- Database System

#### Alternatives to the Client-Server architecture
Have a *single program* on one computer that does
everything.

Have *no communication*.
- Each computer performs the work separately

Have some mechanism other than client-server
communication for *exchanging information*.
- E.G.: One program writes to a database; the other reads from the database

#### Advantages of Client-Server Architecture

- The *work* can be *distributed* among *different machines*
- The *clients* can access the *server’s functionality* from a distance
- The client and server can be *designed separately*
- They can both be *simpler*
- All the *data* can be *kept centrally* at the server
- Conversely, *data* can be *distributed* among many different geographically-distributed clients or servers
- The server can be accessed simultaneously by *many clients*
- *Competing clients* can be written to communicate with the same server, and vice-versa

Activities of the server :
> [!failure] 

Activities of the client :
> [!failure] 
> ... threads

#### Thin-client vs. fat-client systems

> [!important] Thin-client system (a)
>- Client is made as small as possible
>- Most of the work is done in the server.
>- Client easy to download over the network

> [!important] Fat-client system (b)
>- As much work as possible is delegated to the clients.
>- Server can handle more clients

![[Design Principles - FIG3.png]]

#### Communication protocols
The *messages* the *client* *sends* to the server form a *language*.

- The server has to be programmed to understand that language.

The *messages* the *server* *sends* to the client also form a *language*.
- The client has to be programmed to understand that language.

When a client and server are *communicating*, they are in effect having a *conversation* using these *two languages*.
The two *languages* and the *rules* of the conversation, taken together, are called the **communication protocol**

#### Tasks to perform to develop Client-Server Applications

Design :
- The primary *work* to be performed by *both client and server*.
- How the *work* will be *distributed*.
- The details of the set of *messages* that will be sent.
- The mechanism for :
	- Initializing
	- Handling connections
	- Sending and receiving messages
	- Terminating

#### Technology Needed to Build Client-Server Systems

Internet Protocol (*IP*)
- Route messages from one computer to another
- Long messages are normally split up into small pieces

Transmission Control Protocol (*TCP*)
- Handles connections between two computers
- Computers can then exchange many IP messages over a connection
- Assures that the messages have been satisfactorily received

A *host* has an IP address and a host name
- Several servers can run on the same host.
- Each server is identified by a port number (0 to 65535).
- To initiate communication with a server, a client must know both the host name and the port number

> [!failure]
> ... sending and receiving messages



### The Object Client-Server Framework (OCSF)
> 60% Of questions of the exam are about the OCSF and CSA


![[Design Principles - FIG4.png]]

#### Using OCSF
> [!warning] OCSF
> Software engineers using OCSF *never modify its three classes*
> They:
>- Create *subclasses* of the abstract classes in the framework
>- Call *public methods* that are provided by the framework
>- *Override* certain slot and hook methods (explicitly designed to be overridden)

### The Client Side
> [!failure]
> ... Using Abstract...

#### Internals of AbstractClient
Instance variables:
- A **Socket** which keeps all the *information*
about the connection to the server
- Two *streams*, an *ObjectOutputStream* and an *ObjectInputStream*
- A *Thread* that runs using AbstractClient’s run method
- Two variables storing the *host* and *port* of the server

### The Server Side
> [!failure] ... Internals...

#### Internals of AbstractServer and ConnectionToClient

### An Instant Messaging
> [!example] Application: SimpleChat
> Dessiner schema comme ça à l'examen :
> ![[Design Principles - FIG5.png]]
> ClientConsole can eventually be replaced by ClientGUI

> [!failure] compléter au dessus

# Design

> [!important] Design
> **Design** is a problem-solving process whose objective is  to find and describe a way :
>- To implement the system’s *functional requirements*
>- While respecting the *constraints* imposed by the quality, platform, and process requirement
>- And while adhering to general principles of *good quality*

> [!important] Design issues
> A designer is faced with a series of **design issues :**
>- These are *sub-problems* of the overall design problem.
>- Each issue normally has several *alternative solutions*:
>	- Design options
>- The designer makes a **design decision** to resolve each issue. This process involves choosing the best option from among the alternatives.

> [!failure]
## Design Principles

### Divide and conquer
### Increase cohesion when possible

A subsystem or module has high **cohesion** if it *keeps together* things that are related to each other, and keeps out other things :
- This makes the system as a whole easier to understand and change.
- Type of cohesion:
	- Functional, Layer, Communicational, Sequential,Procedural, Temporal, Utility

> [!important] Functional cohesion
> This is achieved when all the code that computes a particular result is *kept together*, and everything else is *kept out*.
> Benefits to the system:
>- Easier to understand
>- More reusable
>- Easier to replace
>
>Modules that *update a database, create a new file or interact with the user are not functionally cohesive*.

> [!example]
> When a module only performs a single computation, and returns a result, without having side-effects.

>[!failure]


> [!important] Utility Cohesion
> When related utilities which *cannot be logically placed in other cohesive* units are kept together.
>-  A utility is a procedure or class that has wide applicability to many different subsystems and is designed to be reusable.
>- For example, the `java.lang.Math` class.

### Reduce coupling where possible

**Coupling** occurs when there are *interdependencies* between one module and another.
- When *interdependencies* exist, changes in one place will require *changes* somewhere else.
- A network of interdependencies makes it hard to see at a glance how *some component works*.
- Type of coupling:
	- Content, Common, Control, Stamp, Data, Routine Call, Type use,Inclusion/Import, External

> [!example] Example
> Left *BAD* | Right *GOOD*
> ![[Design Principles - FIG6.png]]

---

> [!important] Content coupling
> Occurs when one component *secretly modifie*s data that is internal to *another component*.
>- To reduce content coupling you should therefore encapsulate all instance variables.
>	- declare them *private*
>	- and provide *get* and *set* methods
>- A worse form of content coupling occurs when you directly modify an instance variable of an instance variable.

> [!example] Example of content coupling
> ``` Java
> public class Line
{
private Point start, end;
…
public Point getStart() { return start; }
public Point getEnd() { return end; }
}
public class Arch
{
private Line baseline;
...
void slant(int newY)
{
Point theEnd = baseline.getEnd();
theEnd.setLocation(theEnd.getX(),newY);
}
}

--- 

> [!important] Common coupling
> Occurs whenever you use a *global variable* :
>- All the components using the global variable become coupled to each other.
>- A weaker form of common coupling is when a variable can be accessed by a subset of the system’s classes.
>	- e.g. a Java package
>- Can be acceptable for creating global variables that represent system-wide default values
>- The Singleton pattern provides encapsulated global access to an object.

> [!important] Control coupling
> Occurs when one procedure calls another using a ‘*flag*’ or ‘*command*’ that explicitly controls what the second procedure does.
>- To make a change you have to change both the calling and called method
>- The use of polymorphic operations is normally the best way to avoid control coupling
>- One way to reduce the control coupling could be to have a *look-up table*
>	- Commands are then mapped to a method that should be called when that command is issued.

> [!example] Example of content coupling
> ``` Java
> public routineX(String command)
{
if (command.equals("drawCircle"))
{
drawCircle();
}
else
{
drawRectangle();
}
}

> [!important] Stamp coupling:
> Occurs whenever one of your application classes is declared as the *type* of a method argument.
>- Since one class now uses the other, changing the system becomes harder.
>	- Reusing one class requires reusing the other
>- Two ways to reduce stamp coupling :
>	- using an interface as the argument type
>	- passing simple variables

> [!example] Example of stamp coupling
> ``` Java
> public class Emailer
> {
> public void sendEmail(Employee e, String text)
> {...}
> ...
> }
> ```
> Using simple data types to avoid it:
> ``` Java
> public class Emailer
> {
> public void sendEmail(String name, String email, String text)
> {...}
> ...
> }
> ```
> Using an interface to avoid it:
> ``` Java
> public interface Addressee
> {
> public abstract String getName();
> public abstract String getEmail();
> }
> public class Employee implements Addressee {…}
> public class Emailer
> {
> public void sendEmail(Addressee e, String text)
> {...}
> ...
> }

---

> [!important] Data coupling
> Occurs whenever the types of method arguments are either primitive or else simple library classes
>- The more arguments a method has, the higher the coupling
>	- All methods that use the method must pass all the arguments
>- You should reduce coupling by not giving methods unnecessary arguments
>- There is a trade-off between data coupling and stamp coupling.
>	- Increasing one often decreases the other

> [!important] Routine call coupling
> Occurs when one routine (or method in an object oriented system) calls another.
>- The routines are coupled because they depend on each other’s behaviour
>- Routine call coupling is always present in any system.
>- If you repetitively use a sequence of two or more methods to compute something
>	- then you can reduce routine call coupling by writing a single routine that encapsulates the sequence

> [!important] Type use coupling
> Occurs when a module uses a data type defined in another module
>- It occurs any time a class declares an instance variable or a local variable as having another class for its type.
>- The consequence of type use coupling is that if the type definition changes, then the users of the type may have to change
>- Always declare the type of a variable to be the most general possible class or interface that contains the required operations.

> [!important] Inclusion or import coupling
> Occurs when one component imports a package or when one component includes another.
>- The including or importing component is now exposed to everything in the included or imported component.
>- If the included/imported component changes something or adds something.
>	- This may raises a conflict with something in the includer, forcing the includer to change.
>- An item in an imported component might have the same name as something you have already defined.

> [!important] External coupling
> When a module has a dependency on such things as the operating system, shared libraries or the hardware.
>- It is best to reduce the number of places in the code where such dependencies exist.
>- The Façade design pattern can reduce external coupling.

### Keep the level of abstraction as high as possible

Ensure that your designs allow you to *hide or defer consideration of details*, thus reducing *complexity*.
- A good abstraction is said to provide *information hiding*
- Abstractions allow you to understand the  essence of a subsystem without having to know unnecessary details.

> [!tip] Abstraction and classes
> **Classes** are data *abstractions* that contain procedural abstractions.
>- Abstraction is increased by defining all variables as private.
>- The fewer public methods in a class, the better the abstraction.
>- Superclasses and interfaces increase the level of abstraction.
>- Attributes and associations are also data abstractions.
>- Methods are procedural abstractions.
>	- Better abstractions are achieved by giving methods fewer parameters

### Increase reusability where possible
Design the various aspects of your system so that they can be used again in other contexts.
- Generalize your design as much as possible
- Follow the preceding three design principles
- Design your system to contain hooks
- Simplify your design as much as possible

### Reuse existing designs and code where possible

Design with reuse is complementary to design for reusability
- Actively reusing designs or code allows you to take advantage of the investment you or others have made in reusable components.
	- Cloning should not be seen as a form of reuse

### Design for flexibility
Actively anticipate changes that a design may have to undergo in the future, and prepare for them.
- Reduce coupling and increase cohesion
- Create abstractions
- Do not hard-code anything
- Leave all options open
	- Do not restrict the options of people who have to modify the system later
- Use reusable code and make code reusable


### Anticipate obsolescence
Plan for changes in the technology or environment so the software will continue to run or can be easily changed.
- Avoid using early releases of technology
- Avoid using software libraries that are specific to particular environments
- Avoid using undocumented features or little-used features of software libraries
- Avoid using software or special hardware from companies that are less likely to provide long
- Use standard languages and technologies that are supported by multiple vendors


### Design for Portability
Have the software run on as many platforms as possible
- Avoid the use of facilities that are specific to one particular environment
- E.g. a library only available in Microsoft Windows


### Design for Testability
Take steps to make testing easier.
- Design a program to automatically test the software :
	- Ensure that all the functionality of the code can by driven by an external program, bypassing a graphical user interface
- In Java, you can create a main() method in each class in order to exercise the other methods.

### Design defensively
Never trust how others will try to use a component you are designing.
- Handle all cases where other code might attempt to use your component inappropriately
- Check that all of the inputs to your component are valid: the preconditions.
	- Unfortunately, over-zealous defensive design can result in unnecessarily repetitive checking

### Design by contract
A technique that allows you to design defensively in an efficient and systematic way.
- Each method has an explicit contract with its callers
- The contract has a set of assertions that state:
	- What preconditions the called method requires to be true when it starts executing
	- What postconditions the called method agrees to ensure are true when it finishes executing
	- What invariants the called method agrees will not change as it executes

> [!abstract] Techniques for making good design decisions
> Using priorities and objectives to decide among alternatives
>- 1) List and describe the alternatives for the design decision.
>- 2) List the advantages and disadvantages of each alternative with respect to your objectives and priorities.
>- 3) Determine whether any of the alternatives prevents you from meeting one or more of the objectives.
>- 4) Choose the alternative that helps you to best meet your objectives.
>- 5) Adjust priorities for subsequent decision making.

> [!example] Example priorities and objectives
> Imagine a system has the following objectives, starting with top priority:
> - Security: Encryption must not be breakable within 100 hours of computing time on a 400Mhz Intel processor, using known cryptanalysis techniques.
> - Maintainability: No specific objective.
> - CPU efficiency. Must respond to the user within one second when running on a 400MHz Intel processor.
> - Network bandwidth efficiency: Must not require transmission of more than 8KB of data per transaction.
> - Memory efficiency. Must not consume over 20MB of RAM.
> - Portability. Must be able to run on Windows 98, NT and XP as well as Linux
> 
> Example evaluation of alternatives
> ![[Design Principles - FIG7.png]]

> Bonne présentation pour d'autres projets pour la décision de technologies ou algorithmes
### Using cost-benefit analysis to choose among alternatives

To estimate the *costs*, add up:
- The *incremental cost* of doing the software engineering work, including ongoing *maintenance*.
- The incremental costs of any *development technology required*
- The incremental costs that *end-users* and product *support personnel* will experience.

To estimate the *benefits*, add up:
- The incremental software engineering *time* saved
- The incremental benefits measured in terms of either increased *sales* or else *financial* benefit to users

## Architecture

### Software Architecture
> [!important] SA
> **Software architecture** is process of designing the global *organization* of a software system, including:
>- *Dividing* software into *subsystems*.
>- Deciding how these will *interact*.
>- Determining their *interfaces* :
>	- The architecture is the core of the design, so all  software engineers need to *understand* it.
>	- The architecture will often constrain the overall *efficiency*, *reusability* and *maintainability* of the system.


> [!failure] mettre en ###


> [!tip] The importance of Software Architecture :
> Why you need to develop an architectural model:
> - To enable everyone to better understand the system
> - To allow people to work on individual pieces of the system in isolation
> - To prepare for extension of the system
> - To facilitate reuse and reusability

### Contents of a good architectural model
A system’s architecture will often be expressed in terms of several different *view*.
- The logical breakdown into subsystems
- The interfaces among the subsystems
- The dynamics of the interaction among components at run time
- The data that will be shared among the subsystems
- The components that will exist at run time, and the machines or devices on which they will be located

### Design stable architecture
To ensure the maintainability and reliability of a system, an architectural model must be designed to be stable
- Being stable means that the new features can be easily added with only small changes to the architecture


### Developing an architectural model
Start by sketching an outline of the architecture :
- Based on the principal requirements and use cases
- Determine the main components that will be needed
- Choose among the various architectural patterns
- ***Suggestion***: have several different teams independently develop a first draft of the architecture and merge together the best ideas

Refine the architecture :
- Identify the main ways in which the components will interact and the interfaces between them
- Decide how each piece of data and functionality will be distributed among the various components
- Determine if you can re-use an existing framework, if you can build a framework

Consider each use case and adjust the architecture to make it realizable
Mature the architecture

### Describing an architecture using UML

All UML diagrams can be useful to describe aspects of the architectural model
Four UML diagrams are particularly suitable for architecture modelling:
- Package diagrams
- Subsystem diagrams
- Component diagrams
- Deployment diagrams

> [!tip] Package diagrams
> ![[Design Principles - FIG8.png]]

> [!tip] Component diagrams
> ![[Design Principles - FIG9.png]]

> [!tip] Deployment diagrams
> ![[Design Principles - FIG10.png]]

> [!tip] Subsystem Missing ?
> > [!failure]


### Architectural Patterns
The notion of patterns can be applied to software architecture.
- These are called architectural patterns or architectural styles.
- Each allows you to design flexible systems using components.
	- The components are as independent of each other as possible.

### The Multi-Layer architectural pattern
In a layered system, each layer communicates only with the layer immediately below it.
- Each layer has a well-defined interface used by the layer immediately above.
	- The higher layer sees the lower layer as a set of  services.
- A complex system can be built by superposing layers at increasing levels of abstraction.
	- It is important to have a separate layer for the UI.
	- Layers immediately below the UI layer provide the application functions determined by the use
	- Bottom layers provide general services.

> [!example] Multi-Layer Systems
> ![[Design Principles - FIG11.png]]

> [!important] The multi-layer architecture and design principles
>- 1) Divide and conquer: The layers can be independently designed.
>- 2) Increase cohesion: Well-designed layers have layer cohesion.
>- 3) Reduce coupling: Well-designed lower layers do not know about the higher layers and the only connection between layers is through the API.
>- 4) Increase abstraction: you do not need to know the details of how the lower layers are implemented.
>- 5) Increase reusability: The lower layers can often be designed generically.
>- 6) Increase reuse: You can often reuse layers built by others that provide the services you need.
>- 7) Increase flexibility: you can add new facilities built on lower-level services, or replace higher-level layers.
>- 8) Anticipate obsolescence: By isolating components in separate layers, the system becomes more resistant to obsolescence.
>- 9) Design for portability: All the dependent facilities can be isolated in one of the lower layers.
>- 10) Design for testability: Layers can be tested independently.
>- 11) Design defensively: The APIs of layers are natural places to build in rigorous assertion-checking.

### The Client-Server and other distributed architectural patterns

- There is at least one component that has the role of server, waiting for and then handling connections.
- There is at least one component that has the role of client, initiating connections in order to obtain some service.
- A further extension is the Peer-to-Peer pattern.
	- A system composed of various software components that are distributed over several hosts.

> [!example] An example of a distributed system
> ![[Design Principles - FIG 12.png]]


### The distributed architecture and design principles

- Divide and conquer: Dividing the system into client and server processes is a strong way to divide the system.
- Increase cohesion: The server can provide a cohesive service to clients.
- Reduce coupling: There is usually only one communication channel exchanging simple messages.
- Increase abstraction: Separate distributed components are often good abstractions.
- Increase reuse: It is often possible to find suitable frameworks on which to build good distributed systems.
	- However, client-server systems are often very application specific.
- Design for flexibility: Distributed systems can often be  easily reconfigured by adding extra servers or clients.
- Design for portability: You can write clients for new platforms without having to port the server.
- Design for testability: You can test clients and servers independently.
- Design defensively: You can put rigorous checks in the message handling code.

### The Broker architectural pattern
Transparently distribute aspects of the software system to different nodes.
- An object can call methods of another object without knowing that this object is remotely located.
- CORBA is a well-known open standard that allows you to build this kind of architecture.
![[Design Principles - FIG12.png]]

- Divide and conquer: The remote objects can be independently designed.
- Increase reusability: It is often possible to design the remote objects so that other systems can use them too.
- Increase reuse: You may be able to reuse remote objects that others have created.
- Design for flexibility: The brokers can be updated as required, or the proxy can communicate with a different remote object.
- Design for portability: You can write clients for new platforms while still accessing brokers and remote objects on other platforms.
- Design defensively: You can provide careful assertion checking in the remote objects.
### The Transaction-Processing architectural pattern

A process reads a series of inputs one by one.
- Each input describes a transaction – a command that typically some change to the data stored by the system
- There is a transaction dispatcher component that decides what to do with each transaction
- This dispatches a procedure call or message to one of a series of component that will handle the transaction

> [!example] Example of a transaction-processing system
> ![[Design Principles - FIG13.png]]
> 

