# SemaJS
library/structure for single page applications
SemaJs doesn't support routing, for routing library please check SemaFeJS

Tiny but powerfull library as alternative for javascript framework.
Using ES6 with code generators to compile code pre run.

## Core
The core include the following

### App


### Model
Model repository for loaded models

### View
View Repositorty, creates and manage components.

### Request
Send/load data

### Evemt
Dispatch/subscribe events, one central points for all dom evetnts.
No need to add/remove most of the event listeners, 
they will be auto delegated to the view.

### Bindings
View to Model bindings created when the views are loaded,
removed when the views removed.
The bindings are string key based, no elements is used as refrence.
