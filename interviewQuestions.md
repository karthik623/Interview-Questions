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



