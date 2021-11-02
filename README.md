# Nx Storybook issue demonstration for buildable libs

This is minimal reproduction of issue when storybook doesn't run for buildable libraries.

## Current Behavior 
The storybook won't run for buildable libraries

## Expected Behavior
The storybook shoud run.

## Steps to reproduce
The repo was generated via following commands (see the commits history):
```shell
npx create-nx-workspace --package-manager=yarn --name=nx-sb-demo --preset=oss --nx-cloud=false

yarn add -D @nrwl/angular @nrwl/storybook

yarn update
yarn update --run-migrations

yarn nx g @nrwl/angular:lib first-lib --buildable

yarn nx g @nrwl/angular:lib second-lib --buildable

yarn nx g @nrwl/angular:component demo --project=second-lib

yarn nx g @nrwl/storybook:configuration --name=second-lib --configure-cypress=false --ui-framework=@storybook/angular

yarn nx g @nrwl/angular:stories --name=second-lib --cypress-project=false --generate-cypress-specs=false

```

Now, the following command fail:
```shell
yarn nx run second-lib:storybook
```

### Failure Logs
```lo
yarn run v1.22.0
$ nx run second-lib:storybook

> nx run second-lib:storybook 
info => Loading presets
info => Loading 1 config file in "/xxx/nx-sb-demo/packages/second-lib/.storybook"
info => Loading 8 other files in "/xxx/nx-sb-demo/packages/second-lib/.storybook"
info => Adding stories defined in "/xxx/nx-sb-demo/packages/second-lib/.storybook/main.js"
(node:35656) [DEP0148] DeprecationWarning: Use of deprecated folder mapping "./" in the "exports" field module resolution of the package at /xxx/nx-sb-demo/node_modules/tslib/package.json.
Update this package.json to use a subpath pattern like "./*".
(Use `node --trace-deprecation ...` to show where the warning was created)
info => Found custom tsconfig.json
info => Using implicit CSS loaders
info => Loading angular-cli config
info => Using angular project "first-lib:build" for configuring Storybook
ERR! => Could not get angular cli webpack config
TypeError [ERR_INVALID_ARG_TYPE]: The "path" argument must be of type string. Received undefined


          Broken build, fix the error above.
          You may need to refresh the browser.
        

———————————————————————————————————————————————

>  NX   ERROR  Running target "second-lib:storybook" failed

  Failed tasks:
  
  - second-lib:storybook
  
  Hint: run the command with --verbose for more details.

error Command failed with exit code 1.
info Visit https://yarnpkg.com/en/docs/cli/run for documentation about this command.

```

### Environment
```
yarn run v1.22.0
$ nx report

>  NX  Report complete - copy this into the issue template

  Node : 16.10.0
  OS   : darwin x64
  yarn : 1.22.0
  
  nx : 13.1.2
  @nrwl/angular : 13.1.2
  @nrwl/cli : 13.1.2
  @nrwl/cypress : 13.1.2
  @nrwl/devkit : 13.1.2
  @nrwl/eslint-plugin-nx : 13.1.2
  @nrwl/express : Not Found
  @nrwl/jest : 13.1.2
  @nrwl/linter : 13.1.2
  @nrwl/nest : Not Found
  @nrwl/next : Not Found
  @nrwl/node : Not Found
  @nrwl/nx-cloud : Not Found
  @nrwl/react : Not Found
  @nrwl/schematics : Not Found
  @nrwl/tao : 13.1.2
  @nrwl/web : Not Found
  @nrwl/workspace : 13.1.2
  @nrwl/storybook : 13.1.2
  @nrwl/gatsby : Not Found
  typescript : 4.3.5

```
