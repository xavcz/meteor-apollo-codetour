---
title: Asking for data client-side with Apollo Client
code: https://github.com/apollographql/meteor-integration/blob/master/main-client.js#L8-L14
---

`apollo` helps you for configuring an Apollo Client instance in ~100 lines of code in three main steps, plus optional configuration that you can modify. Let's walk these steps from the inside to the outside.

<a href="https://github.com/apollographql/meteor-integration/blob/master/main-client.js#L19-L43"><h4>Network interface configuration</h4></a>

Apollo Client has a pluggable network interface layer, and `apollo` leverages it. The [`BatchingNetworkInterface`](http://dev.apollodata.com/core/network.html#query-batching) is used by default, and you can also use the classic `NetworkInterface` by setting `batchingNetworkInterface` to `false` in your configuration options.

The default endpoint where queries are sent is your Meteor app's `ROOT_URL` + `/graphql`. For example, in development mode: `http://localhost:3000/graphql`. It's also editable in your configuration options.

<a href="https://github.com/apollographql/meteor-integration/blob/master/main-client.js#L45-L78"><h4>User Accounts Middleware</h4></a>

Meteor's account system if often _referred as magic_: it is awesome and that would be a shame to throw it away just because we use GraphQL.

In a nutshell, the current user is recognized in a client-session thanks to a login token, usually stored in the browser's local storage. It can also be stored in a cookie, for example thanks to `meteorhacks:fast-render`.

`apollo` takes care of sending the right login token with every request for us, if `useMeteorAccounts` is set to true (default value) and if it exists! A custom middleware catch the login token & modify the request before the request is sent over the wire. 🚀

<a href="https://github.com/apollographql/meteor-integration/blob/master/main-client.js#L83-L98"><h4>Configure the Apollo Client</h4></a>

Last but not least, it's time to use this super network interface in our Apollo Client, in addition to some other great options.

The Apollo Client can be exported server-side to achieve server-side rendering. `apollo` automatically recognizes the environment and sets the `ssrMode` accordingly.

`apollo` takes advantages of the [store normalization](http://dev.apollodata.com/core/how-it-works.html#query-benefits): it references every object result with their typename, which can be for instance a collection name, combined with their unique Mongo `_id`.

All good? Let's hop in the server-side configuration!
