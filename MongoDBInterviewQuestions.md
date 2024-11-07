# Interview Questions

### Q. What is MongoDB and how does it differ from traditional relational databases?
- Mongo DB is a noSQL Database that stores data in binary format called BSON (Binary JSON). BSON is similar to the JSON but it can includes additional datatypes such as Date and Binary Data
- In the case of MongoDB, we have Collections and the documents. In each collection, we can store multiple documents.

- ### Q. How do you create a new database in MongoDB? Can you provide an example?
- To create a new database, we can use "use" command. Below is the example.
```js
use myNewDatabase
```

- ### Q. How do you create a collection in MongoDB? Can you show an example?
- To create a Collection, we can use UseCollection method.
- We can also directly specify the collection name and start inserting the documents. In either way the collections are created.
```js
db.createCollection("myCollection")
db.myCollection.insertOne({name:'karthik',age:'24'})
```

- ### Q. How do you insert a document into a collection? Can you provide an example?
- You can insert a document using the insertOne or insertMany methods. Below is the example
```js
db.myCollection.insertOne({ name: "Alice", age: 30 })
```
```js
try {
   db.users.insertMany([
      { name: "Ivy", age: 29 },
      { name: "Jack", age: "not-a-number" }  // This will cause an error
   ], { ordered: true });
} catch (e) {
   print(e);
}
```
- If you're using ordered: true and an error occurs, the entire operation will fail, and no documents will be inserted. You can catch the error using a try-catch block: 

- ### Q. What are the different ways to update documents in MongoDB? Please explain with examples.
- We can use updateOne, updateMany, and replaceOne. Below are the examples.
Syntax: 
```js
db.collection.updateOne(
  filter,
  update,
  options
)
//Here we can use the option called upsert which is both update and insert
```
```js
db.users.updateOne(
  { username: "john_doe" },  // Filter: Find user by username
  { $set: { email: "john@example.com", status: "active" } },  // Update: Set new email and status
  { upsert: true }  // Upsert option
);
```
- This will insert the new document even if it didnt find any existinig documents with the filter condition.
```js
db.users.updateOne(
  { username: "john_doe" },  // Filter: Find user by username
  { $set: { email: "john@example.com", status: "active" } },  // Update: Set new email and status
);
```
Note: No Action will be taken if no documents are found with the filtering criteria.

- #### updateMany():
- This  will udpate all the documents that matches the filtering criteria.
```js
db.myCollection.updateMany({ age: { $gt: 30 } }, { $set: { status: "Senior" } })
```
- #### replaceOne(): 
- This will replace a single Document entirely that matches the filter condition. 
```js
db.users.replaceOne(
  { username: "john_doe" },
  { username: "john_doe", email: "john@example.com", status: "active" }
);
```
- ### How do you delete a database in MongoDB? Can you provide an example?
- You can delete a database using the dropDatabase method. Below is the example
```js
use myDatabase
db.dropDatabase()
``` 

- ### How do you delete a collection in MongoDB? Can you show an example?
- You can delete a collection using the drop method.Below is the example
```js
db.myCollection.drop()
```

- ### How do you delete documents from a collection? Can you provide examples?
- We can use deleteOne or deleteMany. This function  will take the filtering condition and deletes the documents that matches the filtering condition.
```js
db.myCollection.deleteOne({ name: "Alice" })

db.myCollection.deleteMany({ age: { $lt: 20 } })
```
- ### Q. What is the purpose of the $ operators in update operations? Can you provide examples?
- #### $set :
    - Updates the value of a field.
    ```js
    db.users.updateOne(
        { _id: ObjectId("someObjectId") },
        { $set: { name: "Jane Doe" } }
    );
    ```
- #### $unset :
    - Removes a field from a document.
    ```js
    db.users.updateOne(
        { _id: ObjectId("someObjectId") },
        { $unset: { age: "" } }
    );
    ```
- #### $push :
    - The $push operator adds a specified value to an array. If the array does not exist, MongoDB will create it.
    ```js
    db.users.updateOne(
        { _id: ObjectId("someObjectId") },
        { $push: { hobbies: "swimming" } }
    );
    ```
- #### $each Modifier :
    - The $each modifier allows you to add multiple values to an array using the $push operator. It takes an array of values and pushes them into the specified array.
    ```js
    db.users.updateOne(
        { _id: ObjectId("your_document_id") },
        { $push: { scores: { $each: [85, 90, 95] } } }  // Adds 85, 90, and 95 to the scores array
    )
    ```
- #### $pull :
    - Removes an item from an array.
    ```js
    db.users.updateOne(
        { _id: ObjectId("someObjectId") },
        { $pull: { hobbies: "gaming" } }
    );
    ```
- #### $pop :
    - Removes the first or last item from an array. Use 1 to pop the last item, -1 for the first.
    ```js
    db.users.updateOne(
        { _id: ObjectId("someObjectId") },
        { $pop: { hobbies: 1 } }  // Removes the last hobby
    );
    ```
- #### $addToSet :
    - The $addToSet operator in MongoDB is used to add a value to an array only if it does not already exist in that array. This operator is helpful for maintaining unique values within an array.
    ```js
    db.users.updateOne(
        { _id: ObjectId("your_document_id") },  // Filter to find the specific user
        { $addToSet: { hobbies: "painting" } }  // Adds "painting" to the hobbies array if it doesn't already exist
    )
    ```
- #### $inc :
    - Increments the value of a field by a specified amount.
    ```js
    db.users.updateOne(
        { _id: ObjectId("someObjectId") },
        { $inc: { age: 1 } }
    );
    ```
- #### $rename : 
    - the $rename operator is used to rename a field in a document. This can be done using the updateOne or updateMany method.
    ```js
    db.collection.updateOne(
        { /* filter criteria */ },
        { $rename: { "oldFieldName": "newFieldName" } }
    )

    db.users.updateOne(
        { _id: ObjectId("your_document_id") },  // Filter to find the specific user
        { $rename: { "username": "user_name" } }  // Renames 'username' to 'user_name'
    )
    ```
- #### $currentDate :
    - the $currentDate operator is used to set a field to the current date and time. This operator can be particularly useful for updating timestamps in documents, such as last modified times.
    ```js
    db.users.updateOne(
        { _id: ObjectId("your_document_id") },  // Filter to find the specific user
        { $currentDate: { lastModified: { $type: "date" } } }  // Sets 'lastModified' to the current date
    )
    ```
- #### $min and $max :
    - $min and $max operators are used to update a feild to a specified value .
    ```js
    db.products.updateOne(
        { _id: ObjectId("product_id") },
        { $min: { price: 10 } }  // This will keep the price at 10
    )

    db.products.updateOne(
        { _id: ObjectId("product_id") },
        { $set: { price: 9 } }  // This will fail to update because 9 < 10
    )
    ```
    - In this case, if you attempt to set the price to 9 but still The price will remain at 10. we can still insert the less values  using  the insertOne function.
    ```js
    db.products.insertOne(
        { name: "New Product", price: 9 }  // This will succeed
    )
    ```
- #### $mergeObjects : 
    - the $mergeObjects operator is used to combine multiple documents or objects into a single object. It is particularly useful in aggregation pipelines when you want to combine fields from different documents
    ```js
    db.users.aggregate([
   {
      $project: {
         userInfo: {
            $mergeObjects: [
               { name: "John", age: 25 },
               { name: "Doe", city: "New York" }
            ]
         }
      }
   }
    ])
    ```
- ####  $sort :
    - Sorts elements in an array.
    ```js
    db.users.updateOne(
        { _id: ObjectId("someObjectId") },
        { $push: { hobbies: { $each: ["hiking"], $sort: 1 } } }
    );
    ```
- #### $setOnInsert :
    - the $setOnInsert operator is used in the context of an upsert operation, which means it is specifically designed to set a field value only when a new document is inserted. If the document already exists, $setOnInsert does not modify the existing fields.
    ```js
    db.users.update(
        { username: "johndoe" },  // Filter criteria
        { 
            $set: { email: "johndoe@example.com" },  // Update email if user exists
            $setOnInsert: { createdAt: new Date() }  // Set createdAt only if inserting
        },
        { upsert: true }  // Perform an insert if no document matches the filter
    )
    ```
    - Suppose you have a collection called users and you want to either insert a new user or update an existing user’s information. You want to set a createdAt timestamp only when a new document is inserted.
    
- ### Comparision Operator:
    - #### $gt (Greater Than) :
    - Used to filter documents where a field's value is greater than a specified value.
    ```js
    db.users.find({ age: { $gt: 25 } });
    ```
    - #### $lt (Less Than) :
    - Used to filter documents where a field's value is less than a specified value.
    ```js
    db.users.find({ age: { $lt: 30 } });
    ```
    - #### $gte (Greater Than or Equal To) :
    - Used to filter documents where a field's value is greater than or equal to a specified value.
    ```js
    db.users.find({ age: { $gte: 25 } });
    ```
    - #### $lte (Less Than or Equal To) :
    - Used to filter documents where a field's value is less than or equal to a specified value.
    ```js
    db.users.find({ age: { $lte: 30 } });
    ```
    - #### $ne (Not Equal) :
    - Used to filter documents where a field's value does not equal a specified value.
    ```js
    db.users.find({ age: { $ne: 30 } });
    ```
- ### Q. Mention Few Characteristics of MongoDB?
    - MongoDB is a document Oriented NoSQL Database. 
    - It Stores data in BSON(Binary JSON)
    - This BSON Format allows various structers within a collection.
    - #### Key Characteristics of MongoDB:
    - 1. Schema-less : Each document can have a different structure, making it easy to evolve your data model over time.
    - 2. Document-Based: Data is stored in documents that can include nested arrays and sub-documents, allowing for complex data representation.
    - 3. Scalability: MongoDB supports horizontal scaling through sharding, distributing data across multiple servers.
    - 4. Rich Query Language: It provides a powerful query language to perform complex queries, aggregations, and indexing.