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
