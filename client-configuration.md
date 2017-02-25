---
title: Asking for data client-side with Apollo Client
code: https://github.com/apollographql/meteor-integration/blob/master/main-client.js#L10-L24
---

`apollo` helps you for configuring an Apollo Client instance in three main steps with default configuration that you can extend or replace. Let's walk these steps from the inside to the outside.

<a href="https://github.com/apollographql/meteor-integration/blob/master/main-client.js#L26-L43"><h4>Network interface configuration</h4></a>

Based on the `defaultNetworkInterfaceConfig` and your possible `customNetworkInterfaceConfig`, `createMeteorNetworkInterface` will create a configurable network interface that fits the requirement of your Meteor app.

The default endpoint where queries are sent is your Meteor app's `ROOT_URL` + `graphql`. For example, in development mode: `http://localhost:3000/graphql`. You can specify a custom endpoint to query by passing any `uri` field in your `customNetworkInterfaceConfig` object.

Apollo Client has a pluggable network interface layer, and `apollo` leverages it. The [`BatchingNetworkInterface`](http://dev.apollodata.com/core/network.html#query-batching) is used by default, and you can also use the classic `NetworkInterface` by setting `batchingNetworkInterface` to `false` in your configuration options.

<a href="https://github.com/apollographql/meteor-integration/blob/master/main-client.js#L45-L86"><h4>User Accounts Middleware</h4></a>

Meteor's account system if often _referred as magic_: it is awesome and that would be a shame to throw it away just because we use GraphQL.

In a nutshell, the current user is recognized in a client-session thanks to a login token, usually stored in the browser's local storage. 

`apollo` takes care of sending the right login token with every request for us, if `useMeteorAccounts` is set to true (default value) and if it exists! A custom middleware catch the login token & modify the request before the request is sent over the wire. 🚀

The login token can also be stored in a cookie, for example thanks to `meteorhacks:fast-render`, that will then be passed to the Apollo Client `customNetworkInterfaceConfig` when doing server-side rendering.

<a href="https://github.com/apollographql/meteor-integration/blob/master/main-client.js#L92-L115"><h4>Configure the Apollo Client</h4></a>

Last but not least, it's time to use this network interface in our Apollo Client, in addition to some other great options.

The Apollo Client can be exported server-side to achieve server-side rendering. `apollo` automatically recognizes the environment and sets the `ssrMode` accordingly.

`apollo` takes advantages of the [store normalization](http://dev.apollodata.com/core/how-it-works.html#query-benefits): it references every object result with their typename, which can be for instance a collection name, combined with their unique Mongo `_id`.

As for the `createMeteorNetworkInterface`, you can extend or replace any options by passing a `customClientConfig` object to `meteorClientConfig`.

All good? Let's hop in the server-side configuration!
