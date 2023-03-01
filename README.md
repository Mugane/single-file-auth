# Simple PHP Authorization (login/pass)
Login form and authorization (hashed login/pass) for single PHP files
## Features
- Timeout after a customizable period `$timeout` (defaults to 15 minutes)
- Allow multiple logins in hashed `$credentials` array (defaults to "admin" and "password")
- Add custom `$salt` (defaults to none)
- Set a maximum number of failed login attempts via `$max_logins` (default 5)
- Set a minimum number of hours before a user may retry logging in after exceeding the maximum failed logins via `$ban_time` (defaults to 24). This is not super secure, since using a different computer/clearing cookies would allow retrying the login anyway. A better way (not implemented) would be to store the usernames that were tried (if they exist) on the server (in a text file for example) and block those. Or interface to fail2ban and block the IP. Also, it would be better to silently reject logins after banning (even if correct), instead of displaying a notice indicating that there was a ban. 
- Set a maximum login time (even if there is activity) via `$max` (defaults to 86400 seconds/one day)
## Usage
`include '/path/to/auth.php';` in your script. Make sure you modify the `$credentials` array and other optionally customizable parameters to store sha256 hashes of your username/passwords. To generate a sha256 hash of a string in bash, use `echo $(echo -n "texttohash" | sha256sum | cut -d " " -f1)`
