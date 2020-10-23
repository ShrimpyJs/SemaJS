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

### Event
Dispatch/subscribe events, one central points for all dom evetnts.
No need to add/remove most of the event listeners, 
they will be auto delegated to the view.

### Bindings
View to Model bindings created when the views are loaded,
removed when the views removed.
The bindings are string key based, no elements is used as refrence.

## Componetns
The components are bounded the same inteface:

```
module.exports = {
   create,
   init,
   render,
   onEvent.
   onDocumentEvent,
   onWindowsEvent,
   distroy
};
```
The only mandatory method is create.

### Structure

All componets has the same structure

```
main.js
style.scss
template.html
```
Once the build is run, template.generated will be added,
the tempalte can use ES6 string literals that will be auto replaces with the model.
```
module.exports = {
   create
};

function create(view, model) {
   return `<div id="${view.id}">${model.value}</div>`;
}
```
When running Jest in Webpack the followig files can be used
```
spec.js
stub.josn
```
Test could be comparing the template result
```
const main = require('./main');
const stub =  require('./stub');

describe("Hello world test", () => {
  test("html template", () => {
    const result = main.create(stub.view, stub.model);
    const expected ="<div>Hello World</div>";
    
    expect(result).toEqual(expected);
  });
});
```




