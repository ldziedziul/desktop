# Mattermost Desktop Development Guides

## Build instructions

### Prerequisites
- C++ environment which supports C++11 (e.g. VS 2015, Xcode, GCC)
- Python 2.7
- Node.js 4.2.0 or later
- Git

### Installing dependencies
`npm install` is executed twice to install dependencies of `src/` directory.

```
$ npm install
```

### Building
Build JavaScript codes with `webpack`, and copy other assets into `dist/` directory.

```
$ npm run build
```

After building is done, you can execute the application with `npm start`.

### Packaging
Package `dist/` directory as distributable formats with [`electron-builder`](https://github.com/electron-userland/electron-builder).
Packages will be generated into `release/` directory.

```
$ npm run package:<all | windows | mac | linux>
```

#### Dependencies
Need to install some software required by `electron-builder` to build packages.
Please see [electron-builder wiki](https://github.com/electron-userland/electron-builder/wiki/Multi-Platform-Build) for detailed description.

**Minimum requirements for current platform:**
- Windows: Nothing.
- macOS: Nothing.
- Linux (64 bit): `icnsutils`, `graphicsmagick` and `xz-utils` if Ubuntu is used.

#### Code signing
Set environment variables to build trusted packages.
Please see [electron-builder wiki](https://github.com/electron-userland/electron-builder/wiki/Code-Signing) for detailed description.

**Quoted from the wiki:**

| Env name | Description |
|---|---|
| `CSC_LINK` | The HTTPS link (or base64-encoded data, or `file://` link) to certificate (`*.p12` or `*.pfx` file). |
| `CSC_KEY_PASSWORD` | The password to decrypt the certificate given in `CSC_LINK`. |
| `CSC_NAME` | *macOS-only* Name of certificate (to retrieve from login.keychain). Useful on a development machine (not on CI) if you have several identities (otherwise don't specify it). |

### Tests
Execute automated tests.

```
$ npm test
```

There are two steps in `npm test`.

Test functionality:

```
$ npm run test:app
```

Test coding style:

```
$ npm run lint:js
```

### Helper commmands

#### `npm run watch`
Reload the application automatically when you have saved source codes.

#### `mpm run prettify`
Format the source codes to pass `npm test`.

## Directory Structure

```
Mattermost Desktop
├── docs/ - Documentations.
├── resources/ - Resources which are used outside of the application codes, and original images of assets.
├── scripts/ - Helper scripts.
├── src/ - Application source code.
│   ├── assets/ - Assets which are loaded from the application codes.
│   ├── browser/ - Implementation of Electron's renderer process.
│   │   ├── components/ - React.js components.
│   │   ├── css/ - Stylesheets.
│   │   ├── js/ - Helper JavaScript modules.
│   │   └── webview/ - Injection code for Electron's <webview> tag.
│   ├── common/ - Common JavaScript modules for both Electron's processes.
│   └── main/ - Implementation of Electron's main process.
│       └── menus/ - Application menu.
└── test/ - Automated tests.
    ├── modules/ - Scripts which are commonly used in tests.
    └── specs/ - Test scripts.
```

### Other directories
- **dist/** - Built application code and asset.
- **node_modules/** - Third party Node.js modules to build the application.
- **release/** - Packaged distributable applications.
- **src/node_modules/** - Third party Node.js modules to use in the application.
