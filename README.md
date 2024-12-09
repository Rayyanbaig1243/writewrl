# writewrl
## Writeurl - an online collaborative editor    ### Writeurl is a collaborative editor  Writeurl is a client server system. The frontend code is written in pure  javascript using no frameworks. The backend is a node.js application.  The client and server communicate through a WebSocket connection. The client stores local  changes in the browser's local storage. The editor can be used in offline mode. Changes are  always uploaded to the server when a connection is available.   Writeurl documents are identified by their (write)url:  www.writeurl.com/text/id/read-password/write-password    There is a read only version with a (read)url of the form  www.writeurl.com/text/id/read-password  This url structure makes it easy to share documents. No user registration is needed.    ####  Writeurl as an online service   Writeurl is available as an online service at www.writeurl.com  The code running the online service is the same as in this git repo.    ###Local installation  Writeurl can be installed and run locally as an alternative to using the online service.     #### Installation instructions    ##### Dependencies  The only required dependeny is node.js and the modules in package.json.  It is recommended to use node.js version 8.    ##### Clone the repo  ``` git clone https://github.com/morten-krogh/writeurl.git ```     ##### Install the node js modules   ``` npm install ```    ##### Build the browser code   Go to the writeurl directory. Use the build script.  ``` bash build.sh browser ```    Now the browser code is available in the directory  `build/release/browser/`    ##### Configuring the server  The node.js server code is located in the directory `server-nodejs-express`  The server needs a configuration file in the YAML format. An example file is   ```server-nodejs-express/config.yaml```    ``` port: 9000  release:   public: /Users/mkrogh/writeurl/build/release/browser  debug:   host: debug.writeurl.localhost   public: /Users/mkrogh/writeurl/build/debug/browser  documents:   path: /Users/mkrogh/writeurl-test-dir/doc_dir  publish:   public: /Users/mkrogh/writeurl-test-dir/publish_dir  # Pino logger # Output goes to stdout. logger:   # levels: silent, fatal, error, warn, info, debug, trace   level: trace ```    `port` is the port at which the server listens.     `release` and `debug` are the directories built above containing the browser code.    `documents` is the directory where all the writeurl documents will be stored. The server uses files to   store the documents (one subdirectory per document).    `publish` is the directory where the published (html) versions of the documents will be stored.    `logger.level` is the logging level. Logging goes to standard output.    ##### Starting the server  In the directory `server-nodejs-express`  type  ```node writeurl-server.js config.yaml ```    ##### Start typing  Go to localhost:9000 in the browser and start typing.    ### Example production installation  For production, it is recommended to use a reverse proxy with TLS, and to daemonize the   Writeurl server. For daemonization, one can use a node.js process manager or a system daemon   such as systemd on Linux.     The online Writeurl service uses nginx as a reverse proxy and systemd under Linux for daemonization.    ##### Example nginx configuration    An example nginx.conf file is located at   https://github.com/morten-krogh/writeurl/blob/master/documentation/nginx.conf      ##### Example systemd unit file  ``` [Unit]  Description = writeurl server After = network.target  [Service] Type = simple User = www ExecStart = /home/www/.nvm/versions/node/v8.9.4/bin/node /home/www/writeurl/server-nodejs-express/writeurl-server.js /home/www/writeurl/server-nodejs-express/config-debian.yaml Restart = on-failure  [Install] WantedBy = multi-user.target ```    ### Backup  The server can be backed up by just backing up the files in the `documents` and `publish`  directories specified in the config.yaml file. Any type of file backup can be used, e.g. periodic   rsync. The backup script can be used while the server is running as long as the backup script does not  change any files.     The server can be restarted from a backup by just placing the backup directories in the place   pointed to by `documents` and `publish` in the config file.    ### Embedding    Writeurl can be embedded as described in   https://github.com/morten-krogh/writeurl/blob/master/html/embed/index.html  This page is available on the online service as well  https://www.writeurl.com/embed    ### Contributions and issues  Bugs and feature requests are appreciated and can be opened as Github issues.   We also welcome code contributions as pull requests.


# HOW TO CONTRIBUTE
- Fork the Repository: Click the "Fork" button to create your own copy of the repository.
- Clone the Repository: Use the command git clone <your-forked-repo-url> to download it locally.
- Create a New Branch: Run git checkout -b <branch-name> to work on a separate branch.
- Make Your Changes: Modify code, fix bugs, or update documentation as needed.
- Commit Your Changes: Use git commit -m "Descriptive message about your changes" to save your changes locally.
- Push to GitHub: Push the changes to your forked repository with git push origin <branch-name>.
- Create a Pull Request (PR): Go to the original repository and open a pull request explaining your changes.
- Address Feedback: Be ready to discuss and make additional changes if needed during the review process.
