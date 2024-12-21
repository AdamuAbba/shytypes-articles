---
id: Source Code Arch
aliases: []
tags: []
---

# Overview

# Detail Overview

- We would be using aliased imports meaning we have to configure `webpack`, `jest` and `eslint` to work with this aliases we would be defining. this would include the following aliases
  - “@components” : “./src/components”
  - “@screens” : “./src/screens”
  - “@assets”: “./src/assets”
  - “@redux”: “./src/redux”
  - ... (i.e all folders under the `src` folder would be aliased)
- Eslint rules would be followed ensuring there are no linting warnings
- `package.json` would contain scripts to
  - [ ] to initiate test using jest
  - [ ] to run lint on the whole app
  - [ ] to fix lint on the whole app
  - [ ] to run prettier fix on the whole app’s file
  - [ ] to create a production build of the js assets
  - [ ] to run cypress (on headless mode)
  - [ ] to open cypress ( with UI)
- All Images should be web friendly images with size `not` more than **1mb.**
- We would also make use of husky in order to ensure that linting and test(when we have test enabled) pass on the developer’s machine before its pushed to the remote repo

# Tooling

- Prettier (file formatting)
- Eslint (linting)
- husky (git action hook)
- react-testing-library/jest (unit test)
- cypress-cucumber (cypress plugin to enable [**Gherkin**](https://www.guru99.com/gherkin-test-cucumber.html) **scripting)**

# **Directory scaffold**

.

├ ...

- ├ config
  ├ ...
  ├ jest.config.js
  ├ firebase.config.js

├ Readme.md

├ .env

├ .eslinignore

├ eslint.config.js

├ .prettierrc  
├ src

- ├ components
  - ├ TextField
    ├ Index.js
    ├ constants.js. (this is optional if there are no constants for the screen or components)
    - ├ hooks
      ├ useTextFieldHook1.js
      └ useTextFieldHook1.js
      ├ TextField.js
      ├ TextField.style.js
      └ TextField.test.js
  - ├ Button
    ├ Index.js
    ├ constants.js
    ├ Button.js
    ├ Button.style.js
    └ Button.test.js
- ├ pages
  - ├ Register
    ├ Index.js
    ├ constants.js
    ├ hooks
    └ useRegister.js
    ├ Register.js
    ├ Register.style.js
    └ Register.test.js
  - ├ Login
    ├ components
    ├ LoginComponent1.js
    └ LoginComponent2.js
    ├ constants.js
    ├ Index.js
    ├ Login.js
    ├ Login.style.js
    ├ Login.test.js
    └ hooks
    └ useLogin.js
- ├ routes
  ├ index.js
  ├ dashboard.routes.js
  ├ income.routes.js
  └ expense.routes.js
- ├ services
  ├ income.service.js
  ├ expense.service.js
  ├ budget.service.js
- ├ utils
  ├ helpers.js
- ├ assets
  ├ images
  ├ svgs
  ├ fonts
  └ gifs
- ├ redux
  - ├ reducers
    ├ app.reducer.js
    ├ login.reducer.js
  - ├ actions
    ├ app.action.js
    ├ login.recuer.js
  - ├ actionTypes
    ├ app.type.js
    ├ login.type.js
    ├ combinedReducer.js
    └ middleware.js
- ├ tests
  ├ cypress.json
  ├ cypress
  ├ fixtures
  ├ helpers
  └ mocks

└ ...

# Form validation

We would be making use of Formik as your mode of form validation

# Eslint rule

```JSON
{
  "parser": "@babel/eslint-parser",
  "extends": ["airbnb", "plugin:react/recommended"],
  "plugins": ["import", "babel", "jsx"],
  "globals": {
    "describe": true,
    "it": true,
    "beforeEach": true,
    "afterEach": true,
    "jest": true,
    "expect": true
  },
  "env": {
    "es2020": true,
    "browser": true,
    "node": true
  },
  "parserOptions": {
    "requireConfigFile": false
  },
  "rules": {
    "arrow-parens": "off",
    "react/jsx-props-no-spreading": "off",
    "jsx-a11y/control-has-associated-label": "off",
    "import/no-cycle": "off",
    "import/named": "off",
    "jsx-a11y/alt-text": "off",
    "jsx-a11y/anchor-is-valid": "off",
    "jsx-a11y/click-events-have-key-events": "off",
    "jsx-a11y/heading-has-content": "off",
    "jsx-a11y/href-no-hash": "off",
    "jsx-a11y/label-has-associated-control": "off",
    "jsx-a11y/label-has-for": "off",
    "jsx-a11y/no-autofocus": "off",
    "jsx-a11y/no-noninteractive-element-interactions": "off",
    "jsx-a11y/no-static-element-interactions": "off",
    "react/button-has-type": "off",
    "react/default-props-match-prop-types": "off",
    "react/destructuring-assignment": "off",
    "react/forbid-prop-types": "off",
    "react/jsx-filename-extension": "off",
    "react/jsx-no-bind": "off",
    "react/jsx-no-target-blank": "off",
    "react/no-access-state-in-setstate": "off",
    "react/no-array-index-key": "off",
    "react/no-did-mount-set-state": "off",
    "react/no-did-update-set-state": "off",
    "react/no-multi-comp": "off",
    "react/no-unused-prop-types": "off",
    "react/no-unused-state": "off",
    "react/prefer-stateless-function": "off",
    "react/require-default-props": "off",
    "react/sort-comp": "off",
    "react/display-name": "off",
    "implicit-arrow-linebreak": "off",
    "react/jsx-closing-tag-location": "off",
    "jest/no-focused-tests": "off",
    "prefer-destructuring": "off",
    "prefer-object-spread": 2,
    "func-names": "off",
    "global-require": "off",
    "new-cap": [
      "error",
      {
        "newIsCapExceptions": ["mnemonic"]
      }
    ],
    "react/prop-types": "off",
    "no-plusplus": "off",
    "no-restricted-exports": "off",
    "no-underscore-dangle": "off",
    "import/no-extraneous-dependencies": "off",
    "linebreak-style": 0,
    "no-param-reassign": "off",
    "complexity": ["error", 10],
    "max-depth": ["error", 3],
    "max-nested-callbacks": ["error", 3],
    "max-statements": ["error", 10],
    "max-lines": ["error", 400]
  },
  "overrides": [
    {
      "files": ["*.test.js", "*.spec.js"],
      "rules": {
        "max-depth": ["error", 2],
        "max-nested-callbacks": ["error", 4],
        "max-statements": ["error", 30],
        "max-lines": ["error", 500]
      }
    }
  ]
}
```

# Jest config

```JSON
{
	/* eslint-disable max-lines */
	module.exports = {
  rootDir: './',
  modulePaths: ['src/modules'],
  testMatch: ['<rootDir>/src/**/*.test.js'],
  verbose: false,
  moduleFileExtensions: ['js'],
  moduleDirectories: ['node_modules'],
  moduleNameMapper: {},
  collectCoverage: true,
  coverageDirectory: '<rootDir>/coverage/jest',
  collectCoverageFrom: ['src/**/*.js'],
  coveragePathIgnorePatterns: ['src/App.test.js'],
  testPathIgnorePatterns: ['<rootDir>/src/App.test.js'],
  // TODO: we need to had more coverate threshold for other folder directory
  coverageThreshold: {},
  setupFiles: ['jest-canvas-mock'],
  transform: {
    '^.+\\.js$': 'babel-jest',
    '^.+\\.svg|png|jpg|jpeg|otf|ttf$': '<rootDir>/tests/__mocks__/fileTransform.js',
  },
  testURL: 'http://localhost',
  globals: {
    PRODUCTION: true,
    TEST: true,
    VERSION: '',
  },
  coverageReporters: ['text', 'lcov', 'cobertura', 'html'],
  reporters: ['default'],
  setupFilesAfterEnv: ['./node_modules/@testing-library/jest-dom/extend-expect'],
  testEnvironment: 'jsdom',
  watchPlugins: [
    ['jest-watch-toggle-config', { setting: 'verbose' }],
    ['jest-watch-toggle-config', { setting: 'collectCoverage' }],
    'jest-watch-typeahead/filename',
  ]
}
```
