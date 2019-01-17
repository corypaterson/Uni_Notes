# Mobile HCI
### Lecture 3 - Android Building Blocks
---

### Navigation Patterns

>Navigation: The act of moving between screens to complete tasks. 

Several types of **navigation**:
- **Lateral** navigation 
    - Moving between screens at the same level of hierarchy.
    - E.g. tabs, navigation drawer, button bars etc
- **Forward** navigation
    - Moving between screens at consecutive levels of hierarchy, steps in a flow or across an app
    - E.g. lists, image lists/grids, cards etc
- **Reverse** navigation
    - Moving backwards through screens either chronologically or hierachically.
    - E.g. back buttons

---

### Navigation Components

##### Navigation Drawer:
A hidden drawer on the left of the screen, expands to reveal destinations in your app. This supports **lateral** navigation.

##### Tabs:

Tabs **organise** and allow **lateral navigation** between groups of content that are related. Each tab should contain distinct content.

> Tab bars are **not** *tool bars*, tab bar has items to navigate to while tool bars have actions for the current screen.

---

### Lists, Grids and Carousels

##### Lists:

A continous group of text or images, with associated actions. Supports **forwards navigation**. Select an item from the list to go deeper into the hierarchy.

Has a:

- **section divider**, organises content of the list into groups to facilitate scanning.
- **Line items**, items that are displayed in the list, can be a wide range of data types.

##### Grid Lists: 

A collection of images/cards in an **organized grid**. It is scrollable and supports **forward navigation**. Ordered lists can be indexed for faster scrolling (contact list a-z).

##### Search bar: 

A core feature, supports **forward navigation**. Users should be able to search any data that is available to them (device or internet). 

---

### UI Components

##### Buttons:

Communicate actions that a user can take. Perform action by tapping the button. Different appearance indicates realtive importance.

##### Floating Action Buttons:

Performs the **primary action** of an activity. They float **above** content. Effective with just one or less uses per activity.

##### Text Fields:

Allows the user to enter text. Can be single or multiline compatible. The **field type** determines which keyboard layout should be used (email, phone number etc). 

##### Seek bars and Sliders:

Sliders allow users to make selections from a range of values. The can be **continuous** or **discrete**. They are interactive, so well suited to real-time feedback.

##### Selection Controls:

Allows users to make selections:

- Checkboxes - select many from a set
- Radio buttons - select one from a set
- Switches - toggle state, binary choice

##### Dialogs:

A modal window that appears in front of content to provide critical info or to ask for a decision. App functionality is **disabled** when they appear. They are **purposefully intteruptive** (use sparingly).

##### Pickers:

A simple way to select a single value from a set. Can swipe through the picker values. E.g. Clock alarm picker, date picker etc.

##### Spinners:

A dropdown menu for making a simple selection. Used in forms for data input. Can be combined with other UI elements.

##### Menus:

Like spinners but not linked to a particular field. E.g. action bar menus, context menus for selected text.

---

### Giving Feedback

##### Progress Indicators

- **linear** progress - horizontal bar
- **Circular** progress - circular bar
- **Determinate** - progress is unknown 
- **Indeterminate** - end point unknown or unpredictable

##### Snack bars:

Provide **brief messages** about app operations at the bottom of the user interface. Can have buttons embedded. Can disappear automatically or wait until dismissed.

##### Toasts:

Provide **lightweight feedback** about an operation and disappear automatically after a short time.




