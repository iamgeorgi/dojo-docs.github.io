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
        - Execute the event only once
            ```js
            on.once(div, "mouseenter", function (event) {
                domStyle.set(div, "width", "2500px");
                div.style.background = "yellow";
            })
            ```
        - Execute the event, then remove it
            ```js
            const mouseEnterHandler = on(div, "mouseenter", function (event) {
                domStyle.set(div, "width", "2500px");
                mouseEnterHandler.remove();
            })
            ```
        - Pause the event
            ```js
            const enableButton = dom.byId('enable');
            const disableButton = dom.byId('disable');
            const clickBtn = dom.byId('clickMe');
    
            const buttonHandler = on.pausable(clickBtn, "click", function () {
                alert("I am clickable");
            })
    
            on(disableButton, "click", function () {
                buttonHandler.pause()
            })
    
            on(enableButton, "click", function () {
                buttonHandler.resume()
            })
            ```
        
### _Dojo modules_
- "dojo/dom-style"
    ```js
        const domStyleDiv = dom.byId("domStyle");
        domStyle.set(domStyleDiv, "width", "2500px"); // sets the width of node to 2500px
        domStyle.get(domStyleDiv, "width"); // gets the width of node
        
        const styles =domStyle.getComputedStyle(domStyleDiv); // takes all the styles of the element
        console.log(styles.width) // get the width of the element
    ```
- "dojo/topic"
    ```js
    const btn1 = dom.byId("one");
    topic.subscribe("test/topic", function (a, b) {
        alert(a + b);
    })
    on(btn1, "click", function () {
        topic.publish("test/topic", "Testing", "And Testing again")
        // the second param also can be array ot an object
    }) // subscribes on event called test/topic
    ```
- "dojo/dom-construct"
    ```js
    const parent = dom.byId("list");
    const child = dom.byId("three");
    const fourthChild = dom.byId("four");
    const button = dom.byId("move");

    domConstruct.place(child, parent, "first"); // moves the element to the top
    domConstruct.place(child, fourthChild, "after"); // moves the element after the specified element
    domConstruct.place(child, parent, "3"); // moves the element at the fourth position inside the parent element, counts from zero
    domConstruct.place(child, fourthChild, "replace"); // removes fourthChild and place the child element instead
    domConstruct.place(child, list, "only"); // removes all child elements of list and the child instead
    domConstruct.empty(parent); // empty the content from the specified element(child nodes ot text)
    query(".list-items").forEach(domConstruct.empty); // empty the content from all elements with class list-items
    domConstruct.destroy(child) // removes the node completely
    ```
    
