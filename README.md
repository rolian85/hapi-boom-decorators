# hapi-boom-decorators

[![Circle CI](https://circleci.com/gh/brainsiq/hapi-boom-decorators/tree/master.svg?style=svg&circle-token=9fe584ee6c1099bec9ba2864d3a63428f444a098)](https://circleci.com/gh/brainsiq/hapi-boom-decorators/tree/master)

A plugin for [hapi.js](hapijs.com) to make responding with [boom](https://github.com/hapijs/boom) errors a little less verbose by decorating the reply interface with equivilent methods.


## Install

`npm install hapi-boom-decorators --save`

## Register Plugin

```
server.register({
  register: require('hapi-boom-decorators')
}, function(err) {
  ...
});
```

## API

Standard way of replying with boom response:

```
server.route({
  method: 'GET',
  path: '/resource/{id}',
  handler: (request, reply) => {
    reply(Boom.notFound());
  }
});
```

New way:

```
server.route({
  method: 'GET',
  path: '/resource/{id}',
  handler: (request, reply) => {
    reply.notFound();
  }
});
```

Check the [boom documentation](https://github.com/hapijs/boom#overview) for all available methods. Every 4xx and 5xx error type has been implemented in hapi-boom-decorators with the same function signature e.g. `reply.xxx([message], [data])`.


* [wrap](https://github.com/hapijs/boom#wraperror-statuscode-message) - `reply(Boom.wrap(err, 500, 'a message'))` can be written as `reply.boom(500, err, 'a message')`
* [create](https://github.com/hapijs/boom#createstatuscode-message-data) - `reply(Boom.create(500, 'a message', {}))` can be written as `reply.boom(500, 'a message', {})`
