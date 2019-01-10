# Mobile HCI
### Lecture 2 - Android
---

### Software Components
An android app is made of several components:

### Activity

A visual UI for **one focussed task**. Seperate activities work together to form a **cohesive** user interface, but each **independant** of the others.

An activity is a subclass of the **Activity** class in the SDK. 

Typically, one activity is presented to the user first when the application is launched. **Moving to another activity** is done from the *current activity*. 

Normally an activity fills the screen, but it may be smaller and float ontop of another one. 
##### Activity Lifecycle:

An activity has three states:

1. *Active or Running* when it is at the foreground (top of activity stack). Focus of the user's actions
2. *Paused* if it has lost user focus but is still visible to the user (activity floating on top of it). Some of the paused screen must still be seen.
3. *Stopped* if it has been completely obscured by another activity. Can still retain state and member information

##### Fragments:

A part of a user interface. One activity can have several fragments side-by-side if there is sufficient space. Often used for, lists of items (list of emails etc.)

---

### Intents

A messaging object for **communicating** between components (Activities, Service, etc). An intent asks the OS to perform an action - E.g. starting a next activity.

Intent Filters:

An intent can explicitly name a target component. 

If a target is not explicitly named, Android must find the best component to respond to the intent. 

- It does so by comparing the intent object to the *intent filters* of potential targets.
- A component intent filter informs Android of the kind of intents the component is able to handle.
- These are declared in the manifest file
---

### Services

For **persistent background tasks**. They will always run in the background, even if switching apps. 

Services dont have an Activity, but Activities can interact with them. 

> Music players use a service to play music and different Activities can send commands (e.g. to play and pause)

---

### Broadcast Reviews

- Recieves Broadcasts from other applications.
    - E.g. low battery, incoming call etc.
- Allows appropriate response to system events
    - E.g. stop video if battery low, pause game if call incoming etc.
- Applications can also send broadcasts
    - E.g. to let other applications know that some data has been downloaded and is available
- Do not display a user interface
    - However they may start an activity in response to information they recieve

---

### Content providers

These share an applications persistent data with other applications, data might be in a database or the cloud. 

Content providers extend the **ContentProvider** class. To implement a standard set of methods so other applications can access and edit its data.

Applications do not call these methods directly. They use a **content resolver** object instead. 
---

### The manifest file

Android can only use components it knows about. 

- Apps declared their components in a **manifest file**.
- Tells Android about the applications components
    - Activities, Services, Broadcast Receivers etc.
- It names any libaries the application needs to be linked against and identifies any permissions the application expects to be granted.

---

### Core Compomnents Summary

**Activity**: Task user interfaces
**Service**: background operations
**Broadcast Receiver**: recieve event notifications from other apps
**ContentProvider**: manage access to persistent data storage
**Intent**: for communication between application components

---
### Android UI

Basic Concepts:
- **View**: Higher UI elements that can be drawn
- **View Group**: a composite view
- **Intent**: Represents an intention to do some work. Used to invoke system services.
- **Content Provider**: store and retrieve data and make it accessible to all applications
- **Service**: Background processes

##### XML Layout Files:

The layout is the architecture for the user interface in an Activity. It defines the **layout structure** and holds all the elements that appear. It is defined in an **XML Layout File**.

Layout Options:
- Linear
- Relative
- Table
- Grid
- Frame

Views are a point of **interaction** for the user. You define the UI by using a heirarchy of View and ViewGroup nodes. Your activity must call setContentView() to render UI elements on the screen. 

A **widget** is a View object that serves as an interface for interaction with the user. Android provides a set of fully implemented widgets, like buttons, checkboxes and text-entry fields. (Certain high level components exist such as adding a Map or a Video, do this just like a button!).

**Fragments** represent a *behaviour* or *a portion* of a user interface in an Activity. You can define multiple fragments in a single activity, to build a multi-pane UI. Fragments can be resued in different activities. They support **dynamic** and **flexible UI designs** on *larger screens* such as tablets.






