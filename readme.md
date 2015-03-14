## Overview

MirrorMark is a simple, yet extensible Markdown editor created with [Codemirror](http://www.codemirror.net). 

See [Demo](http://themusicbed.github.io/MirrorMark/).

## Install

```
bower install mirrormark
```

## Dependencies
* Codemirror
* Lodash
* Font Awesome (for toolbar icons)

### CSS

```
<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css">
<link href="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.0.0/codemirror.css" rel="stylesheet" />
<link href="./css/mirrormark.min.css" rel="stylesheet" />
```
* `mirrormark.css` contains the theme for the editor and toolbar. If you'd like to adjust the theme create your own `{theme}.css` file and namespace the selectors with your theme name.
* You can load `codemirror.css` and `mirrormark.css` together by using `css/mirrormark.package.css` or just load them separately.

### Javascript

```javascript
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.0.0/codemirror.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.0.0/addon/edit/continuelist.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/codemirror/5.0.0/mode/markdown/markdown.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/lodash.js/3.5.0/lodash.min.js"></script>
<script src="./js/mirrormark.min.js"></script>
```
* You can load all of these together at once by using `js/mirrormark.package.min.js` or just load each piece separately depending on the situation.

## Basic Usage
### HTML
```
<textarea id="textarea1"></textarea>
```

### Javascript
```
textarea1 = mirrorMark(document.getElementById("textarea1"), { showToolbar: true });
textarea1.render();
```

## Custom Actions, Keymaps, and Toolbar.
MirrorMark allows you to add custom actions, keymaps, and toolbar options. Below is an example of how to add two actions at runtime and a tool icon with a dropdown to call these two actions.

### HTML
```
<textarea id="textarea2"></textarea>
```

### Javascript
```
var customActions = {
	// Inserts three images wrapped in a <div>
	"threeUp": function threeUp() {
		var html = [];
		html.push("<div class='threeUp'>");
		html.push("	<img src='' />");
		html.push("	<img src='' />");
		html.push("	<img src='' />");
		html.push("</div>");

		this.insert(html);
	},
	"fourUp": function fourUp() {
		var html = [];
		html.push("<div class='fourUp'>");
		html.push("	<img src='' />");
		html.push("	<img src='' />");
		html.push("	<img src='' />");
		html.push("	<img src='' />");
		html.push("</div>");

		this.insert(html);
	}
}

var customKeyMaps = { 
	"Shift-Cmd-Alt-3": "threeUp",
	"Shift-Cmd-Alt-4": "fourUp",
};

var customTools = [{ 
	name: "threeUp", 
	action: null, 
	className: "fa fa-fighter-jet", 
	nested: [
	    { 
    		name: "threeUp", 
    		action: "threeUp", 
    		showName: true
    	},
    	{
    		name: "fourUp", 
    		action: "fourUp", 
    		showName: true
    	}
	]
}];

textarea2 = mirrorMark(document.getElementById("textarea2"), { autofocus: true, showToolbar: true });
textarea2.registerActions(customActions);
textarea2.registerKeyMaps(customKeyMaps);
textarea2.registerTools(customTools);
textarea2.render();
```

## Options
When instantiating the editor you can pass the various Codemirror options available. There is also an option to opt to show toolbar ``` showToolbar: true ``` (Default: false).

## Custom Methods
* ***registerActions(actions)*** - Accepts an object with an Action name as the key and an anonymous function for the value.
* ***registerKeymaps(keymaps)*** - Accepts an object with Keymap name as the key and an anonymous function for the value.
* ***RegisterToolbar(tools, replace)*** - Accepts an array of custom tool objects with the option of replacing (default: false) the existing toolbar.

## Insertion Methods
* ***this.insert(string)*** - Inserts a string at the current cursor position
* ***this.insertBefore(string, cursorOffset)*** - Inserts a string at the current cursor position and then moves the cursor to the cursorOffset (int).
* ***this.insertAround(start, end)*** - Inserts a given string value at the start and end of a selection.

## Things coming
* Windows support for Keymaps
* Fullscreen editing
* Preview mode
* Status bar


