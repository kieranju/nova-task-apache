### Static Files

- **httpd.conf.default** — Apache server configuration. Instruct how the HTTP server should operate globally.

## Environment

1. Install [Homebrew](https://brew.sh).

2. Execute `brew install httpd`.

3. Execute `sudo apachectl stop`.

4. Check [localhost](http://localhost/) and [localhost on port 8080](http://localhost:8080/) in your web browser to confirm that there are no running Apache processes. The page should not return a response.

5. Execute `sudo launchctl unload -w /System/Library/LaunchDaemons/org.apache.httpd.plist 2>/dev/null` to prevent the default Apache process from starting with the system.

6. Execute `brew install php@7.4`

   - Other versions of php can be installed and unlinked/linked as needed. For example: `brew unlink php@7.4` then `brew link php@7.5` to switch from PHP 7.4 to 7.5.

7. Copy and rename the project file `httpd.conf.default` to `httpd.conf` and make adjustments as necessary.

   - In Nova code editor, the Build action in the Apache task will copy `httpd.conf` and make the necessary modifications automatically.

   - In Nova code editor, the Clean action in the Apache task will remove error and log files that are created by the running Apache process.

8. Execute `apachectl start -f $(pwd)/httpd.conf` to start the Apache process.

   - In Nova code editor, the Run action in the Apache task will start the Apache process.

9. Execute `apachectl stop -f $(pwd)/httpd.conf` to stop the Apache process.

   - In Nova code editor, stopping the Run action in the Apache task will stop the running Apache process. It will also stop itself if it detects the process has been closed elsewhere.
   
## Modules

### XSendFile

mod_xsendfile is a module that allows you to instruct Apache to send a file. It is most useful when performing access checks in PHP, so you could allow or deny access to certain files depending on authentication or other metrics.

Download and follow the instructions to enable this module: https://github.com/nmaier/mod_xsendfile

I am also looking for a better way to install modules like this one directly through homebrew.