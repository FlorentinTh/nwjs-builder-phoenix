
# nwjs-builder-phoenix [![npm version](https://img.shields.io/npm/v/nwjs-builder-phoenix.svg)](https://npmjs.org/package/nwjs-builder-phoenix) [![Standard Version](https://img.shields.io/badge/release-standard%20version-brightgreen.svg)](https://github.com/conventional-changelog/standard-version)

A possible solution to build and package a ready for distribution NW.js app for Windows, macOS and Linux.

## Why Bother?

We already has official `nw-builder` and `nwjs-builder`, which was built as an alternative before `nw-builder` would support 0.13.x and later versions.
`nw-builder` has made little progress on the way, and `nwjs-builder` has been hard to continue due to personal and historic reasons.

`electron-builder` inspired me when I became an Electron user later, loose files excluding, various target formats, auto updater, artifacts publishing and code signing, amazing!

Although NW.js has much lesser popularity than Electron, and is really troubled by historic headaches, let's have something modern.

## Features

* Building for Windows, macOS and Linux
  * Common: `zip`, `7z`
  * Windows: `nsis`
  * macOS: TODO
  * Linux: TODO
* Building for different platforms concurrently
* Chrome App Support
* Configurable executable fields and icons for Windows and macOS
* Integration for `nwjs-ffmpeg-prebuilt`
* Exclusion of useless files from `node_modules`
* TODO Auto Updater inspired by `electron-updater`
* TODO Rebuilding native modules
* Ideas appreciated :)

## Getting Started

* Make sure your NW.js project has a valid `package.json` (eg. generated by `npm init`), and have basic fields like `name`, `description` and `version` filled.

* Install `nwjs-builder-phoenix` as a `devDependencies` of your NW.js project as follows:

```shell
npm install nwjs-builder-phoenix --save-dev
```

By installing it locally, `build` and `run` commands will be available in npm scripts. You can access option lists via `./node_modules/.bin/{ build, run } --help`.

DO NOT install it globally, as the command names are just too common.

* Add `build` properties at the root of the `package.json`, for example:

```json
// package.json
{
    "build": {
        "nwVersion": "0.14.7"
    }
}
```

This will specify the NW.js version we are using. See more in the following Options section.

* Add some helper npm scripts, for example:

```json
// package.json
{
    "scripts": {
        "dist": "build --win --mac --linux --x86 --x64 --mirror https://dl.nwjs.io/ .",
        "start": "run --x86 --mirror https://dl.nwjs.io/ ."
    }
}
```

The above code snippet enables `npm run dist` and `npm run start`/`npm start`. The former builds for all major platforms and both x86 and x64 arch, and the latter runs the project with x86 binaries, both with the specified version of NW.js and use specified mirror to accelerate the download.

* Well done.

This should be the common use case, read the following Options section and configure things if needed.

See also [project for testing](./assets/project/) and [test cases](./test/) for reference.

## Options

Passing and managing commandline arguments can be painful. In `nwjs-builder-phoenix`, we configure via the `build` property of the `package.json` of your NW.js project.

Also [see all available options here](./docs/Options.md).

## Differences to `nwjs-builder`

* `nwjs-builder-phoenix` queries `versions.json` only when a symbol like `lts`, `stable` or `latest` is used to specify a version.
* `nwjs-builder-phoenix` uses `rcedit` instead of `node-resourcehacker`, thus it's up to you to create proper `.ico` files with different sizes.
* `nwjs-builder-phoenix` supports node.js 4.x and later versions only.
* `nwjs-builder-phoenix` writes with TypeScript and benefits from strong typing and async/await functions.

## Known Mirrors

If you have difficulties connecting to the official download source, you can specify a mirror via `--mirror` argument of both `build` and `run`, or by setting `NWJS_MIRROR` environment variable. Environment variables like `HTTP_PROXY`, `HTTPS_PROXY` and `ALL_PROXY` should be useful too.

* China Mainland
  * https://npm.taobao.org/mirrors/nwjs/
* Singapore
  * https://cnpmjs.org/mirrors/nwjs/

## License

MIT.
