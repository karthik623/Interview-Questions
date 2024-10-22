# Interview Questions
### Q. What are the major features of React?

- It uses JSX Syntax which allows to write HTML in JS code

- It uses virtual DOM instead of real DOM to manipulate the UI

- React supports the Server side rendering which is useful for search Engine Optimization

- It follows Unidirectional Data flow

- User reusbale UI components to develop the view
--- 
### Q. How the JSX is exactly converted to DOM element?

- In React, Every component will return a JSX. This JSX just provides the syntactic sugar for the React.createElement().

- This createElement function will create the HTML node with the help of the javascript Compiler like Babel
---
### Q. What are pure components?

- Pure Components are the components which render the same output for the same state and the props i.e If there is any change in the previous state with the current State or the previous props with the current prop

- In the case of class components, Pure Component is implemented by extending the class with PureComponent

- In case of Functional Components, useMemo() helps to acheive this pure Components.

- In case of UseMemo(), we will pass a dependecy array, If the value of that state changes then the function will rerender the component again to get the updated value or UI rerender.
---
### Q. What is the difference between the deep copy and shallow copy?
- Shallow Copy: In the Shallow copy,when we try to copy the reference of an object to a new variable, only the top level properties are copied. While the nested objects or arrays will still reference to the original memory location.
- shallow copy can be made by using the object.assign() method
- we can acheive this shallow copy using spread operator as well

- Deep Copy : This deep copy on the other hand creates a completely independent copy of the object inclusing all the objects or arrays
- Deep copy can be acheived by using
``` js
JSON.parse(JSON.stringify(object))
```
- Deep copy can also be cacheived with the help of lodash.clonedeep() method and also by using custom recursive functions.
---
### Q. What are Non-enumerable property?
- Objects can have properties that don't show up when iterated through the particular object using Object.keys() or for...in loop.Those type of properties are called as non-enumerable properties.

- To create a non-enumerable property we have to use Object.defineProperty() method. This a special method to create non-enumerable properties in an object. 

- In the following example, three properties such as name, age and country were created normally and a property named "salary" was created using Object.defineProperty() method and key named enumerable was assigned with false. When the object "person" got iterated using Object.keys() the properties such as name, age and country were shown up whereas property "salary" was unable to shown up. Since salary property was unable to shown up it is called as non-enumerable property. This is the way to create non-enumerable properties.

- Object.defineProperty() is also let you create read-only properties as we saw below, we are not able to modify salary value of a person object. To make the salary property enumerable assign true to the key named enumerable.

``` js
var person = {
      name: 'gopal'
   };
   
   person.age="21",
   person.country= "India"
   
 Object.defineProperty(person, "salary", {
     value:"80000",
     enumerable :false
 })
 
console.log(Object.keys(person)) // [ 'name', 'age', 'country']
```
---
### Q. Explain all the Object methods?
-  #### 1. Object.assign(target, source):
    - This method will copy all the enumerable values of object from the source object to the target object

    ``` js
    let obj = {
    name: "karthik",
    age: 30
    };

    let obj2 = {
    foo: 32,
    bar: 22,
    data: {
        country: "Afghanistan",
        code: "AF"
        }
    };
    let result = Object.assign(obj2, obj); //Object.assign(target, source)
    console.log(result);
    ```

- #### 2.Object.create(obj):
    - This method will create a new object with required property and values can access the original object methods

    ``` js
    let obj2= {
    foo:32,
    bar:22,
    data:{
        country:"Afganistan",
        code:"AF"
        
    },
    printIntroduction() {
        console.log("Hello");
        }
    }

    let result= Object.create(obj2)
    result.name="karthik",
    result.age=24
    result.printIntroduction()
    console.log(result)
    ```
- #### 3. Object.defineProperty(obj, key, value):
    - This method will defines the new property directly on an object and returns the object. If we add writable as false, we can't edit the property that was added as its only readable

    - This method will takes an object as first parameter, Property name as second parameter and its value and configurations as third parameter

    ``` js
    const person = {
  firstName: "John",
  lastName: "Doe",
  language: "EN" 
    };

    Object.defineProperty(person, "language", {value:"NO", writable :false})
    person.language="MayBe" // Error: Cannot assign to read only property 'property1'

    Object.defineProperty(person, "language", {value:"NO", writable :true})
    person.language="Maybbe"

    Output : const person = {
  firstName: "John",
  lastName: "Doe",
  language: "Maybbe" 
    };

    ```

- #### 4. Object.entries(obj):
    - This method returns an array of the key/value pairs of an object. This will not change the original object
    - This method make it simpler to use objects in loops 

    ``` js
    let obj2= {Bananas:300, Oranges:200, Apples:500}

    for(let[fruit, type]  of Object.entries(obj2)) {
        console.log(`key is ${fruit} and value is ${type}`)
    }

    Output:
    key is Bananas and value is 300
    key is Oranges and value is 200
    key is Apples and value is 500
    ```

-   #### 5. Object.fromEntries(obj):
    - This method  will transform a list of key/value pairs into an object.
    
    ``` js

    const entries = [['a', 1], ['b', 2], ['c', 3]];
    const obj = Object.fromEntries(entries);
    console.log(obj); // { a: 1, b: 2, c: 3 }

    ```


- #### 6. Object.freeze(obj):
    - This method will freeze the object. We can't add or delete or modify any existing property of the object

    ``` js
    const obj = { Bananas:300, Oranges:200, Apples:500 };

    Object.freeze(obj);

    obj.Grapes = 33; // Error: Cannot assign to read only property 'prop'

    console.log(obj); // { Bananas:300, Oranges:200, Apples:500 }

    ```
- #### 7. Object.seal(obj);
    - This method will seal the object which will allow the modification of existing property but doesn't allow to add or delete a property.

    ``` js
    const obj = { Bananas:300, Oranges:200, Apples:500 };

    Object.seal(obj);

    obj.Grapes = 33; // Error: Cannot assign to read only property 'prop'

    obj.Bananas = 100

    console.log(obj); // { Bananas:100, Oranges:200, Apples:500 }

    ```
- #### 8. Object.keys(obj):
    - Returns an array of a keys in the given object.

    ``` js
    const obj = { a: 1, b: 2, c: 3 };

    console.log(Object.keys(obj)); // ['a', 'b', 'c']
    ```
- #### 9. Object.values(obj):
    - Returns an array of a values for the given object.

    ``` js
    const obj = { a: 1, b: 2, c: 3 };

    console.log(Object.values(obj)); // [1, 2, 3]
    ```

- #### 10. Object.hasOwnProperty(prop):
    - Returns a Boolean indicating whether the object has the specified property as its own property or not.

    ``` js 
    const obj = { a: 1 };

    console.log(obj.hasOwnProperty('a')); // true

    console.log(obj.hasOwnProperty('b')); // false

    ```

- #### 11. Object.is(value1, value2):
    - Returns a Boolean by checking whether two values of the object are same or not

    ``` js
    console.log(Object.is(25, 25)); // true

    console.log(Object.is('foo', 'bar')); // false
    ```

- #### 12. Object.getOwnPropertyNames(obj):
    - This method will retrun an array of all keys (enumerable or not) found directly in a given object.
    ``` js
    const obj = { a: 1, b: 2, c: 3 };
    console.log(Object.getOwnPropertyNames(obj)); // ['a', 'b', 'c']

    ```
- #### 13. Object.getOwnPropertyDescriptors(obj):
    - Returns an object containing all own property descriptors of an object.
    ``` js
    const obj = { a: 1 };
    console.log(Object.getOwnPropertyDescriptors(obj)); 
    /* 
    Output:
    {
        a: {
        value: 1,
        writable: true,
        enumerable: true,
        configurable: true
        }
    }
    */

    ```
- #### 14. Object.isFrozen(obj):
    - Retruns a Boolean by checking if the object is frozen or not

    ``` js
    const obj = Object.freeze({ a: 1 });

    console.log(Object.isFrozen(obj)); // true
    ```

- #### 15. Object.isSealed(obj):
    - Retruns a Boolean by checking if the object is sealed or not

    ``` js
    const obj = Object.seal({ a: 1 });

    console.log(Object.isSealed(obj)); // true
    ```
---

- ### Q. Explain all the Array methods?

-  #### 1. Array1.concat(Array2):
    - This method merges 2 or more arrays and returns a new array

    ``` js
    const arr1 = [1, 2];

    const arr2 = [3, 4];

    const result = arr1.concat(arr2);

    console.log(result); // [1, 2, 3, 4]
    ```

- #### 2. Array.copyWithin(target,start,end):
    - This method will shallow copies part of this array to another location in the same array and returns this array without modifying its length.
    ``` js
    const array1 = ['a', 'b', 'c', 'd', 'e'];

    console.log([1, 2, 3, 4, 5].copyWithin(2));//[1, 2, 1, 2, 3]

    console.log(array1.copyWithin(0, 3, 4)); //["d", "b", "c", "d", "e"]

    console.log(array1.copyWithin(1, 3)); //["d", "d", "e", "d", "e"]

    ```

- #### 3. Array.entries():
    - This method will not take any parameters, It will return a new array iterator object that contains the key/value pairs for each index in the array.

    ``` js
    // Create an Array
    const fruits = ["Banana", "Orange", "Apple", "Mango"];

    // Create an Iterator
    const list = fruits.entries();

    // List the Entries
    let text = "";
    for (let x of list) {
        text += x;
    }
    ```

- #### 4. Array.every();
    - This method will returns a boolean by Testing whether all elements pass the provided function.

    ``` js
    const arr = [1, 2, 3, 4];

    const result = arr.every(num => num < 5);

    console.log(result); // true
    ```

- #### 5. Array.fill(value, start, end):
    - This method will take the value and fill the static value from the start position to the end position
    - This method also helps to create a new array with fill and map methods
    
    ``` js
    const array1 = [1, 2, 3, 4];

    // Fill with 0 from position 2 until position 4
    console.log(array1.fill(0, 2, 3));
    // Expected output: Array [1, 2, 0, 0]

    // Fill with 5 from position 1
    console.log(array1.fill(5, 1));
    // Expected output: Array [1, 5, 5, 5]

    console.log(array1.fill(6));
    // Expected output: Array [6, 6, 6, 6]
    ```

    ``` js
    const array = Array(100).fill().map((_, index) => index + 1);
    console.log(array);
    ```
    - Here we are not using the current value, so we are replacing it with the underscore(_). Second Argument is the inndex and the third argument is the array itself, we are not using it here.

- #### 6. Array.map(function):
    - This method will create a new array by accessing every single value of the array and can tranform the element by performing an action

    ``` js
    const arr = [1, 2, 3];

    const result = arr.map(num => num * 2);

    console.log(result); // [2, 4, 6]
    ```


- #### 7. Array.filter(function):
    - This method Creates a new array with elements that satisfies the test condition.

    ``` js
    const words = ['spray', 'elite', 'exuberant', 'destruction', 'present'];

    const result = words.filter((word) => word.length > 6);

    console.log(result);
    // Expected output: Array ["exuberant", "destruction", "present"]
    ```
- #### 8. Array.reduce(accumulator,current):
    - This method will returns a single value by reducing the array and performing the calculations on the every element.

    ``` js
    const arr = [1, 2, 3, 4];

    const sum = arr.reduce((acc, num) => acc + num, 0);

    console.log(sum); // 10
    ```

- #### 9. Array.push(val):
    - Adds elements to the end and returns the new length.
    ``` js
    const arr = [1, 2];
    console.log(arr.push(3)); // 3
    console.log(arr); // [1, 2, 3]
    ```

- #### 10. Array.pop(val):
    - Removes the last element and returns that element.
    ``` js
    const arr = [1, 2, 3];
    console.log(arr.pop()); // 3
    console.log(arr); // [1, 2]
    ```
- #### 11. Array.unshift(val):
    - Adds elements to the start and returns the new length.
    ``` js
    const arr = [2, 3];
    console.log(arr.unshift(1)); // 3
    console.log(arr); // [1, 2, 3]
    ```
- #### 12. Array.shift(val):
    - Removes the first element and returns that element.
    ``` js
    const arr = [1, 2, 3];
    console.log(arr.shift()); // 1
    console.log(arr); // [2, 3]
    ```
- #### 13. Array.sort():
    - Sorts elements in place and returns the sorted array.
    ``` js
    const arr = [3, 1, 2];
    arr.sort();
    console.log(arr); // [1, 2, 3]
    ```
- #### 14. Array.reverse():
    - Reverses the order of elements.
    ``` js
    const arr = [1, 2, 3];
    arr.reverse();
    console.log(arr); // [3, 2, 1]
    ```
- #### 15. Array.toString():
    - Returns a string by converting all the values in the array
    ```js
    const arr = [1, 2, 3];
    console.log(arr.toString()); // "1,2,3"
    ```
- #### 16.Array.values():
    - Returns a new Array Iterator containing values. This Array iterator can be looped over for of loop to get the values
    ``` js
    const arr = ['a', 'b', 'c'];
    const iterator = arr.values();
    for (let value of iterator) {
    console.log(value); // 'a', 'b', 'c'
    }
    ```
- #### 17. Array.slice(start,end):
    - This method will returns a part of an array which will be shallow copied . This part is taken as per the start and end of the index where the end value is not included.
    - This method doesn't modify the original array
    ``` js
    const animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];

    console.log(animals.slice(2));
    // Expected output: Array ["camel", "duck", "elephant"]

    console.log(animals.slice(2, 4));
    // Expected output: Array ["camel", "duck"]
    ```
- #### 18. Array.splice(start, deleteCount,val):
    - This method will change the original array. It takes the start value and delete the number of values as per the second parameter and insert the value at the start index.
    - The splice() method of Array instances changes the contents of an array by removing or replacing existing elements and/or adding new elements in place.
    ```js
    const months = ['Jan', 'March', 'April', 'June'];
    months.splice(1, 0, 'Feb');
    // Inserts at index 1
    console.log(months);
    // Expected output: Array ["Jan", "Feb", "March", "April", "June"]
    months.splice(4, 1, 'May');
    // Replaces 1 element at index 4
    console.log(months);
    // Expected output: Array ["Jan", "Feb", "March", "April", "May"]
    ```

- #### 19. Array.some(function):
    - This method returns a boolean for the callback function where at least one element in the array passes the test implemented by the provided function. 
    - It returns true if, in the array, it finds an element for which the provided function returns true; otherwise it returns false. It doesn't modify the array.
    ``` js
    const array = [1, 2, 3, 4, 5];

    // Checks whether an element is even
    const even = (element) => element % 2 === 0;

    console.log(array.some(even));
    // Expected output: true    
    ```
- #### 20. Array.keys():
    - This method returns a new Array Iterator containing keys.
    - This Array  Iterator can be iterated by using the for of loop to get the keys

    ``` js
    const arr = ['a', 'b', 'c'];
    const iterator = arr.keys();
    for (let key of iterator) {
        console.log(key); // 0, 1, 2
    }
    ```
- #### 21. Array.join(seperator):
    - This method creates and retruns a string of all the values in the array by concatenating the values with the specified seperator.
    ``` js
    const elements = ['Fire', 'Air', 'Water'];

    console.log(elements.join());
    // Expected output: "Fire,Air,Water"

    console.log(elements.join(''));
    // Expected output: "FireAirWater"

    console.log(elements.join('-'));
    // Expected output: "Fire-Air-Water"
    ```
- #### 22. Array.indexOf(val, fromIndex(opt)):
    - This method returns the first index at which a given element can be found in the array, or it will return -1 if  the value is not present.
    ``` js
    const arr = [1, 2, 3];
    console.log(arr.indexOf(2)); // 1
    console.log(arr.indexOf(5)); //-1
    ```
- #### 23. Array.includes(val,fromIndex(opt)):
    - This method returns a Boolean by checking whether the value exists in the array or not. 
    ``` js
    const array1 = [1, 2, 3];

    console.log(array1.includes(2));
    // Expected output: true

    const pets = ['cat', 'dog', 'bat'];

    console.log(pets.includes('cat'));
    // Expected output: true

    console.log(pets.includes('at'));
    // Expected output: false
    ```
- #### 24. Array.forEach(callback Function):
    - The forEach() method of Array instances executes the provided function on each array element.
    - The callback function can take 3 parameters. First parameter is the value, index(opt) and array itself(opt).
    ``` js
    const arr = [1, 2, 3];
    arr.forEach(num => console.log(num * 2)); // 2, 4, 6
    ```

- #### 25. Array.find(callback Function):
    - Returns the first element that satisfies the provided condition in the callback function.
    ``` js
    const arr = [1, 2, 3, 4];
    const result = arr.find(num => num > 2);
    console.log(result); // 3
    ```
- #### 26. Array.findIndex(callback Function):
    - Returns the index of the first element that satisfies the testing function.
    ``` js
    const arr = [1, 2, 3, 4];
    const result = arr.findIndex(num => num > 2);
    console.log(result); // 2
    ```
    Note: Both indexOf and findIndex methods return the first index of the element specified. indexOf method takes the element whose index is to be returned as the argument and findIndex takes a function as an argument. But both the functions return "-1" as output.


- #### 27. Array.flat(depth):
    - Creates a new array by concatening the sub arrays till the provided depth. Default value is 1 and max is infinity
    ``` js
    const arr = [1, [2, [3, 4]]];
    const arr2 = [0, 1, [2, [3, [4, 5]]]];

    const result = arr.flat(2);
    console.log(result); // [1, 2, 3, 4]

    console.log(arr2.flat());
    // expected output: Array [0, 1, 2, Array [3, Array [4, 5]]]

    console.log(arr2.flat(2));
    // expected output: Array [0, 1, 2, 3, Array [4, 5]]

    console.log(arr2.flat(Infinity));
    // expected output: Array [0, 1, 2, 3, 4, 5]
    ```


- ### Q. Can you explain the difference between controlled and uncontrolled components in React?
    - Controlled and Uncontrolled components both refer to how the form data is managed within a component.
    - #### <u>Controlled Components:</u>
    - In the Controlled components, the form data is handled by the component state . The input feilds will be bounded with the state directly allowing to access the values. This gives more control over the form data. 
    ``` js
    import React, { useState } from 'react';

    function ControlledComponent() {
    const [inputValue, setInputValue] = useState('');

    const handleChange = (event) => {
        setInputValue(event.target.value);
    };

    const handleSubmit = (event) => {
        event.preventDefault();
        alert('Submitted: ' + inputValue);
    };

    return (
        <form onSubmit={handleSubmit}>
        <input type="text" value={inputValue} onChange={handleChange} />
        <button type="submit">Submit</button>
        </form>
    );
    }

    export default ControlledComponent;
    ```
    - #### <u>UnControlled Components:</u>
    - In the case of unControlled Components, the form data is handled by the  DOM itself. We can use refs to access the input values directly when needed. 
    ```js
    import React, { useRef } from 'react';

    function UncontrolledComponent() {
    const inputRef = useRef(null);

    const handleSubmit = (event) => {
        event.preventDefault();
        alert('Submitted: ' + inputRef.current.value);
    };

    return (
        <form onSubmit={handleSubmit}>
        <input type="text" ref={inputRef} />
        <button type="submit">Submit</button>
        </form>
    );
    }

    export default UncontrolledComponent;
    ```
- ### Q. Can you explain the React lifecycle methods?
    - There are 3 lifecycle phases in react. They are Mounting,Updating and Unmounting.
    - ### Class Components:
    - #### <u>Mounting:</u> 
        - The phase in which a component is being created and inserted into the DOM.
        - In this phase, componentDidMount() will be called
    - #### <u>Updating:</u> 
        - The phase in which a component is being re-rendered as a result of changes to either its props or state.
        - In this phase, shouldComponentUpdate() and ComponentWillUpdate() methods are called.
    - - #### <u>Unmounting:</u> 
        - The phase in which a component is being removed from the DOM.
        - In this phase, componentWillUnmount() will be called
    - ### Functional Components:
    - In the functional components, the same lifecycle behaviors can be managed using useEffect hook.
    - #### <u>Mounting and Updating:</u> 
        - useEffect(() => { ... }, []) acts like componentDidMount().
        - useEffect(() => { ... }, [dependencies]) acts like both componentDidUpdate() and componentWillUnmount().
        You can return a cleanup function from useEffect to handle side effects when the component unmounts.
    - #### <u>Unmounting:</u> 
        - The cleanup function returned by useEffect serves the same purpose as componentWillUnmount().

- ### Q. What is Hoisting in javascript?
    - Hoisting is a javascript mechanisim where variables and functions declarations are moved to the top of the scope. 
    - It allows to use the variables and functions before they are declared.
    - #### Variable Hoisting:
        - When you declare a variable using var, Javascript hoists the variable to top of its scope.
        - It means that only the decleration is hoisted not the initialization. if we try to access the value before initializing it, we will get the value as undefined instead of actual value.
        ``` js
        console.log(x); // Outputs: undefined
        var x = 5;
        console.log(x); // Outputs: 5
        ```
        - Varibles declared with let and const are also hoisted but they are not initialized. They will enter into a "temporial dead zone" from the time where they are hoisted and to the time where the actual value gets assigned.
        - Accessing those values at that time will gives the Reference Error
        ```js
        console.log(a); // Throws ReferenceError: Cannot access 'a' before initialization
        let a = 10;
        ```
    - #### Function Hoisting:
        - This Function Declerations are fully hoisted. means that both the function name and the body are available before the function is declared in the code.
        ``` js
        greet(); // Outputs: Hello!

        function greet() {
            console.log("Hello!");
        }
         ```
         - In the case of Funciton Expression, means a function assigning to the variable or the arrow functions, this hoisting will not work.
         - In this case, this will be treated as a varible only.
         ``` js
        greet(); // Throws TypeError: greet is not a function
        var greet = function() {
            console.log("Hello!");
        };
         ```
- ### Q. What is Event Loop?
    - Event loop is essential for managing asynchronous operations in JavaScript, enabling non-blocking behavior.
    - This helps to handle tasks like user Interactions, timers, Promises etc which can block the main thread.
    - The Purpose of the Event loop is to check the call stack continuously,whenever the call stack is empty, Event loop takes the task from the ( microstack Queue > callback Queue) and pushes it to callstack.
    - Here the priority is grater for the microstack queue than the callback queue.
    - Microstack queue involves the tasks like Promises and MutationObserver callbacks.
    - Callback Queue takes the tasks like setTimeout, setInterval, I/O Operations and user Interactions.
    ``` js
    console.log("Start");
    setTimeout(() => {
        console.log("Timeout 1");
    }, 0);
    Promise.resolve().then(() => {
        console.log("Promise 1");
    }).then(() => {
        console.log("Promise 2");
    });
    setTimeout(() => {
        console.log("Timeout 2");
    }, 0);
    console.log("End");

    Output:
    // Start
    // End
    // Promise 1
    // Promise 2
    // Timeout 1
    // Timeout 2
    ```
- ### Q. What is difference between setTimeout and setInterval?
    - setTimeout function is used to ececute the function only once after the specified interval.
    - setInterval function is used to execute the function repeadtly after the delay.
    - These both functions will geerate a interval ID that can be cleared by using clearTimeout function
    ```js
    const timeoutId = setTimeout(() => {
        console.log("This won't run");
    }, 2000);

    clearTimeout(timeoutId);

    const intervalId = setInterval(() => {
        console.log("This will stop");
    }, 2000);

    clearInterval(intervalId);
    ```
- ### Q. Rest and Spread Operator.
    - #### Rest Operator:
    - The Rest Operator (...) allows to collect multiple arguments into a single array
    - This mainly helps to deals with the functions that gets varying number of arguments to the function
    - Some of the use cases are:
        - Accepts multiple args to the function and can take as array as an input.
        ```js
        function sum(...numbers) {
            return numbers.reduce((acc, curr) => acc + curr, 0);
        }

        console.log(sum(1, 2, 3, 4)); // Outputs: 10
        ```
        - Destructuring Assignments: We can use rest Operator to extract the remaining properties from an object or array.
        ```js
        const array = [1, 2, 3, 4, 5];
        const [first, second, ...rest] = array;
        console.log(first); // Outputs: 1
        console.log(second); // Outputs: 2
        console.log(rest); // Outputs: [3, 4, 5]
        ```
        - This Rest operator is uesd to combine arrays 
        ```js
        const array1 = [1, 2, 3]
        const array2 = [4, 5, 6]
        const merged = [...array1, ...array2]
        // [1, 2, 3, 4, 5, 6]
        ```
        - Spread Operator: This Spread Operator is used to expand or spread objects or arrays into individual elements.
        - This spread operator is used to create shallow copy of arrays or objects.
        ```js
        const originalArray = [1, 2, 3];
        const copiedArray = [...originalArray];
        console.log(copiedArray); // Outputs: [1, 2, 3]

        const originalObject = { x: 1, y: 2 };
        const copiedObject = { ...originalObject };
        console.log(copiedObject); // Outputs: { x: 1, y: 2 }
        ```
    - This spread operator is also used to create array or object with the existing ones.
    ```js
    const array = [1, 2, 3];
        const newArray = [...array, 4, 5];
        console.log(newArray); // Outputs: [1, 2, 3, 4, 5]

        const obj = { x: 1, y: 2 };
        const newObject = { ...obj, z: 3 };
        console.log(newObject); // Outputs: { x: 1, y: 2, z: 3 }
    ```
    - This spread operator is also used to pass elements of an array as individual arguments to a function.
    ```js
    const numbers = [1, 2, 3];
    const sum = (a, b, c) => a + b + c;
    console.log(sum(...numbers)); // Outputs: 6
    ``` 
- ### Q. What are Closure?
    - A closure is formed when the function retain its access to its lexical scope, then the closure is formed.
    - When an inner function is defined inside an outer function, it forms a closure with the outer variable function.
    - Below is the example of closure
    ```js
    function outerFunction() {
    let outerVariable = 'I am from the outer function';

    function innerFunction() {
        console.log(outerVariable); // Accessing outerVariable
    }

    return innerFunction; // Return the inner function
    }

    const myClosure = outerFunction(); // Executes outerFunction, returns innerFunction
    myClosure(); // Outputs: I am from the outer function
    ```
    - Closures helps to acheive Encapsulation. It can restrict to access the private variables.
    ```js
    function createCounter() {
    let count = 0; // Private variable

    return {
        increment: function() {
            count++;
            return count;
        },
        decrement: function() {
            count--;
            return count;
        },
        getCount: function() {
            return count;
        }
    };
    }

    const counter = createCounter();
    console.log(counter.increment()); // Outputs: 1
    console.log(counter.increment()); // Outputs: 2
    console.log(counter.getCount()); // Outputs: 2
    ```
- ### Q. What is difference between a Promise and a Callback?

    - Both the promise and callback are used to handle asynchronous operations in the code.

    - Callback: A callback is a function passed as an argument to another function, which is then executed after some operation is completed. It is a way to ensure that certain code runs only after a specific asynchronous task finishes.
    - Promise: A promise is an object that represents the eventual completion (or failure) of an asynchronous operation.Promises provide a more structured way to handle asynchronous tasks and chain operations.
    - Callback Example:
    ```js
    function fetchData(callback) {
    setTimeout(() => {
        const data = { message: "Hello, World!" };
        callback(data);
    }, 1000);
    }

    fetchData((result) => {
        console.log(result.message); // Outputs: Hello, World!
    });
    ```
    - Promise Example:
    ```js
    function fetchData() {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            const data = { message: "Hello, World!" };
            resolve(data);
        }, 1000);
    });
    }

    fetchData()
        .then((result) => {
            console.log(result.message); // Outputs: Hello, World!Destructuring
            - #### Rest and Spread Operators
            - #### Promises
            - #### Classes
            - #### Modules including exports and imports
            
        })
        .catch((error) => {
            console.error(error);
        });
    ```
- ### Q. List the Features of ES6?
    -  Let and Const
    -  Arrow Functions
    -  Template Literals
    -  Destructuring
    -  Rest and Spread Operators
    -  Promises
    -  Classes
    -  Modules including exports and imports
    - Iterators and Generators
        - Below is example for the Iterators.
        - This Iterator has a next function which will have a value which holds the actual value and a done boolean to represent whether next values are avilable to iterate or not.
        - Iterators and generators provides a mechanisim for customizing the behaviour of (for...of ) loop.
        - These Iterators and Generators functions helps to traverse between our own custum datatypes and access the values in it.
        ```js 
        const myIterator = {
            index: 0,
            values: ['a', 'b', 'c'],
            next: function() {
                if (this.index < this.values.length) {
                    return { 
                        value: this.values[this.index++], 
                        done: false 
                    };
                } else {
                    return { done: true }; // Indicate completion
                }
            }
        };

        // Using the iterator
        console.log(myIterator.next()); // { value: 'a', done: false }
        console.log(myIterator.next()); // { value: 'b', done: false }
        console.log(myIterator.next()); // { value: 'c', done: false }
        console.log(myIterator.next()); // { done: true }
        ```
        - Generator Function: This Generator function is a special type of function, similar to the Iterator function. 
        - Here we dont have to manage the state internally, dont have to the implement the next() function. we can simply use the yeild keyword. The syntax to define the Generator function is by using the *keyword after the keyword function. 
        - Below is the example of the Generator function.
        ```js
        function* generator() {
        yield 1;
        yield 2;
        yield 3;
        }

        const gen = generator(); // "Generator { }"

        console.log(gen.next().value); // 1
        console.log(gen.next().value); // 2
        console.log(gen.next().value); // 3
        ```
    - Map, Set, WeakMap, and WeakSet
        - Map: A Map is a collection of key-value pairs where both keys and values can be of any type.
        - Set: A Set is a collection of unique values. It allows you to store any type of values, but it automatically removes duplicates.
        - WeakMap: A WeakMap is similar to a Map, but its keys must be objects. if there are no references to an object used as a key, the entry will be garbage collected.
        - WeakSet: SA WeakSet is similar to a Set, but its values must be objects.Similar to the weakmap, if there are no references to an object used as a key, the entry will be garbage collected.
        ```js
        let weakMap = new WeakMap();
        let obj = {};

        weakMap.set(obj, "data");

        // At this point, obj is still accessible, and the WeakMap holds a weak reference to it.
        console.log(weakMap.get(obj)); // "data"

        // If we remove the strong reference to obj:
        obj = null; // Now, there's no other reference to the original object.

        // The garbage collector can now collect the original object,
        // and thus the entry in the WeakMap is also cleaned up.
        ```
    - In summary, WeakMap and WeakSet provide a way to hold references to objects without preventing their garbage collection, making them useful for managing memory in applications efficiently.
    
    - Object.assign() method

    
