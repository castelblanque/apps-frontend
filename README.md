# apps-frontend

Apps-frontend is a frontend app written using VueJS framework.
It makes use of the endpoints exposed by [Apps-manager app](https://github.com/castelblanque/apps-manager).

Allows to list available Helm charts to be installed: install and uninstall them.

## CI

There is a GitHub action to build the image and push it to Docker hub

  [Docker hub repo](https://hub.docker.com/r/castelblanque/apps-frontend)

## Local development

### Project setup

    ```bash
    npm install
    ```

#### Compiles and hot-reloads for development
    
    ```bash
    npm run serve
    ```

#### Compiles and minifies for production
    
    ```bash
    npm run build
    ```

#### Lints and fixes files
    
    ```bash
    npm run lint
    ```

#### Customize configuration

See [Configuration Reference](https://cli.vuejs.org/config/).
