# Moose

## Why
* Unidirectional rendering frameworks have given developers the ability to modularise code bases. 
* The prevailing methodology seems to be small dumb components and large smart components.
* This split is too naive and in practice it doesn't create a meaningful abstraction. Codebases end 
up with a tiny amount of small reusable 'dumb' components and a large amount of monolithic 
application specific 'smart' components.

What the front-end really needs is a way to talk about interfaces that effectively separates its concerns. 

## Core Ideas
At its core Moose aims to provide clear descriptions of the parts that make up a client-side application.
If we can describe these parts correctly it becomes easy to label and categorise the distinct parts 
of our apps. Once categorised, code structure and responsibility becomes much easier to organize.


The client side code has five clear areas of concern:

* Data fetching and storage
* Application logic
* User Interaction Logic
* Positional Styles (Layout)
* Aesthetic Styles (Component Styles)


### Data Fetching
This concern describes how data is fetched from exterior sources and where it is stored once it 
arrives. Your views do not care where the data came from or how it is stored. They just need to know
when it is safe to render. This concern should be separated from the other parts of your app. 

### Application Logic
Often confused with business logic. Application logic is the specific ways that your data structures
are applied to your interfaces. Taking a collection of users and applying them to a table component
is Application logic. In a unique location you have decided that these users are best displayed as 
a table and this is how you transform the data into the shape a table requires. This concern should 
be separated from the other parts of your app.

### User Interaction Logic
Distinct to application logic, interaction logic deals with how a user interacts with parts of the site.
When a user types in a search box and a list of possible choices appears, that is interaction logic.
Some part of the app is concerned with what the user has typed and what possible choices it could show
in response. It is a separate concern from application logic because it doesn't care what data it is 
given or where it came from, just how that data should respond to the users interaction. This concern
should be separate from other parts of you app.

## Aesthetic Styles
Aesthetic styles describe how your individual components should look. Libraries and methodologies,
like Bootstrap, Atomic Design etc. have got this right. You can describe all possible states of a 
button quite clearly and all the code required to define how a button looks should be separate from 
other parts of your app.

## Positional Styles
Positional styles describe how the different parts of your app relate to each other in position. 
Grids, floats, text spacing all fall under this category. Component libraries often become bloated 
and confused when positional styles are combined with aesthetic ones. Class names like 
`.marginLeftLarge` and `paddingTopExtraSmall` become littered throughout the app, making things hard 
to move and refactor. Positional styles are a unique concern and should be separate for other parts 
of you app.


## Application / Interaction
Broadly speaking you can split these five areas of concern into two main categories. Application and 
Interaction. Application is concerned with data and how it is stored and transformed to be rendered.
Interaction is concerned with how things look and feel and how the user interacts with them.



# Moose Terms
With these areas of concern in place we can now start to talk about how Moose solves these problems.



## Affordance
Affordances are the lowest and most abstract parts of an application. They let the user interact in
some way, but only in the most general sense. By themselves they are useless, but when given some
business logic they become useful.

### Example
A button affords the user to click. The component should describe how best to do that. I.e a click-handler
some text and some button-like styles. But it cant describe what that click should perform. 
A callback and a label must be provided to the button before it makes sense.

### Rules
Affordances can contain interaction logic and aesthetic styles. 
Affordances cannot contain application logic or data fetching. 
Affordances in themselves can contain some layout styles. But they cannot control the layout of their 
surrounds.
Affordances must be declared in their own file. They cannot be declared ad-hoc.


## Appliance
An appliance is an affordance bound to data or application logic. A button by itself is just an
affordance but a button with a "Save" label and callback that triggers the save API is an appliance.

A save button inherits all the general affordances given by button (clicking, and a label). But now 
it performs a specific purpose. We can distinguish a save button from a delete button from a log out
button. Each is its own unique appliance. 

### Example

### Rules
Appliances can contain one or many affordances.
Appliances cannot fetch data.
Appliances can be in its own file.
Appliance can be declared ad-hoc in a structure.


## Structure
## Layout
## View





## Hierarchy

1. Views - Data fetching and storage
2. Structures, Appliances - Application Logic
3. Layout - Positional Styling
4. Affordances - User Interaction Logic, Aesthetic Styling


Views have a structure
Structures have a layout & some appliances
Appliances have an affordance
Affordances have a aesthetic styles

