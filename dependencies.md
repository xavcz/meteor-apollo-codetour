---
title: Dependencies you should be aware of
code: https://github.com/apollographql/meteor-integration/blob/master/src/check-npm.js#L4-L16
---

Welcome to the Meteor ↔️ Apollo integration codetour! 🎉

This package, `apollo`, is **essentially** preparing the Apollo client & server tools for you to use them the easiest way possible. 

**The goal of this codetour is to demistify how to implement these tools in a Meteor app.** 

Let's have a brief look at the tools we are relying on to power the `apollo` package.

<a href="https://github.com/apollographql/meteor-integration/blob/master/src/check-npm.js#L6-L7"><h3>Client-side dependencies</h3></a>

The `apollo-client` is is our founding stone client-side. From the docs: it is a library, a vanilla JavaScript GraphQL client that can be used independent of any other framework. Apollo Client also serves as the core library used by various JavaScript integrations, including _React Apollo_, _Angular2 Apollo_ or _Blaze Apollo_.

`isomorphic-fetch` is used to polyfill `fetch` as a global so that its API is consistent between client and server. Some browsers like IE11 doesn't include it, and it doesn't exist by default server-side. `fetch` is used internally by Apollo Client.

To install the client-side dependencies:
```sh
npm install --save apollo-client isomorphic-fetch
```

<a href="https://github.com/apollographql/meteor-integration/blob/master/src/check-npm.js#L11-L15"><h3>Server-side dependencies</h3></a>

<h4>`graphql` & `grapqhl-tools`</h4>

Firt of all, `graphql` is the JavaScript reference implementation for GraphQL: **GraphQL.js**. It provides two important capabilities: building a type schema, and serving queries against that type schema.

It is enhanced by `graphql-tools`, a package that enables you to build a production-ready GraphQL.js schema using the GraphQL schema language, rather than using the GraphQL.js type constructors directly. Easy peasy!

<h4>`graphql-server-express` & stooges</h4>

There are [several implementations of the Graphql server](https://github.com/apollostack/graphql-server) by the Apollo community. They all rely on Node.js HTTP server frameworks.

The Meteor `apollo` package relies on the infamous `express`, combined with `body-parser`, a middleware used to parse incoming POST requests bodies to JSON.

Parsed requests from the `apollo-client` are then sent to the `graphql-server-express`, as we'll see later on.

To install them all:
```sh
npm install --save graphql graphql-tools graphql-server-express express body-parser
```

Let's now have a look at how we configure the Apollo client with `apollo`! 🤔
