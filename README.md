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

# What is the event-driven, non-blocking I/O model in Node.js and why is it important?
>The event-driven, non-blocking I/O model in Node.js is a design pattern that allows the server to handle multiple requests simultaneously without blocking. Instead of waiting for a long-running process to complete, its moving on to the next request, Node.js uses non-blocking I/O operations and an event loop to process multiple requests in parallel. This makes the server more efficient and able to handle a large number of simultaneous connections.

# What is the difference between synchronous and asynchronous programming?
>Synchronous programming is a blocking, sequential execution of code where the next line of code can only be executed after the previous line has completed. In asynchronous programming, multiple operations can run simultaneously and the next line of code can be executed before the previous operation has completed. This allows for more efficient use of resources and enables the program to continue executing while waiting for slow operations to complete.

# Node js is Synchronous or Asyncronous
>Node.js is asynchronous. It uses an event-driven, non-blocking I/O model that allows it to handle multiple requests simultaneously without blocking. This means that multiple operations can run in parallel and the program can continue executing while waiting for slow operations to complete, making it more efficient and scalable.
-Example code
```
console.log("start executing")      
setTimeout(()=>{
    console.log("execution runing")
},0)
console.log("execution complete")

OUTPUT-
start executing
execution complete
execction running
```
- Drawback of Asynchonous
```
let a=10;
let b=0;
setTimeout(()=>{
    b=20
},0)
console.log(a+b);

OUTPUT-
10
```
- To handle this problem we can use Promises or callback function (but promise modern)
```
let a=10;
let b=0;

let waitingData=new Promise((resolve,reject)=>{
    setTimeout(()=>{
        b=20;
    },2000)
})

waitingData.then((data)=>{
    b=data;
    console.log(a+b);
})
```

# How can handle Errors in Node Js?
>Errors in Node.js can be handled using a try-catch statement, by passing a callback function to handle errors in asynchronous functions, or by emitting an 'error' event and listening for it using an 'error' listener. 

# what is Promises?
>Promises in Node.js are objects representing the eventual completion or failure of an asynchronous operation. They provide a way to register callbacks for success or failure and simplify the handling of asynchronous operations with a cleaner syntax. Promises have three states: pending, resolved, and rejected, and can be used with the then() and catch() Or Async await methods to handle the result or error of the asynchronous operation.

# How Node Js Work
<img width="692" alt="Screenshot_20230208_131636" src="https://user-images.githubusercontent.com/106628860/217553322-acc500bd-8d21-498c-a9b2-6e5c0e2ee8b7.png">
<img width="648" alt="Screenshot_20230208_131708" src="https://user-images.githubusercontent.com/106628860/217554057-5464d0c6-6fce-426b-9b2c-cca002bbbfd9.png">
<img width="679" alt="Screenshot_20230208_131600" src="https://user-images.githubusercontent.com/106628860/217554150-d571a669-b731-4d32-8a5c-79c379fabdb8.png">


