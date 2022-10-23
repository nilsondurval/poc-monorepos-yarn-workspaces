# poc-monorepos-yarn-workspaces
This is a POC of monorepos using yarn worspaces from yarnpkg.com. The concepts that i want to prove are:
- I can have multiple apps and libs in the same workspace/repository
- The applications and libs are auto linked
- Changes in a lib are immediately reflected in the apps at runtime
- I can have multiple package.json (one per app/lib)
- I can have dependencies installed in one app/lib and others no
- I can run a single build/start/pack
- I can have ci/cd separate per app

# Stack
- yarn@3.2.4
- angular@14.2.0

# Installing yarn
If you have Node.js >=16.10
```sh
$ corepack enable
```
else
```sh
$ npm i -g corepack
```

# How this yarn workspace was created
```sh
$ mkdir <my-workspace-name>
$ cd <my-workspace-name>
$ yarn init -2
$ mkdir apps
$ mkdir libs
```

-- Note: Alter package json as below
> "workspaces": [
>       "apps/*",
>       "libs/my-lib-workspace",
>       "libs/my-lib-workspace/dist/my-lib"
> ]

## Yarn workspaces pluguin
```sh
$ yarn plugin import workspace-tools // at root directory level
```

# Setup development enviroment

## building the lib first
```sh
// This step is necessary because the apps depends on the lib dist
$ cd libs/my-lib-workspace
$ npm install
$ npm run build
```

## Installing and building all
```sh
// at root level
$ yarn install 
$ yarn workspaces foreach run build
```

## Starting
```sh
// at root level
$  yarn workspace @poc-monorepos-yarn-workspaces/my-app1 run start
$  yarn workspace @poc-monorepos-yarn-workspaces/my-app2 run start
```

# Useful commands

## Building

###  Building of one app/lib
```sh
$ yarn workspace <@my-workspaces-name>/<my-app-name> run build
```

### Building all apps/libs
```sh
$ yarn workspaces foreach run build
```

###  Building app/lib with watch option
```sh
$ yarn workspace <@my-workspaces-name>/<my-app-name> run watch
```

## Starting the apps

### Starting one app
```sh
$ yarn workspace <@my-workspaces-name>/<my-app-name> run start
```

### Creating a new app
```sh
$ cd apps
$ ng new <my-app-name>
```
-- Note: Alter package json as below
> "name": "<@my-workspaces-name>/<my-app-name>"

### Creating a new lib

#### Creating cli workspace
```sh
$ cd libs
$ ng new <my-workspace-name> --no-create-application
$ cd <my-workspace-name>
```
-- Note: Alter package json as below
> "name": "<@my-workspaces-name>/<my-lib-workspace-name>"

#### Generate lib on workspace
```sh
$ ng generate library <my-lib-name>
```

-- Note: Alter package json as below
> "name": "<@my-workspaces-name>/<my-lib-name>"
