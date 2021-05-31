# Lab 8

## Objectives
1. Practive adding fastify and node-fetch require statements
2. Practice fetching JSONPlaceholder data

## Technologies Used
- Terminal 
- VSCode
- Postman

## Source Code
```
const fastify = require("fastify")();
const fetch = require("node-fetch");

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
  
  fastify.get("/viewphotos/:id", (request, reply) => {
    // 1) Get information from request
    const { id = "" } = request.params;  
    // 2) Take action
    fetch(`https://jsonplaceholder.typicode.com/photos/${id}`)
    .then(response => {return response.json()})
    // 3) Reply to client
    .then(jsonFromResponse => {
        reply
        .code(200)
        .header("Content-Type", "text/html; charset=utf-8")
        .send(`<html><body><h1>${jsonFromResponse.title}</h1><img src = ${jsonFromResponse.url}</body></html>`);
    })
    .catch(err => {
        reply
        .code(404)
        .header("Content-Type", "text/json; charset=utf-8")
        .send({ error: "", statusCode: 404, photos: [] });
    })
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
