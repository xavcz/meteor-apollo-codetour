---
title: Using the package and moving forward
code: https://github.com/apollographql/meteor-integration/blob/master/README.md#1-20
---

Hopefully, you now have a **better understanding of what "using Apollo in a Meteor app" means under the hood**.

After all, it's _not that_ terrible! 🌮

<a href="https://github.com/apollographql/meteor-integration/blob/master/README.md#3-5"><h2>Add the package!</h2></a>

If you want to use this package in your Meteor app:
```sh
# install the node dependencies
npm install --save apollo-client graphql-server-express express graphql graphql-tools body-parser
# install the meteor package
meteor add apollo
```

<a href="https://github.com/apollographql/meteor-integration/blob/master/README.md#6-8"><h2>Get started in your app</h2></a>

That's great to know how it works... but the end goal is to use Apollo & Meteor together, isn't it? 😏

To get started, here are some useful resources:

- [The official Meteor - Apollo docs](http://dev.apollodata.com/core/meteor.html): it should look familiar to you now, and it provides practical examples on giving a schema to `createApolloServer` or setting up Apollo Client with `meteorClientConfig`.

- [Meteor - Apollo Starter Kit](https://github.com/apollographql/meteor-starter-kit/): a simple kit to start experimenting with Apollo, Meteor and React.

<a href="https://github.com/apollographql/meteor-integration/blob/master/README.md#10-20"><h2>Make this package going forward!</h2></a>

<h4>All contributions are welcome!</h4>

You have found a bug? You have ran into a problem using this package? [Open an issue](https://github.com/apollostack/meteor-integration/issues) and contributors will help you solve this! 🙌

You have modified the package to enable an awesome feature not supported at the moment? You think some part of the package could be written more clearly? 🤔 [Open a pull request on the Meteor integration repo](https://github.com/apollostack/meteor-integration/pulls)!

You find the Meteor integration docs to be not clear enough? [Fork the docs and open a pull request on its repo](https://github.com/apollographql/core-docs/blob/master/source/meteor.md)!

You want to speak with others Meteor folks using Apollo? Join the [Apollo Slack chatroom](http://www.apollodata.com/#slack) ➡️ #meteor-apollo

You think this code tour could be better? [Open a pull request on its repo](https://github.com/xavcz/meteor-apollo-codetour)! 🎉

Well, you get the point: [get involved in the community, you'll be warmly welcomed](http://dev.apollodata.com/community/)!

If you do roll your own implementation of Meteor & Apollo, and find interesting patterns, please open an issue or open a pull request on the package's repo, the community will be thankful! 🙏

<h4>Related resources</h4>
_Note: Most of the content written here comes from existing docs & readmes, huge thanks to their writers! If you want to have a deeper look at these resources, here is a non-exhaustive list._

**Apollo Client & friends**
* [Apollo Client, docs](http://dev.apollodata.com/core/)
* [React integration of Apollo Client, docs](http://dev.apollodata.com/react/)
* [Angular integration of Apollo Client, docs](http://dev.apollodata.com/angular2/)
* [Blaze integration of Apollo Client, docs + repo](https://github.com/Swydo/blaze-apollo)
* [Vue integration of Apollo Client, docs + repo](https://github.com/Akryum/vue-apollo)

**GraphQL Server et al.**
* [Apollo server tools, docs](http://dev.apollodata.com/tools/)
* [GraphQL.js implementation, repository](https://github.com/graphql/graphql-js)
* [GraphiQL, repository](https://github.com/graphql/graphiql)

<h4>Happy hacking with Meteor & Apollo! 🎉</h4>
