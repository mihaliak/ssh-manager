# SSH Manager
SSH Manager is shell script especially for *MacOS* to manage your SSH keys and SSH config hosts.
It is generating SSH keys using `ed25519` and `bcrypt` with 100 rounds.

## Examples
List all SSH keys and hosts in SSH config.
This command is calling both `ssh-manager list-keys` and then `ssh-manager list-host`

    $ ssh-manager list
    ￫ List of available keys:
    - id_ed25519.pub
    - id_ed25519_github.pub
    ￫ List of available hosts in SSH config:
    - production
    - github

Copy public SSH key `id_ed25519_github.pub` to the clipboard.

    $ ssh-manager copy github
    ￫ Success: Your public SSH key id_ed25519_github.pub was successfully copied to the clipboard.

Generate new SSH key.

    $ ssh-manager new
    ￫ Enter key file name: production
    ￫ Enter key comment: your@username
    Generating public/private ed25519 key pair.
    Enter passphrase (empty for no passphrase):
    Enter same passphrase again:
    Your identification has been saved in /Users/nipid/.ssh/id_ed25519_production.
    Your public key has been saved in /Users/nipid/.ssh/id_ed25519_production.pub.
    The key fingerprint is:
    SHA256:xspERr/FFG8ZEwOkO1kziC+Ep+oZMCCx4j39rwkCiGM your@username
    The key's randomart image is:
    +--[ED25519 256]--+
    |.     .  .=o=.   |
    | o   o o = . =   |
    |=   . * + * +    |
    |B . .* o * +     |
    |*E o..o S        |
    |.+...o.+ .       |
    |  o. .o.         |
    | . o. . o        |
    |  o    o..       |
    +----[SHA256]-----+
    ￫ Success: SSH key 'production' was successfully created with comment 'your@username'.

Create new host to SSH config.

    $ ssh-manager host
    ￫ Enter host short name: production
    ￫ Enter host name: production-server.com
    ￫ Enter host port (default 22):
    ￫ Enter host user (default root): username
    ￫ Enter SSH key name (default none): production
    ￫ Would you like to transfer public key id_ed25519_production.pub to server production-server.com (production)? (y|n):
    ￫ Success: SSH host 'production' was successfully added to SSH config.
    ￫          You can now use 'ssh production' to go to SSH.

Remove host from SSH config.
You can also pass host short name as third parameter. `ssh-manager remove production`

    $ ssh-manager remove
    ￫ Enter host short name: production
    ￫ Success: SSH host 'production' was successfully remove from SSH config.

## Help command
    $ ssh-manager
    ￫ Usage: ssh-manager <command>

    Commands:
       help             This help message
       list             List of all SSH keys and hosts in SSH config
       list-keys        List of all SSH keys
       copy             Copy public SSH key
       new              Generate new SSH key
       host             Add host to SSH config, use --key to generate new key
       remove           Remove host from SSH config
       list-host        List of all hosts in SSH config
