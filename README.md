cytoscape.js-undo-redo
================================================================================


## Description
 This extension represents an interface to control actions on Cytoscape.js graph and also provides 
 built-in functionalities for common cytoscape.js operations like dragging nodes, adding/removing new node et al.



## API

```javascript
    var cy = cytoscape({...});

    var ur = cy.undoRedo(options);

```


`ur.action( actionName, actionFunction, undoFunction)`
Register action with its undo function & action name.

`ur.do(actionName, args)`
Calls registered function with action name actionName via actionFunction(args)

`ur.undo()`
Undo last action

`ur.redo()`
Redo last action

`cy.on("undo", function(actionName, args){} )`
Calls registered function with action name actionName via actionFunction(args)

`cy.on("redo", function(actionName, args){} )`
Calls registered function with action name actionName via actionFunction(args)
*Note that args are returned from opposite action like (undo => redo || redo => undo)

`ur.isUndoStackEmpty()`
Get whether undo stack is empty (namely is undoable)

`ur.isRedoStackEmpty()`
Get whether undo stack is empty (namely is redoable)

`ur.getUndoStack()`
Gets actions (with their args) in undo stack

`ur.getRedoStack()`
Gets actions (with their args) in redo stack


## Default Options
```javascript
      var options = {
            isDebug: false, // Debug mode for console messages
            actions: {},// actions to be added
            undoableDrag: true, // Whether dragging nodes are undoable
            keyboardShortcuts: {
                ctrl_z: true, // undo
                ctrl_y: true, // redo
                ctrl_shift_z: false // redo
            },
            beforeUndo: function () { // callback before undo is triggered.

            },
            afterUndo: function () { // callback after undo is triggered.

            },
            beforeRedo: function () { // callback before redo is triggered.

            },
            afterRedo: function () { // callback after redo is triggered.

            },
            ready: function () {

            }
        }
        
       var ur = cy.undoRedo(options); // Can also be set whenever wanted.
```

## Default Actions (Undoable/Redoable)
 * Default actions can be run by the same way like `ur.do("remove", "#spec")`
 * Undoable dragging can be disabled through options `undoableDrag: false`
 
 `.do("add", eleObj)` http://js.cytoscape.org/#cy.add
 
 `.do("remove", eles/selector)` http://js.cytoscape.org/#cy.remove
 
 `.do("layout", options)` http://js.cytoscape.org/#core/layout
 
 * Following actions take argument(s) instead of extending
 
 `.do("restore", eles/selector)` http://js.cytoscape.org/#eles.restore
 
 `.do("clone", eles/selector)` http://js.cytoscape.org/#eles.restore
 
 `.do("select", eles/selector)` http://js.cytoscape.org/#eles.select
 
 `.do("unselect", eles/selector)` http://js.cytoscape.org/#eles.unselect
 
 `.do("move", arg)` http://js.cytoscape.org/#eles.move 
 
 ```javascript
    var arg = {
        eles: ... // eles/selector
        location: ... // as is in docs
        }
 ```


## Dependencies

 * Cytoscape.js ^1.5.0
 
 

## Usage instructions

Download the library:
 * via npm: `npm install cytoscape.js-undo-redo`,
 * via bower: `bower install cytoscape.js-undo-redo`, or
 * via direct download in the repository (probably from a tag).

`require()` the library as appropriate for your project:

CommonJS:
```js
var cytoscape = require('cytoscape');
var undoRedo = require('cytoscape.js-undo-redo');

undoRedo( cytoscape ); // register extension
```

AMD:
```js
require(['cytoscape', 'cytoscape.js-undo-redo'], function( cytoscape, undoRedo ){
  undoRedo( cytoscape ); // register extension
});
```

Plain HTML/JS has the extension registered for you automatically, because no `require()` is needed.



## Publishing instructions

This project is set up to automatically be published to npm and bower.  To publish:

1. Set the version number environment variable: `export VERSION=1.2.3`
1. Publish: `gulp publish`
1. If publishing to bower for the first time, you'll need to run `bower register cytoscape.js-undo-redo https://github.com/iVis-at-Bilkent/cytoscape.js-undo-redo.git`
