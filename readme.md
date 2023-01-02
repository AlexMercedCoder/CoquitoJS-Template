[CoquitoJS Documentation](https://www.npmjs.com/package/coquito)

## Template Documentation

### What's setup
- RPC SERVER and CLIENT if not building a seperate frontend
- GraphQL Server and Client if not build a seperate frontend
- Template routers, rpc actions, and graphql resolvers to use as an example to build out what your app needs
- ejs is configured by default for server side rendering, use the head.ejs partial to auto-loads the rpc and graphql clients.
- Look at an example of the use of the RPC and GraphQL clients in `public/app.js` and see an example use of the ejs partial in `views/index.ejs`
- `cors.js` for defining your cors whitelist which is only used if NODE_ENV is set to `production`

#### How the GraphQL API Works

[GraphQL Documentation (how to write resolvers and functions)](https://graphql.org/learn/)

1. Define the functions that should handle your GraphQL queries in the ./graphql/rootValue.js file. The express req, res object will be inside the context argument of the graphql resolver.

2. Define your API's schema in ./graphql/schema.js

The api is accessed by making post requests to /graphql with a json body with a query property that is your graphql query string. GraphQL clients should automatically do this, you'll just have to provide the client the url and the query string. (Popular Javascript clients include Apollo and Relay)

[GraphQL Bin - Great Tool for Testing your GraphQL API](https://www.graphqlbin.com/v2/new)

If you need to register any middleware specifically on the /graphql router pass a function under the gqlhook property in the CoquitoApp constructor. The function takes the router as an argument and in the function you can do whatever you like with it (mainly regiser middleware).

#### How the SimpleRPC API Works

- [SimpleRPC Server Library](https://www.npmjs.com/package/@alexmerced/simplerpc-server)
- [SimpleRPC Client Library](https://www.npmjs.com/package/@alexmerced/simplerpc-client)

The functions that can be called are all defined in ./rpc/actions.js, these functions get two arguments.

- payload (data that is passed from the client dispatch call)
- context (includes data in ./rpc/context.js plus the express req/res objects)

These functions are called by making post requests to /rpc with a request body following this shape:

```json
{
    "type":"functionName",
    "payload":{
        "arg1": "something",
        "arg2": "something else"
    }
}
```

Type is used to determine which function is called, and the payload object is passed to it. There is a javascript frontend client

If you need to register any middleware specifically on the /rpc router pass a function under the rpchook property in the CoquitoApp constructor. The function takes the router as an argument and in the function you can do whatever you like with it (mainly regiser middleware).