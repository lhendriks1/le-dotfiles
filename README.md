## My Dotfiles

1. First clone this repo (see intructions below for installing and using gh cli). 
2. Then run install.sh and install.next.sh.

---
###Instructions to set up separate Github and Bitbucket accounts:
https://gist.github.com/rosswd/e1afd2b0b0d515517eac

Setting up github and bitbucket on the same computer (Mac OS)
Github will be the main account and bitbucket the secondary.

Intall Git
Use Homebrew to install Git.

Configure Git
git config --global user.name "Your Name"
git config --global user.email "username@email.com"
Confirm changes: git config --global -l

Create SSH Keys
ssh-keygen -t rsa -C "github email"

Enter passphrase when prompted. If you see an option to save the passphrase in your keychain, do it for an easier life.

Save keys to:

~/.ssh/id_rsa

Repeat for bitbucket:

ssh-keygen -t rsa -C "bitbucket email"

Save bitbucket key to ~/.ssh/id_rsa_bb

Attach Keys
Login to remote repo and add ssh key:

pbcopy < ~/.ssh/id_rsa.pub
pbcopy < ~/.ssh/id_rsa_bb.pub
Obviously run each pbcopy command individually.

Paste into text area, under ssh settings, in your github or bitbucket account. Also give the ssh key a title like "your name" Laptop.

Create Config file
I am using vim, enter your editor here if different:

vim ~/.ssh/config

Create your git aliases like so:

#Github (default)
Host gh
HostName github.com
User git
IdentityFile ~/.ssh/id_rsa

#Bitbucket (secondary)
Host bb
HostName bitbucket.org
User git
IdentityFile ~/.ssh/id_rsa_bb
Note: On Mac OS Sierra onwards you have to add this to the top of the config file:

Host *
UseKeychain yes
AddKeysToAgent yes
Add the identities to SSH:
ssh-add ~/.ssh/id_rsa
ssh-add ~/.ssh/id_rsa_bb
Enter passphrase if prompted.

Check keys were added:

ssh-add -l

Check that repo recognizes keys:
ssh -T gh
ssh -T bb

For the secondary account, the username and email have to be overwritten, using secondary account values, at the repo level:

git config user.name "Full Name"
git config user.email email_address
This must be done once for every secondary (e.g. github) repo, it is not needed for github (or primary) repos because the global is used in that scenario. There may be a cleaner way to do this but right now it works okay.

Just to be clear you do not need to change these values back afterwards because the global values (which apply to all future repos created) will be set.

