#How to install

As this project actually spans several tools (js reporting library & context adaptor, backend
server & data dashboard). Therefore installation breaks down into each individual component.

##mole-reporter

This is the core reporting library. It gathers action-states of a js application in its internal
state and sends it back to the mole-server when errors occur. 

###Install requirements

The library depends on [fetch](https://github.com/github/fetch) to perform http requests to the
server. To install on your front end project install as a dependency follow the [project's
instructions](https://github.com/github/fetch/blob/master/README.md#installation).

###Install mole-reporter

Install as a dependency of your project:
```
npm install --save mole-reporter
```

##mole-server

In order to integrate mole