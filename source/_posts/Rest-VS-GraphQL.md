---
title: Rest VS GraphQL
date: 2017-10-29 13:45:32
tags:
---

Hi guys, I have read some articles about Rest vs GraphQL, I would like to summarize a bit of what I learn so far, and give my suggestions:

*Background*:
People used to have their model, view and controller all live on the server, getting data from models to view is ok because almost all the data is right there on the server. In modern JS or Mobile apps, that is no longer the case, the controllers and views now live mostly on the client, however, most of the data is still on the server. With all but the most custom RESTful APIs, fetching data from the server is both costly and complicated: the latency is high, and chances are you will either fetch more data than you need or make more roundtrips you would like — or both! That’s where GraphQL comes to the rescue.

With REST, the server determines what data will be sent down to the client
problem: app evolves, become more complex
1. make separate endpoints for different views of the same object
2. make many calls for to complete one result or create a new endpoint for this specific result.
3. generic endpoints -> make app slow, too many useless info within API calls, not specific enough.
4. dynamic table (if let clients choose the data field) -> cannot eliminating any old code (needs to remain compatibility with the old client), then we always create a new endpoint, leave the old ones untouched.

With GraphQL, the server exposes a comprehensive data schema to the client, and the client decides exactly what it needs. 
1. Unlike with discrete REST endpoints, all the data for any given UI (page) can be sent in one trip to the client.
2. GraphQL fits between your backend and your frontend. It lets you define a model for your data and a mapping between that model and your backends. It is not a replacement for your existing backend.
3. GraphQL fetches your data in one call to the server instead of many, and they cache the data for you.
4. GraphQL has an increasingly active ecosystem, with implementations in Java, Python, Ruby, Scala, .NET, Go, etc.
5. Used with many different databases, can combine data from multiple sources into one GraphQL schema
    * SQL DB
    * MongoDB
    * Even REST endpoint

![grapql](https://philsblog.b-cdn.net/images/grapql.png "grapql")

Here is [tutorial](https://dev-blog.apollodata.com/tutorial-building-a-graphql-server-cddaa023c035#.pia6zcwlg) of how to GraphQL Server

*Summary*:
Most of the articles are introducing this new tech in a positive attitude, and to myself, I do believe GraphQL is a better alternative to REST. However, I also suggest that we should take a deep look into our requirements, because I am not entirely familiar with FE (Web, mobile), so I am not sure what is the situation. To my understanding so far, GraphQL benefits the projects that:
* have more than one client (e.g. web + iOS)
* have a mobile client and care about latency and bandwidth
* are moving to a microservices architecture
* have a REST API that has gotten so complicated and it’s a significant drag on product development.
* want to decouple frontends and backends to speed up development

If that is the case, then I highly recommend adopting this new tech. Even if it is not, I still think GraphQL is an excellent option to adopt when we got time, because it brings:

* Clean API between backends and frontends
* Less communication overhead and fewer meetings
* No more time spent writing API documentation
* No more time spent trying to figure out an API
* Great tooling for your API - GraphiQL, not GraphQL read it carefully.
Here is a [story](https://voice.kadira.io/adopting-graphql-2f00dfe0fda2#.htpdce1sm) of adopting GraphQL and you will find the benefits list above in it.

By the way, here is another option call Falcor, designed by Netflix, which is similar to GraphQL, but with different syntax. Falcor is easier to learn but not as powerful as GraphQL. Also, Falcor is JS only; GraphQL has so many implementations.

References:
REST API downfalls, and dawn of GraphQL
https://medium.com/@ottovw/rest-api-downfalls-and-dawn-of-graphql-dd00991a0eb8#.5kf08z2n7

Tutorial: How to build a GraphQL server
https://dev-blog.apollodata.com/tutorial-building-a-graphql-server-cddaa023c035#.pia6zcwlg

GraphQL vs. Falcor
https://dev-blog.apollodata.com/graphql-vs-falcor-4f1e9cbf7504#.xeearf6rs

Just Because Github Has a GraphQL API Doesn’t Mean You Should Too
https://www.programmableweb.com/news/just-because-github-has-graphql-api-doesn%E2%80%99t-mean-you-should-too/analysis/2016/09/21

GraphQL in the age of REST APIs
https://medium.com/chute-engineering/graphql-in-the-age-of-rest-apis-b10f2bf09bba#.ezbukzu35

Adopting GraphQL
https://voice.kadira.io/adopting-graphql-2f00dfe0fda2#.htpdce1sm
