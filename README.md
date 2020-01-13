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
