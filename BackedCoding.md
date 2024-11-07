### Q. Create a RESTful API that perform crud opearations on application. The API should support the following operations: create, read, update, and delete to-do items. How would you structure your routes, controllers, and models?
```js
const express= require("express")
const mongoose= require("mongoose")
const  app= express()

const mongooseConnect= async ()=>{
    try {
        await mongoose.connect("mongodb://localhost:27017/test", {
            useNewUrlParser:true,
            useUnifiedTopology:true
        })
        console.log("Connected Successfully to MongoDB");
    } catch (error) {
        console.log("Error while connecting to Mongo" +error
        )
    }
}

mongooseConnect();

const userSchema= new mongoose.Schema({
    empId: { type: Number, required: true },
    name: { type: String, required: true },
    dept: { type: String, required: true },
    age: { type: Number },
    position: { type: String }
},{collection:"users"})

const User= mongoose.model("User",userSchema)
app.use(express.json());

app.post("/todos",async (req,res)=>{
    const {empId, name, dept, age, position}= req.body;
    try {
        const data= await User.findOneAndUpdate(
            {empId},
            {name, dept, age, position},
            {new:true, upsert:true})
        res.status(200).json({
            message:"Users Added Successfully", data
        })
    } 
    catch (error) {
        console.log("Error while saving user"+error);
        res.status(500).json(
            {
                message:"Error while saving user"+error
            }
        )
    }
})

app.get("/todos", async(req,res)=>{
    try {
        const data= await User.find()
        res.status(200).json({
            message:"User Details are",
            data:data
        })
    } catch (error) {
        console.log("Error while Fetching the records"+error)
        res.status(500).json({
            message:"Error while Fetching the records"+error
        })
    }

})

app.patch("/todos/:id", async(req,res)=>{
    const id= req.params.id
    try {
        const data= await User.updateOne(
           {empId:id},
            {dept:req.body.dept},
            {new:true}
        )
        res.status(200).json({
                message:"Updated request done",
                data:data
            })
    } catch (error) {
        console.log("Error while updating the records"+error)
        res.status(500).json({
            message:"Error while updating the records"+error
        })
    }
})

app.delete("/todos/:id", async(req,res)=>{
    const id= req.params.id
    try {
        const data=await User.deleteOne({empId:id})
        res.status(200).json({
            message:"User Deleted Successfully",
        })
    } catch (error) {
        console.log("Unable to Delete the User")
        res.send(500).json({
            message:"Unable to Delete the User",
        })
    }
})
app.listen(8000, ()=>{
    console.log("Server running on port 8000")
})
```

- ### Q. How would you implement logging in your Express application? Discuss the libraries you would use (e.g., Winston, Morgan) and how you would set up monitoring for performance and errors.
```js
const winston= require("winston");

const logger= winston.createLogger({
    level:"info",
    format:winston.format.json(),
    transports:[
        new winston.transports.File({
            filename:"customer.log",
            level:"info"
    }),
    new winston.transports.File({
        filename:"error.log",
        level:"error"
    })
    ]
})
```

- ### Q. Implement Authentication logic, hash the password and save it.

```js

const express= require("express")
const mongoose= require("mongoose")
const winston= require("winston")
const bcrypt= require("bcrypt")
const jwt=require("jsonwebtoken")
const dotenv= require("dotenv").config()
const  app= express()
const logger= winston.createLogger({
    level:"info",
    format:winston.format.json(),
    transports:[
        new winston.transports.File({
            filename:"customer.log",
            level:"info"
    }),
    new winston.transports.File({
        filename:"error.log",
        level:"error"
    })
    ]
})

const mongooseConnect= async ()=>{
    try {
        await mongoose.connect("mongodb://localhost:27017/test", {
            useNewUrlParser:true,
            useUnifiedTopology:true
        })
        console.log("Connected Successfully to MongoDB");
        logger.info("Connected Successfully to MongoDB")
    } catch (error) {
        console.log("Error while connecting to Mongo" +error
        )
    }
}

mongooseConnect();

const loginSchema = new mongoose.Schema({
    username:{type:String, required:true, unique:true},
    password:{type:String, required:true}
})

loginSchema.pre("save", async function (next) {
    this.password= await bcrypt.hash(this.password,10)
    next();
}
)
const Login = mongoose.model("Login", loginSchema)

app.use(express.json());

app.post("/register", async(req, res)=>{
    const {username, password} = req.body
    try {
        const data= new Login({username:username, password:password})
        await data.save()
        logger.info(data)
        res.status(200).json({
            message:"User Registered Successfully"
        })
    } catch (error) {
        logger.error("Registration  Failed")
        res.status(500).json({
             message:"Registration  Failed"+error
        })
    }
})

app.post("/login", async(req,res)=>{
    const {username, password}= req.body
    try {
        const user= await Login.findOne({username:username})
        logger.info(user)
        
        if(!user){
            logger.error("Invalid Credentails, No users found")
            return res.status(401).json({
                message:"Invalid Credentails, No users found"
            })
        }

        const checkPassword= await bcrypt.compare(password, user.password)

        if(!checkPassword){
            logger.error("Wrong Password")
           return res.status(401).json({
                message:"Wrong Password"
            })
        }

        const token = jwt.sign({id:user._id},process.env.secretKey, {expiresIn:"1h"})
        res.status(200).json({token})
    } catch (error) {
        logger.error("Login Failed")
        res.status(500).json({
             message:"Login Failed"
        })
    }
})

app.listen(8000, ()=>{
    console.log("Server running on port 8000")
})
```

