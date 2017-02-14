---
title: Making of a GraphQL Server and Meteor cohabit
code: https://github.com/apollographql/meteor-integration/blob/master/main-server.js#L38-49
---

`apollo` allows you to use a handy `createApolloServer` to set up a GraphQL server in your app that will friendly cohabit with your Meteor server.

It is:
* a simple `express` server ...
* ... with a specific endpoint `/graphql` (by default), enhanced with useful middlewares like `bodyParser` & `grapqhlExpress` ...
* ... bound to the `WebApp`, Meteor's HTTP request handler.

You can add any custom middleware on the `express` server thanks to the `configServer` option: enabling CORS with `cors` for instance.

<a href="https://github.com/apollographql/meteor-integration/blob/master/main-server.js#L53-L65"><h4>GraphQL Server Context</h4></a>

Some options are set for you by default, you can overwrite them by giving your own options as an object or a function returning an object.

`apollo` specifically cares about one of these options: `context`. 

The `context` is an object shared by all resolvers in a particular query, and is used on a per-request basis, for instance to initialize user data, caching tools like `DataLoader`, set up some API keys, or anything else that should be taken into account when resolving the query.

<a href="https://github.com/apollographql/meteor-integration/blob/master/main-server.js#L67-L88"><h4>Authenticate the current user</h4></a>

In the eventuality of a login token sent with every queries, it's time to process it!

🤖... String check, ...ok! Hash the token, ...ok! Query `Meteor.users` collection to find the relevant user, ...ok! 🎉 

If the query returns a `user` document and the token isn't expired, `apollo` will automatically assign `userId` & `user` to the `context` object, thus [you can use it in your resolvers](https://github.com/apollographql/meteor-starter-kit/blob/master/imports/api/schema.js#L29-L31)! Great success!

If no user is found, no bother: it just move forward and will try next time.

<a href="https://github.com/apollographql/meteor-integration/blob/master/main-server.js#L93-L96"><h4>Graph<em>i</em>QL</h4></a>

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

<a href="https://github.com/apollographql/meteor-integration/blob/master/main-server.js#L98-L99"><h4>Bind the GraphQL server to Meteor!</h4></a>

This last line put the final touches to the `createApolloServer` function in two steps. 💅

Step one, the `graphQLServer` is wrapped in `Meteor.bindEnvironment` to ensure the code will run in a [`Fiber`](https://github.com/laverdet/node-fibers), keeping consistency with the Meteor server-side environment.

Step two, the `graphQLServer` is attached to the Meteor's `WebApp.connectHandlers`, which process incoming HTTP requests.

➡️ The server is ready for consumption! You can [setup your schema & resolvers](http://dev.apollodata.com/core/meteor.html#Server)!
