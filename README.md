# Node-Js-Questions
# What is node JS in simple words?
Node. js (Node) is an open source, cross-platform runtime environment for executing JavaScript code. Node is used extensively for server-side programming, making it possible for developers to use JavaScript for client-side and server-side code without needing to learn an additional language.

# What is Middleware?
Middleware is a function in Node.js <br/>
Operates between the server and routes<br/>
Can process incoming requests before they reach route handler<br/>
Can perform operations such as authentication, logging, validation, etc.<br/>
Middleware functions are executed in the order in which they are added to the request pipeline and can modify the request and response objects, or end the request-response cycle.

>Application level middleware- its Applied All Routes
```
const express = require('express');
const app = express();
const reqFilter = (req, resp, next) => {
    if (!req.query.age) {
        resp.send("Please provide your age")
    }
    else if (req.query.age<18) {
        resp.send("You are under aged")
    }
    else {
        next();
    }
}

app.use(reqFilter);

app.get('/', (res, resp) => {
    resp.send('Welcome to Home page')
});

app.get('/users', (res, resp) => {
    resp.send('Welcome to Users page')
});
app.listen(5000)
```
>group level or single level middleware(example of verifyToken)[Passed this jwtVerification as a parameter in routes in which we want to apply] 
```
function jwtVerification(req,res,next){
    let token = req.headers['authorization']
    if(token){
        token = token.split(' ')[1];
        // console.log("verification",token);
        jwt.verify(token,process.env.jwtKey,(err,valid)=>{
            if(err){
                res.status(401).json({result: "please provide valid token"});
            }else{
                next();
            }
        })
    }else{
        res.status(404).json({result: "please add token with header"});
    }
    
}
```
# Node Js is Single Threaded Or multi-Threaded.
* Node Js is Single Threaded
* Node.js uses an event loop to handle multiple events.
* Node.js is efficient for server-side applications.
* The event loop runs on the main JavaScript thread.
* Node.js relies on JavaScript's single-threaded nature.
* Node.js does not create a separate thread for each connection.
* The event loop is responsible for handling incoming requests and delegating tasks to worker threads.
* Node.js uses an event-driven, non-blocking I/O model.
