#mole-reporter

This is the core reporting library. It gathers action-states of a js application in its internal
state and sends it back to the mole-server when errors occur. 

## Install requirements

The library depends on [fetch](https://github.com/github/fetch) to perform http requests to the
server. To install on your front end project install as a dependency follow the [project's
instructions](https://github.com/github/fetch/blob/master/README.md#installation).

## Install

```bash
npm install --save mole-reporter
```

## Usage

The only configuration required is for setting the error-server url:

```javascript
import Mole from 'mole-reporter';

Mole.config({url: 'http://errors.example.com/mole'});

```

To record errors, simply report them.

```javascript
import Mole from 'mole-reporter';

Mole.report(error);

```

In order to record app action-state history, record every action and state.

```javascript
import Mole from 'mole-reporter';

Mole.registerActionState(action, state);

```

## Optional config

Extra config options are self-explanatory (values in the example are defaults).
```javascript
import Mole from 'mole-reporter';

Mole.config({
    url: '',
    stacktraceLimit: 50,
    historyLimit: 10
});

```