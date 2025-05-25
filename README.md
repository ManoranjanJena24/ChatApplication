# ChatApplication

## Backend
 -> npm i express mongoose dotenv jsonwebtoken bcryptjs cookie-parser cloudinary socket.io

 ->  npm i nodemon -D

 | Type              | Used For                         |
| ----------------- | -------------------------------- |
| `dependencies`    | Needed to **run** the app        |
| `devDependencies` | Needed to **build/test/develop** |


npm i nodemon -D
what is the use of dev dependecies in easy words tell

❓Why?
Because nodemon is only used to restart the server automatically when you make changes in development.

🚀 In production:
Your real users don’t need nodemon.

It makes your app lighter and faster by excluding unneeded tools.

Summary:
Type	Used For
dependencies	Needed to run the app
devDependencies	Needed to build/test/develop


----------------------------------------------------------------------------------------------------------------------

Added the line   "type":"module",


to convert the 

const express =require("express")

const app = express();


app.listen(5001,()=>{
    console.log("Server is running on port 5001")
})



to 
----------------------------------------------------------------------------------------------------------------------

created the 4 folders inside the self created src folder controllers, lib,middleware,models,routes





import authRoutes from "./routes/auth.route.js"
## since it is a local file we have to to add the extension in the end 




MONGODB_URI=mongodb+srv://manoranjanjenamitsy17:5W6qluxrKlh9ChD8@cluster0.m3fwtk3.mongodb.net/?retryWrites=true&w=majority&appName=Cluster0


before this ? write the database name otherwise it will take it as test


MONGODB_URI=mongodb+srv://manoranjanjenamitsy17:5W6qluxrKlh9ChD8@cluster0.m3fwtk3.mongodb.net/**chat_db**?retryWrites=true&w=majority&appName=Cluster0



-------------------------------------------------------------------------------------------

**user.model.js**
->we have to insert the const User = mongoose.model("**User**",userSchema);

this **User should be singular and upper case first alphabet**






Absolutely! Let's break this line down:

```js
const User = mongoose.model("User", userSchema);
export default User;
```

This line does **two things**:

---

### ✅ 1. `mongoose.model("User", userSchema)`

This **creates a Mongoose model**.

* `mongoose.model()` is a function provided by the **Mongoose** library.
* It takes two arguments:

  1. `"User"` — the **name of the model**.
  2. `userSchema` — the **schema** that defines the structure of the documents in the MongoDB collection.

> 💡 Behind the scenes, Mongoose **automatically converts** the name `"User"` to lowercase and pluralizes it to **`users`**, which is the name of the MongoDB collection it interacts with.

So this line tells Mongoose:

> "Create a model named `User` based on the structure defined in `userSchema`, and link it to the `users` collection in MongoDB."

Example:

```js
const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  password: String
});
const User = mongoose.model("User", userSchema);
```

---

### ✅ 2. `export default User`

This **exports the model**, so you can import it and use it in other files.

For example, in your `controller` or `routes` file, you might use:

```js
import User from "../models/userModel.js";

const user = await User.findOne({ email: "abc@example.com" });
```

---

### 🔁 Summary:

| Part                                 | Purpose                                                   |
| ------------------------------------ | --------------------------------------------------------- |
| `mongoose.model("User", userSchema)` | Creates the `User` model for interacting with MongoDB     |
| `export default User`                | Makes the `User` model usable in other files via `import` |

Let me know if you want a quick visual explanation of how this works with a collection.



-----------------------------------------------------------------------------------------------------------------------------------


to grab 
 const {fullName,email,password}=req.body
 we need to add middleware in the index.js



#### "app.use(express.json()) allows Express to parse JSON data sent in HTTP request bodies and make it available on req.body.



step by step 
step 1 : create the user
step 2 :hash the password 
step 3:create token to authenticate that   




Great! Let's walk through a **realistic example** of how salt affects the hash, using actual values.

---

### 🧠 Think of this:

We're taking the password `"mysecret123"` and adding a **random salt** to it before hashing.

---

### ✅ Example (Manual Conceptual Version):

Let's pretend:

* Password = `"mysecret123"`
* Random Salt 1 = `"abc123salt"`
* Random Salt 2 = `"xyz789salt"`

---

Now, we “simulate” the hash like this:

```plaintext
hash("mysecret123abc123salt") → Hash1 = "e91a3e...abc"
hash("mysecret123xyz789salt") → Hash2 = "b82e7c...xyz"
```

**Even though the password is the same**, the salts are different — so the final hash output is completely different.

---

### ✅ Real Code Example (With bcrypt):

```js
const bcrypt = require('bcrypt');

const password = 'mysecret123';

async function run() {
  const salt1 = await bcrypt.genSalt(10);
  const hash1 = await bcrypt.hash(password, salt1);

  const salt2 = await bcrypt.genSalt(10);
  const hash2 = await bcrypt.hash(password, salt2);

  console.log("Salt 1:", salt1);
  console.log("Hash 1:", hash1);

  console.log("Salt 2:", salt2);
  console.log("Hash 2:", hash2);
}

run();
```

---

### 🧾 Sample Output:

```
Salt 1: $2b$10$KbM3pUNFkA6nQ5b8Zgacwe
Hash 1: $2b$10$KbM3pUNFkA6nQ5b8Zgacwe0vhHdz7vMTJcKRMtdd.Mo3UzN.1dz0S

Salt 2: $2b$10$wXzfhykDeUlEIjXuj9mfZu
Hash 2: $2b$10$wXzfhykDeUlEIjXuj9mfZuJMPFroV9v6vZuvM10jAxPoxzhBNY6pO
```

Notice:

* `Hash 1` and `Hash 2` are completely different.
* Why? Because `Salt 1` and `Salt 2` are different.

---

### ✅ Bottom Line:

Adding a **unique salt** to every password:

* Prevents duplicate hashes
* Makes your app more secure
* Ensures even the same passwords look different when hashed

---

Would you like a visual analogy, like cooking or padlocking, to understand salt better?



----------------------------------------------------------------------------------------------------------------------------


export const protectRoute =async(req,res)=>{
    try {
        const token = request.cookies.**jwt**
    } catch (error) {
        
    }
}

#### this **jwt** comes from given higlighted the name u give there same name will be given here also



import jwt from "jsonwebtoken"

export const generateToken=(userId,res)=>{
const token =jwt.sign({userId},process.env.JWT_SECRET,{
    expiresIn:"7d"
})
// once we decode this we can really see which belongs to the token 

res.cookie("**jwt**",token,{
    maxAge: 7*24*60*60*1000, //ms
    httpOnly:true, //prevent XSS attacks cross-site scripting attacks
    sameSite:"strict", //CSRF attacks cross-site request forgery attacks
    secure:process.env.NODE_ENV !== "development"
})

return token 

}

----------------------------------------------------------------------------------------

to grab the token from the cookies we need the cookie parser in protected route we are using so add on index.js



UNDER SETTINGS IN CLOUDINARY GOING TO API KEYS SECTION 




----------------------------------------------------------------------------------------------------------------------


so whenever we are refreshing our application we will be calling this function router.get("/check",protectRoute,checkAuth)





----------------------------------------------------------------------------------------------------------------------



const messageSchema=new mongoose.Schema(
{
senderId:{
type:mongoose.Schema.Types.ObjectId,
ref:'User',
required:true,

},
receiverID:{
    type:mongoose.Schema.Types.ObjectId,
    ref:"User",
    required:true
},
text:{
    type:String
},
image:{
    type:String
},


},{
    timestamps:true
}  

)

const Message = mongoose.model("Message",messageSchema);
export default Message;



This basically just tells to mongodb that that senderId and receiverId will bee reference to **User** model


text and image will not be required true because  some messages will be only text and some wiuloll be image and some will be both

 

