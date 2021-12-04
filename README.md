# lamejs issue #65

**NOTE: This issue has since been resolved and this repository has been archived.**

This repository was created in response to [issue #65 of lamejs](https://github.com/zhuker/lamejs/issues/65). It contains a minimal project that can be used to reproduce the issue. 

## Relevant Files

- [`package.json`](package.json): Dependencies and script for running the project.
- [`index.ts`](index.ts): TypeScript file that imports `lamejs`.
- [`index.html`](index.html): HTML page that loads [`index.ts`](index.ts).

## Dependencies

- `lamejs`: The library that contains the issue.
- `parcel`: Bundles [`index.ts`](index.ts) for web use. Note, that the bug occurs when `parcel build` is used (for production ready output), but not with `parcel serve`. I have not yet taken steps to further isolate the issue (i.e. removing this dependency).
- `http-server`: Static HTTP server for testing the output of `parcel build` in the browser. It is not related to the issue.

## Steps to reproduce

Clone the repository, install dependencies, and run the `start` script, which builds the project with `parcel` runs `http-server`:

~~~sh
git clone https://github.com/eibens/lamejs-issue-65.git
cd lamejs-issue-65
npm install
npm start
~~~

Go to [http://127.0.0.1:8080](http://127.0.0.1:8080) and open the developer console. It should show the following error:

~~~txt
Uncaught ReferenceError: assignment to undeclared variable Lame
~~~

## Solution

Adding `var` at the start of lines 17 to 25 in `node_modules/lamejs/src/js/index.js` fixes the problem. This solution was proposed in [pull request #59 of lamejs](https://github.com/zhuker/lamejs/pull/59).
