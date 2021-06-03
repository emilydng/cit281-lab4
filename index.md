## Lab 4

``` markdown
Goals and Outcomes

  - Create initial Fastify Node.js web server
  - Initialize as a Node.js project folder using Node Package Manager (npm)
  - Add Fastify to project using npm, and test using Visual Studio Code (VSCode)
  - Add git repo, exclude node_modules folder from git, make commits
  - Fix MIME error, test, and commit
  - Add a second route with query parameters, test, and commit

```

Lab-04.js

```rouge
  `/*
    CIT 281 Lab 4
    Name: Emily Deng
*/

// Require the Fastify framework and instantiate it
const fastify = require("fastify")();
// Handle GET verb for / route using Fastify
// Note use of "chain" dot notation syntax
fastify.get("/", (request, reply) => {
  reply
    .code(200)
    .header("Content-Type", "text/html; charset=utf-8")
    .send("<h1>Hello from Lab 4!</h1>");
});

// Route for /name
fastify.get("/name", (request, reply) => {
    //(A) Getting information from the requester
    const {first, last} = request.query;
    console.log(first, last);

    // (B) Transforming the request into useful infprmation
    const name = first && last ? `${first} ${last}` : `Guest`;

    // (C) Using the transformed data to inform our response to the client
    reply
      .code(200)
      .header("Content-Type", "text/html; charset=utf-8")
      .send(`<h1>Hello, ${name}</h1>`);
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
});`

```
