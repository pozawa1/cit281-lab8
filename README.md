# Objectives
1. Practive adding fastify and node-fetch require statements
2. Practice fetching JSONPlaceholder data

# Technologies Used
- Terminal 
- VSCode
- Postman

# Part 1
Create a new, empty file called lab-08.js in the cit281/p7/lab8 folder.

# Part 2
Install fastify node-fetch package.

# Part 3
Use the following fastify starter code as the basis of your lab-08.js file contents.
```
// #1 TODO: Declare fastify object from fastify, and execute

// #2 TODO: Declare fetch object from node-fetch

fastify.get("/photos", (request, reply) => {
  // #3 TODO:
  // Adapt the following code to attempt to retrieve
  // all photos from JSONPlaceholder site
  // using fetch, and handle returned Promise using:
  // - two .then() chain methods, return 200
  // - single .catch() chain method, return 404
  reply
  .code(200)
  .header("Content-Type", "text/json; charset=utf-8")
  .send({ error: "", statusCode: 200, photos: [] });
});

fastify.get("/photos/:id", (request, reply) => {
  // #4 TODO:
  // Adapt the following code to attempt to retrieve
  // a single photo from JSONPlaceholder site
  // using fetch, and handle returned Promise using:
  // - single .then() chain method, return 200
  // - single .catch() chain method, return 404
  // You may also try to use Object.keys() to 
  // ensure JSONPlaceholder returns an object with
  // properties. An empty object returned from 
  // JSONPlaceholder means that the passed photo ID
  // was invalid. Your server would also return
  // a 404 status code for an invalid Photo ID.

  const { id = "" } = request.params;  
  reply
  .code(200)
  .header("Content-Type", "text/json; charset=utf-8")
  .send({ error: "", statusCode: 200, photo: {} });
});

// Start server and listen to requests using Fastify
const listenIP = "localhost";
const listenPort = 8080;
fastify.listen(listenPort, listenIP, (err, address) => {
  if (err) {
    console.log(err);
    process.exit(1);
  }
  console.log(`Server listening on ${address}`);
});
```

# Part 4
Add fastify and node-fetch require statements.
```
// #1 TODO: 
const fastify = require("fastify")();

// #2 TODO: 
const fetch = require("node-fetch");
```

# Part 5
Fetch JSONPlaceholder data.
```
// #3 TODO:
fastify.get("/fotos", (request, reply) => {
    fetch("https://jsonplaceholder.typicode.com/photos")
    .then(response => {return response.json()})
    .then(jsonFromResponse => {
        reply
        .code(200)
        .header("Content-Type", "text/json; charset=utf-8")
        .send({ error: "", statusCode: 200, photos: jsonFromResponse });
    })
    .catch(err => {
        reply
        .code(404)
        .header("Content-Type", "text/json; charset=utf-8")
        .send({ error: "", statusCode: 404, photos: [] });
    })   
  });
  
  // #4 TODO:
  fastify.get("/fotos/:id", (request, reply) => {
    // 1) Get information from request
    const { id = "" } = request.params;  
    // 2) Take action
    fetch(`https://jsonplaceholder.typicode.com/photos/${id}`)
    .then(response => {return response.json()})
    // 3) Reply to the client
    .then(jsonFromResponse => {
        reply
        .code(200)
        .header("Content-Type", "text/json; charset=utf-8")
        .send({ error: "", statusCode: 200, photos: jsonFromResponse });
    })
    .catch(err => {
        reply
        .code(404)
        .header("Content-Type", "text/json; charset=utf-8")
        .send({ error: "", statusCode: 404, photos: [] });
    })
  });
```

[Return to Homepage](https://pozawa1.github.io/)
