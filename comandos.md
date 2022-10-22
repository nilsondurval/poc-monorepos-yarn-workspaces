# yarn workspaces

## Instalação
$ corepack enable

## Criar monorepo
$ mkdir <my-workspace-name>
$ cd <my-workspace-name>
$ yarn init -2

## Adicionar workspaces
$ mkdir apps
$ mkdir libs
-- Adicionar ao package.json
"workspaces": [
  "apps/*",
  "libs/my-lib-workspace",
  "libs/my-lib-workspace/dist/my-lib"
]

## Instalar pluguin de workspaces yarn
$ yarn plugin import workspace-tools

## Criar aplicação
$ cd apps
$ ng new <my-app-name>
-- Adicionar ao package.json
"name": "<@my-workspaces-name>/<my-app-name>",
"version": "0.0.0",
"packageManager": "yarn@3.2.4",
"packageManager": "yarn@3.2.4",
...

## Criar biblioteca
$ cd libs
$ ng new <my-workspace-name> --no-create-application
$ cd <my-workspace-name>
$ ng generate library <my-lib-name>
-- Adicionar ao package.json
"name": "<@my-workspaces-name>/<my-lib-name>",
"version": "0.0.0",
"packageManager": "yarn@3.2.4",
...

## Instalar dependencias em todos pacote
$ yarn install -- Na pasta raiz

## Iniciar aplicação
$ yarn workspace <@my-workspaces-name>/<my-app-name> run start

## Iniciar todas aplicações
$ yarn workspaces foreach run start

## build de todas aplicações e libs
$ yarn workspaces foreach run build