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