# Test your Gitbook locally


1. First, run yarn to install node_modules

    ```sh
    yarn
    ```

    > If you get an error similar to this *ENOSYS: function not implemented, symlink '../../../mkdirp/bin/cmd.js*
    Run the command `yarn --no-bin-links`

1. Next, run ./publish.sh

    ```sh
    ./publish.sh
    ```

    It creates a folder _book.

1. Open the static `index.html` file under the folder _book

    ![](./images/vscode-browser.png)

1. Once you're satisfied, push the content on your remote repo

    ```
    git push
    ```