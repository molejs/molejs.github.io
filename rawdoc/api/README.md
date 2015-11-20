# API

The API of the [mole-reporter](https://github.com/molejs/mole-reporter) consists of a set of methods that aim to send the reports and provide a way to create adaptors for integrating the reports in your framework or web application.

## `config`

Config is the method that sets some configuration variables for the reporter.

**Params**

Name | Type | Description
--- | --- | ---
`config` | Object | Object with all the configuration files

Options to configure:

* **url**: the url to send the error reports. It will send a POST request with a JSON object following the mole log specification.
* **stacktraceLimit**: Max items of the stacktrace to retrieve.
* **historyLimit**: Max pairs of action state to store until the next error report.

```javascript
Mole.config({
    url: 'http://error.molejs.org/foo',
    stacktraceLimit: 50,
    historyLimit: 10
});
```

## `report`

Report receives an error and reports it to the URL specified in the config. It gathers the last pairs of actions and states and sends them along with the error.

**Params**

Name | Type | Description
--- | --- | ---
`error` | Error object | The error that is going to be reported

```javascript
try {
        errorCausingFunc();
} catch (err) {
        Mole.report(err);
}
```

## `registerActionState`

Registers a pair of action and state on the stack of pairs.

**Params**

Name | Type | Description
--- | --- | ---
`action` | Object | Action that happened
`state` | Object | Current status at the moment

```javascript
Mole.registerActionState({action: 1}, {state: 1});
```
