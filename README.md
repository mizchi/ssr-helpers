# @mizchi/ssr-helpers

Implement `react-cache` SSR helpers.

## Requirements

- react: ^16.7
- react-dom: ^16.7
- regenerator-runtime(included babel-polyfill)

## Data fetcher

```tsx
import { renderAsync, createResource } from "@mizchi/ssr-helpers";

// data fetcher
const resource = createResource(async () => {
  await new Promise(r => setTimeout(r, 1000));
  return { message: "hello" };
});

function App() {
  const data = resource.read();
  return <div>{data.message}</div>;
}

const html = await renderAsync({
  tree: <App />
});
```

Client rendering

```tsx
import React from "react";
import ReactDOM from "react-dom";

const root = document.querySelector(".root") as HTMLDivElement;
ReactDOM.hydrate(
  <Suspense fallback="loading">
    <App />
  </Suspense>,
  root
);
```

## How to dev

- `yarn dev`: Start application server on `http://localhost:1234`
- `yarn build`: Generate `dist`
- `yarn test`: Run jest
- `yarn deploy`: Deploy to netlify (need netlify account)

## LICENSE

MIT
