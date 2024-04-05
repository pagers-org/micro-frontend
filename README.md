# Next.js 14 with Module Federation

## Getting Started

1. run `pnpm install`
2. run `pnpm run start` and browse to `http://localhost:3001`

## Context

We have three next.js applications

- `checkout` - port 3000
- `home` - port 3001
- `shop` - port 3002

The applications utilize omnidirectional routing and pages or components are able to be federated between applications like a SPA

I am using hooks here to ensure multiple copies of react are not loaded into scope on server or client.

### Sharing

Next.js does not have an async boundary. Between the entrypoint and the shared code.
Read this for more context: https://github.com/sokra/slides/blob/master/content/ModuleFederationWebpack5.md

In order for webpack to figure out who shares what, an async boundary is typically needed somewhere before the module is used.
Usually, we can work around async boundaries for things like `react` by specifying the following

https://medium.com/dev-genius/module-federation-advanced-api-inwebpack-5-0-0-beta-17-71cd4d42e534?source=friends_link&sk=70658eb0bf58dfcc5ce534cb1cd78b1f

```js
const config = {
  shared: {
    react: {
      eager: true,
      singleton: true,
    },
  },
};
```
