# Bolster - Vue with Axios & Mirage

This Vue app is set up with Mirage for both local development and UI testing with Vue Test Utils.

It uses Axios for its network requests, and the test shows how to force Axios to use `window.XMLHttpRequest` so Mirage can intercept the Vue app's network requests.

The Mirage server is in [src/server.js](./src/server.js). The test is in [tests/unit/example.spec.js](./tests/unit/example.spec.js).

## How to use

Pull down the repo and install deps:

```sh
git clone https://github.com/icodepixels/bolster.git
cd bolster
npm i
```

To run this app in development against a local Mirage server:

```sh
npm run dev
```

To run the Linting Utils:

```sh
npm run lint
```


To run the Vue Test Utils test:

```sh
npm run test:unit
```
