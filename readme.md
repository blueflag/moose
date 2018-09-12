# Moose

## Why
* Unidirectional rendering frameworks have given developers the ability to modularise code bases. 
* The prevailing methodology seems to be small dumb components and large smart components.
* This split is too naive and in practice it doesn't create a meaningful abstraction. Codebases end 
up with a tiny amount of small reusable 'dumb' components and a large amount of monolithic 
application specific 'smart' components.

What the front-end really needs is a way to talk about interfaces that effectively separates its concerns. 

## Core Ideas
Moose aims to provide clear descriptions of the parts that make up a client-side application.
If we can describe these parts correctly it becomes easy to label and categorise the areas of our 
apps. Once categorised, code structure and responsibility becomes much easier define.

## Clientside Concerns
The client side code has six clear areas of concern:

* Data fetching
* Data Storage
* Application logic
* User Interaction Logic
* Positional Styles (Layout)
* Aesthetic Styles (Component Styles)

_Broadly speaking you can split these five areas of concern into two main categories. Application and 
Interaction. Application is concerned with data and how it is stored and transformed to be rendered.
Interaction is concerned with how things look and feel and how the user interacts with them._


### Data Fetching
This concern describes how data is fetched from exterior sources and where it is stored once it 
arrives. Your views do not care where the data came from or how it is stored. They just need to know
when it is safe to render. This concern should be separated from the other parts of your app. 

### Data Storage
Often labelled as state management, this concern describes how data fetched from API's is stored 
in memory throughout your app.

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

### Aesthetic Styles
Aesthetic styles describe how your individual components should look. Libraries and methodologies,
like Bootstrap, Atomic Design etc. have got this right. You can describe all possible states of a 
button quite clearly and all the code required to define how a button looks should be separate from 
other parts of your app.

### Positional Styles
Positional styles describe how the different parts of your app relate to each other in position. 
Grids, floats, text spacing all fall under this category. Component libraries often become bloated 
and confused when positional styles are combined with aesthetic ones. Class names like 
`.marginLeftLarge` and `paddingTopExtraSmall` become littered throughout the app, making things hard 
to move and refactor. Positional styles are a unique concern and should be separate for other parts 
of you app.



# Moose Terms
With these areas of concern in place we can now start to talk about how Moose categorises them.
Moose starts from the lowest most general concerns and works it's way up to the higher and more specific.

## Affordance
An affordance is a component that affords the user a single action.

* Text affords the user reading
* Button affords the user clicking
* Input affords the user typing

They are the lowest and most abstract parts of an application. They let the user interact in
some way, but only in the most general sense. By themselves they are useless, but when given some
business logic they become useful. Affordances are similar in this respect to 'dumb' components: 
They are small and single purpose. Affordances differ from dumb components in that they must be 
general. A save button is not an affordance, but a button is. A friend list is not an affordance but
a user list is.

### Example
A button affords the user to click. The button affordance should describe how best to do that. 
i.e. a click-handler, some text, and some button-like styles. Importantly the button cant describe 
what that click should perform. A specific callback and label must be provided to the button before 
it makes sense.


### Rules
* Affordances can contain interaction logic
* Affordances can contain aesthetic styles. 
* Affordances can contain layout styles. But only the to control internal positioning, they cannot
influence surrounding components.
* Affordances can contain other affordances.
* Affordances cannot contain application logic.
* Affordances cannot contain data fetching. 
* Affordances must only have one concern.
* Affordances must be declared in their own file; they cannot be declared ad-hoc.



## Appliance
An appliance is an affordance bound to data or application logic. A button by itself is just an
affordance but a button with a "Save" label and callback that triggers the save API is an appliance.

A save button inherits all the general affordances given by button (clicking, and a label). But now 
it performs a specific purpose. We can distinguish a save button from a delete button from a log out
button. Each is its own unique appliance. 

### Example

### Rules
* Appliances can contain one or many affordances.
* Appliances can be in its own file.
* Appliances can be declared ad-hoc in a structure.
* Appliances cannot fetch data.



## Layout
### Example
### Rules
* Layouts can contain positional affordances
* Layouts can perform a null check before rendering an element
* Layouts cannot contain aesthetic affordances
* Layouts cannot declare aesthetic styles
* Layouts cannot contain interaction logic
* Layouts cannot contain application logic



## Structure
Structures bind data and application logic to affordances and layouts. In the process creating 
appliances. Appliances can be created ad-hoc in the structures or if common they can be moved out 
to their own file.

Structures are the glue between your specific data and your general affordances.
Structure are where your application logic is realised. 

### Example
If you take a list of coffee shops and bind them to a table affordance, placing it in the body of a
profile layout. You have started to create the application logic of the coffee shop profile page by
creating a coffee shop table appliance and placing the body of the page.

### Rules
* Structures can declare ad-hoc appliances
* Structures cannot fetch data
* Structures cannot store data
* Structures cannot contain interaction logic



## View
Views bind data to your structures. They orchestrate what data is fetched, and when it returns they 
provide it to the structure. The structure defines an api for what data it requires to render 
correctly. It is up to the view to make sure that data is given to it. 

### Example
Our coffee shop profile page structure needs data before it can render. It needs a list of coffee 
shops, information on the state of the request. The coffee shop
profile view should then fetch the required list of coffee shops and pass them to the view.

### Rules
* Views can contain data fetching code.
* Views are specific
* Views can have a one to one relationship to a structure
* Views don't have to be a component. (Hoc chain)




## Hierarchy

1. Views - Data fetching and storage
2. Structures, Appliances - Application Logic
3. Layout - Positional Styling
4. Affordances - User Interaction Logic, Aesthetic Styling


Views have a structure
Structures have a layout & some appliances
Appliances have an affordance
Affordances have a aesthetic styles

