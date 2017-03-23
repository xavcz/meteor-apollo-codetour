---
title: Making a GraphQL Server and Meteor cohabit
code: https://github.com/apollographql/meteor-integration/blob/master/src/main-server.js#L16-L46
---

`apollo` allows you to use a handy `createApolloServer` to set up a GraphQL server in your app that will friendly cohabit with your Meteor server. It is a simple `express` server enhanced with `graphqlExpress` middleware.

The `createApolloServer` has two defaults configuration objects, one for the `express` server, and one for the `graphqlExpress` middleware.

<a href="https://github.com/apollographql/meteor-integration/blob/master/main-server.js#L46-L62"><h4>Express Server Configuration</h4></a>

Based on the `defaultServerConfig` and your possible `customServerConfig`, `createApolloServer` will setup an `express` server. You can extend the server configuration with a `configServer` function on `customServerConfig`. It could be useful for instance to enable CORS or prepare the request before it hits the GraphQL endpoint.

Speaking about the GraphQL endpoint, it is defined `/graphql` by default. Original, isn't it?

<a href="https://github.com/apollographql/meteor-integration/blob/master/main-server.js#L62-L73"><h4>GraphQL Endpoint Configuration</h4></a>

The GraphQL endpoint is a combination of `body-parser` & `graphqlExpress` middlewares. The former parses requests to exploitable JSON objects & the latter handles the requests in accordance with your schema to get the relevant data.

`graphqlExpress` options are based on the default `defaultGraphQLOptions` and extendable/replaceable as similar as for the server config thanks to `customOptionsObject`. 

The GraphQL server specifically cares about one of these options: `context`. By default, it's an empty object.

The `context` is an object shared by all resolvers in a particular query, and is used on a per-request basis, for instance to initialize user data, caching tools like `DataLoader`, set up some API keys, or anything else that should be taken into account when resolving the query.

Moreover, this is on the `customOptionsObject` that you pass a GrahQL `schema` created thanks to `makeExecutableSchema` to get data from your various backends.

<a href="https://github.com/apollographql/meteor-integration/blob/master/main-server.js#L75-L114"><h4>Authenticate the current user</h4></a>

In the eventuality of a login token sent with every queries, it's time to process it!

🤖 String check, ...ok! 

🤖 Hash the token, ...ok! 

🤖 Run a query on `Meteor.users` collection to find the relevant user, ...ok! 

If the query returns a `currentUser` document and the token isn't expired, `apollo` will automatically assign `userId` & `user` to the `context` object, thus [you can use it in your resolvers](https://github.com/apollographql/meteor-starter-kit/blob/master/imports/api/schema.js#L29-L31)! Great success! 🎉

If no user is found, no bother: it just move forward and will try next time. ✌️

<a href="https://github.com/apollographql/meteor-integration/blob/master/main-server.js#L128-L137"><h4>Graph<em>i</em>QL</h4></a>

There is another nitty-gritty feature this package enables for you: Graph<em>i</em>QL. It is a graphical interactive in-browser GraphQL IDE. It is perfect to test what you are building. 

If you've never used it, you can give it a try [on a live demo with the Star Wars API](http://graphql.org/swapi-graphql/) and start with this query example: 
```graphql
query {
  allFilms {
    films {
      title
    }
  }
}
```

Graph<em>i</em>QL is by default enabled in development, and disabled in production.  

<a href="https://github.com/apollographql/meteor-integration/blob/master/main-server.js#L139-L140"><h4>Bind the GraphQL server to Meteor!</h4></a>

This last line put the final touches to the `createApolloServer` function in two steps.

Step one, the `graphQLServer` is wrapped in `Meteor.bindEnvironment` to ensure the code will run in a [`Fiber`](https://github.com/laverdet/node-fibers), keeping consistency with the Meteor server-side environment.

Step two, the `graphQLServer` is attached to the Meteor's `WebApp.connectHandlers`, which process incoming HTTP requests.

➡️ The server is ready for consumption! You can [setup your schema & resolvers](http://dev.apollodata.com/core/meteor.html#Server)!
