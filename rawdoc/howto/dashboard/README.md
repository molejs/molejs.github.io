#mole-dashboard

Mole dashboard is a tool to view and explore all your logs stored in a mole server.


## Install

To install, you have the option to do so with docker, as the Dockerfile is provided in the repo.

If you choose to install it the "classic" way, follow these steps:

```bash
git clone git@github.com:molejs/mole-dashboard.git
cd mole-dashboard
npm install
vim src/config.js # Edit the URL of the mole-server
npm build
```

Now you just have to serve the directory and you're done.

**Note:** you may want to filter all the files that are not `index.html` and the files under `dist` from apache, nginx or whatever you are using to serve the app.

