# Dojo Toolkit

## Getting started
### _There are two ways of initalization dojo in your project_
- As function call when the library is fully loaded
    ```js
    dojo.ready(function(){})
    ```
- AMD - Asynchronus Module Definiten (load modules only when they needed)
    ```js
    require([module1, module2,…], function(module1, module2,…){});
    ```
### _DOM Manipulation in dojo_
- Select nodes from the DOM tree
    ```js
     dojo.byId("test"); // id selector
     dojo.query("#test"); // css selector(return all the nodes with id test)
     dojo.query(".testClass"); // returns nodes with class testClass
     dojo.query("div"); // select all div elements
     dojo.query("div > a"); // look for all div elements with a href tags
     dojo.query("[name='testName']") // returns array, synthax for getting elements by they attributes
     dojo.query("[name^='test']") // queries all the nodes with attr name and starting with test
    ```
- Event handlers
    - Basic synthax
        ```js
            on(element, event, function (e) {
                // callback function
            })
        ```
    - Example events
        - Basic click event
        ```js
        const hideButton = dom.byId("hideDiv");
        on(hideButton, "click", function (event) {
            div.style.display = "none";
        })
        ```
        - Attach one event to multiple nodes inside parent element
        ```js
        const myDivElement = dom.byId("myDiv1");
        on(myDivElement, on.selector(".clickMe", "click"), function (e) {
            alert(e.target.id);
        })
        
        on(myDiv1Element, ".clickMe:click", function (e) {
            alert(e.target.id);
        }) // another way to attach event on multiple elements
        
        // <div id="myDiv">
            //<button id="button1" class="clickMe">Click me1</button>
            //<button id="button2" class="clickMe">Click me2</button>
            //<button id="button3" class="clickMe">Click me3</button>
        //</div>
        ```
    
