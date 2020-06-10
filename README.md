# sapper-template / Nollup

Experimental branch exploring Sapper support of Nollup :zap:


## Running the demo

```bash
npx degit "rixo/sapper-template-hot#nollup" my-app
cd my-app
yarn
yarn dev
```

Open http://localhost:3333

**ATTENTION** Sapper's normal server is listening on port 3000, because Nollup's dev server is configured to proxy non-bundle requests to Sapper's backend. but you need to access your app at http://localhost:3333 with the current config.
