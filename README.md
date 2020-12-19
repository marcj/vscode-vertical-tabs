# VSCode vertical tabs extension


Since VSCode does not allow to configure the editor tabs and I need them to be vertical (because I usually have a lot of open files), 
I wrote a little CSS/JS to have that feature. It's not perfect and more hacky than necessary, but I don't have the time to wrap it in a official extension. 

![screenshot](https://github.com/marcj/vscode-vertical-tabs/blob/main/vscode-vertical-tabs.png?raw=true)

So you have to copy und paste this code and load it via the extension [Cusom CSS and JS Loader](https://marketplace.visualstudio.com/items?itemName=be5invis.vscode-custom-css)

Install it and place following code in your settings.json:

```
"vscode_custom_css.policy": true,
"vscode_custom_css.imports": [
  "file:///Users/YOUR_USER_NAME/.vscode/tabs.css",
  "file:///Users/YOUR_USER_NAME/.vscode/tabs.js",
]
```


tabs.css

```body {
    --vertical-bar-width: 200px;
}

.editor-container {
    display: flex;
}

.editor-container .tabs-container {
    flex: 0 0 var(--vertical-bar-width);
}

.editor-container .tabs-container .tab .tab-actions {
    margin-left: auto;
}

.editor-container .tabs-container .tab {
    position: relative;
    display: flex;
    white-space: nowrap;
    align-items: center;
    cursor: pointer;
    height: 26px;   
    box-sizing: border-box;
    padding-left: 10px;
    border-bottom: 1px solid #c0c0c00a;
}

.editor-group-container .tabs {
    display: flex;
    flex-direction: row-reverse;
    align-items: center;
    overflow: hidden;
}

.editor-group-container .tabs .tabs-breadcrumbs {
    flex: 1;
    overflow: hidden;
}

.monaco-workbench .monaco-editor {
    margin-top: 0 !important;
}

.minimap.slider-mouseover {
    transform: translateX(calc(var(--vertical-bar-width) * -1));
}

.monaco-scrollable-element.editor-scrollable.vs-dark {
    width: calc(100% - 66px) !important;
}
 
.monaco-workbench .monaco-editor,
.monaco-workbench .overflow-guard {
    max-width: 100%;
}

.editor-container .editor-instance {
    flex: 1;
    overflow: hidden;
}
```


tabs.js

```
function setup() {
    const groups = document.querySelectorAll('.editor-group-container');
    console.log('tabs', groups);
    if (!groups.length) return false;

    for (const group of groups) {
        const container = group.querySelector('.editor-container');
        const tabs = group.querySelector('.tabs-and-actions-container .tabs-container');
        if (!container || !tabs) continue;
        
        container.classList.add('show-file-icons');
        container.insertBefore(tabs, container.firstChild);
    }
}

setInterval(setup, 2000);
```
