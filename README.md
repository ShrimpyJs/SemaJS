# SemaJS
library/structure for single page applications.

Created to remove the need to used large libraries like React, angular for small to large project.

SemaJs doesn't support routing, for routing library please check SemaFeJS

Tiny but powerfull library as alternative for javascript framework.
Using ES6 with code generators to compile code pre run.

```
Approx 10k uncompiled.
```

## View Model
All content of the page comes in a form of view/model.

A model can have one or more views.

When a model is loaded it will automatically update all his views.

When a view is loaded it will get be added the model to create a view/component.

```
{
   "models": [{
      "key": "HW",
      "value": "Hello World"
   }],
   "views": [{
      "modelKey": "HW",
      "containerId": "content",
      "component": "TextDisplay"
   }]
}
```


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
See below for example in the Build section.

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

## Build
Before a project is compoiles, a node build runs and does the following.

### Componentss
Find all the components create under the 'conponents' folder and builds compoent factory
```
components.generated.js
```

```
module.exports = {
   get: get
};

const components = {
    HelloWorld: require('../components/HelloWorld/main.js'),
};

function get(type) {
   if (components[type] == null) {
      console.log('component not found for ', type);
   }

   return components[type];
}
```

### Style
compile all the scss files into one and creates
```
style.generated.scss
style.generated.css
```

### Templates
Convert all the html template files into generated js files
```
template.html -> template.generated.js

<div id="${view.id}">${model.value}</div>

to 

module.exports = {
   create
};

function create(view, model) {
   return `<div id="${view.id}">${model.value}</div>`;
}
```

### Preview
All components are displayed in an html table generated from
the html temlpate and the stub.js for quick preview.




