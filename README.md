# Swagger2graphQL

Swagger2graphQL wraps your existing Swagger schema to GraphQL types where resolvers perform HTTP requests to certain real endpoints.
It allows you to move your API to GraphQL with nearly zero afford and maintain both: REST and GraphQL APIs.


## Usage

```js
const express = require('express');
const app = express();
var graphqlHTTP = require('express-graphql');
var graphql = require('graphql');
var graphQLSchema = require('swagger-to-graphql');

graphQLSchema('./petstore.json').then(schema => {
  app.use('/graphql', graphqlHTTP(() => {
    return {
      schema,
      context: {
        GQLProxyBaseUrl: API_BASE_URL
      },
      graphiql: true
    };
  }));

  app.listen(3009, 'localhost', () => {
    console.info(`API is here localhost:3009/graphql`);
  });
}).catch(e => {
  throw e;
});
```
