# Web-API-Node---Build-a-Web-API---Intro-to-NodeJs-and-Express
Web API: Node - Build a Web API - Intro to NodeJs and Express

#### Q: What is Node.js?  
#### A: Node.js is a runtime environment (a program that runs other programs), a platform used to execute JavaScript applications outside the browser.

Some of the advantages of using Node.js for writing server side code are:    

- JavaScript on the server: use the same programming language and paradigm for both client and server. This minimizes context switching and makes it easy to share code between the client and the server.    
- Single-threaded: removes the complexity involved in handling multiple threads.    
- Asynchronous: can take full advantage of the processor it’s running on. This matters because the node process will be running on a single CPU.    
- Npm repository: access the largest ecosystem of useful libraries (most of them free to use) in the form of npm modules.    

Some of the disadvantages of using Node.js for writing server-side code are:    

- JavaScript on the server: we lose the ability to use the right tool (language) for the job.    
single-threaded: can’t take advantage of servers with multiple cores/processors.    
- Asynchronous: it is harder to learn for developers that have only worked with languages that default to synchronous operations that block the execution thread.    
- npm repository: too many packages that do the same thing makes it harder to choose one and, in some cases, may introduce vulnerabilities into our code.    


#### Q: What is Express?
#### A: Express is a light and unopinionated framework that sits on top of Node.js and makes it easier to create web applications and services. 

Some of the benefits of using Express are that it is:    

- Simple    
- Unopinionated    
- Extensible    
- Light-weight    
- Compatible with connect middleware. (This means we can tap into an extensive collection of modules written for connect.)    
- All packaged into a clean, intuitive, and easy to use API.    
- Abstracts away common tasks (writing web applications can be verbose, hence the need for a library like this)    


### Working with Express

1. At the terminal ```npm init```   This will create a package.json.  A list of questions will come up.
   You can make the entry point "server.js" w/o quotes.    
2. Now install express ```npm install express```    
3. This is without routers, modules, etc

```
// Bring in express
const express = require("express")
// Bring in database
let db = require('./database')

// Create an instance of express
const app = express();

// middleware
app.use(express.json())


// create a route
app.get("/", (req, res) => {
    res.send("This is live")
})

app.get("/lambda", (req, res) => {
    res.redirect("https:/lambdaschool.com")
})

app.get("/users", (req, res) => {
    res.json(db)
})

app.get("/users/:id", (req, res) => {
    const user = db.find(row => row.id === req.params.id)

    if(user){
        res.json(user)
    } else {
        res.status(404).json({ error: "User not found" })
    }
})

app.post("/users", (req, res) => {
    if(!req.body.name){
        return res.status(400).json({ error: "need a user name"})
    }
    const newUser = {
        id: String(db.length + 1),
        name: req.body.name
    }
    db.push(newUser)
    res.status(201).json(newUser)
})

app.delete("/users/:id", (req, res) => {
    const user = db.find(row => row.id === req.params.id)

    if(user){
        db = db.filter(row => row.id !== req.params.id)
        res.json(user)
    } else {
        res.status(404).json({ error: "User not found" })
    }
})

// Set the listening port
const PORT = 5000

// Listen for the port
app.listen(PORT, () => {
    console.log(`console is running on port ${PORT}`)
})
```

#### This is using routers, modules, knex, ect
```
// https://www.youtube.com/watch?v=2poEnenm9pE&feature=youtu.be

// bring in express
const express = require('express');

// bring in db
const db = require('./data/hubs-model.js')

// create server
const server = express();

// middleware - body parser
server.use(express.json())

// request handler
server.get("/", (req, res) => {
    res.send('Hi there')
})

// request date
server.get("/now", (req, res) => {
    const date = new Date().toISOString();
    res.send(date)
})

// Get /hubs
server.get('/hubs', (req, res) => {
    db.find()
    .then(hubs => {
        res.json(hubs)
    })
    .catch(err => {
        res.status(500).json({ err: err})
    })
})

// Post /
server.post('/hubs', (req, res) => {
    const newHub = req.body;
    db.add(newHub)
    .then(hub => {
        res.status(201).json(hub)
    })
    .catch(err => {
        res.status(500).json({
            err: err,
            message: 'failed to create new hub'
        })
    })
})


// Delete /hubs/:id
server.delete('/hubs/:id', (req, res) => {
    const {id} = req.params;

    db.remove(id)
    .then(deletedHub => {
        if(deletedHub){
            res.json(deletedHub)
        }else{
            res.status(404).json({
                message: 'invalid hub id'
            })
        }
    })
    .catch(err => {
        res.status(500).json({
            err: err,
            message: 'failed to delete hub'
        })
    })
})

// Put /hubs/:id

server.put('/hubs/:id', (req, res) => {
    const {id} = req.params;
    const changes = req.body 

    db.update(id, changes)
    .then(updated => {
        if(updated){
            res.json(updated)
        } else {
            res.status(404).json({
                message: 'invalid hub id'
            })
        }
    })
    .catch(err => {
        res.status(500).json({
            err: err,
            message: 'failed to update hub'
        })
    })
})

// listen for server and give it a port
server.listen(4000, () => {
    console.log('Server is running on port 4000...')
})
```



