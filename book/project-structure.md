
1. Create a file **package.json** at the root level

    ```json
    {
        "name": "book",
        "version": "1.0.0",
        "description": "",
        "scripts": {
        },
        "author": "IBM",
        "license": "Apache-2.0",
        "devDependencies": {
        },
        "dependencies": {
            "gitbook-cli": "2.3.2"
        }
    }
    ```

1. Create a file **publish.sh** at the root level

    ```sh
    #!/bin/bash
    set -e
    export SHELLOPTS

    # prepare gitbook
    ./node_modules/.bin/gitbook install

    # all files to the same date to reduce the amount of updated files after each new generation
    touch -t 201811111111.11 book/*

    # patch gitbook so START_TIME remains the same in the generated html
    sed -i 's/var START_TIME = new Date();/var START_TIME = new Date(2018, 10, 11, 11, 11, 11);/g' ~/.gitbook/versions/3.2.3/lib/gitbook.js

    # build the book
    ./node_modules/.bin/gitbook build
    ```

1. Create a file **book.json** at the root level

    ```json
    {
        "root": "book",
        "title": "Gitbook template",
        "pluginsConfig": {
        "theme-default": {
            "showLevel": true
        },
        "fancybox": {
            "openEffect": "elastic",
            "closeEffect": "elastic"
        },
        "prism": {
            "css": [
            "prismjs/themes/prism-tomorrow.css"
            ]
        },
        "webheader": {
            "headerTitle" : "Gitbook Template"
        }
        },
        "plugins": [
        "prism", "-highlight",
        "collapsible-chapters",
        "hints",
        "copy-code-button",
        "back-to-top-button",
        "fancybox",
        "web-header",
        "codetabs"
        ],
        "gitbook": "3.2.3"
    }
    ```

1. Create a file **travis.yml** at the root level

    ```yaml
    language: node_js
    dist: trusty
    sudo: required

    node_js:
    - "6.9.1"

    script:
    - ./publish.sh

    deploy:
    - provider: pages
    local-dir: _book
    skip-cleanup: true
    github-token: $GITHUB_TOKEN
    keep_history: true
    on:
        branch: master
    ```