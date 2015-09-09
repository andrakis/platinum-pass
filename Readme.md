Platinum Pass
=============

Encrypted password management script, designed to be run from the commandline.
The passwords file is committed to git in an encrypted manner.

For best results, you should have your own (private) git repository in which to commit your updated passwords.txt.gpg to.

Getting Started
---------------

1. Clone the git repository to "platinum-vault"
```
   git clone --bare git@github.com:andrakis/platinum-pass platinum-vault
```
2. Clone the cloned repository. This will ensure all commits will be pushed to your local machine.
```
    git clone platinum-vault platinum-pass
```
3. Add platinum pass to your PATH
```
    export PATH=`readlink -f platinum-pass`/bin:$PATH
```
4. Create your first password and save the file
```
    pw -c Test
```
5. Commit your changes to passwords.txt and push. You will be prompted for your password.
```
    pw commit "Initial passwords.txt commit" push
```

You may want to add the export line in step 3 to your .bashrc file.

After this, you may run pw to search for passwords:

    pw search test

How it works
------------
Manages passwords.txt.gpg, which lives in this repository. The user will be asked to input their symmetric key for encryption and decryption.
If passwords.txt is already present, decryption will not occur.

If there is no passwords.txt.gpg file present, you do not yet have any passwords. Add a password and encrypt (see Getting Started.)

Git is used to keep track of the encrypted passwords.txt.gpg file. This means that diffs generally will not work.
However a command, "diff", has been added to the script to show you differences.

Operations
----------

    pw clean              Clean intermediate files
    pw atlassian          Search for "atlassian" in password file
    pw search atlassian   Same as above
    pw --                 Consider the rest of the line to be searches, not commands
    pw -c NameOfService   Create a new service and open $VISUAL on the file
    pw edit               Edit the passwords file
    pw encrypt            Encrypt the passwords file
    pw commit "Message"   Commit the pending changes to git
    pw push               Push the pending changes
    pw status             Display status
    pw list               Display passwords
    pw diff               Display diff between current passwords.txt and encrypted
                          version of the file. You will be asked for the password.

Operations can be combined, and are run sequentially.
Eg:

    pw atlassian -c BitBucket commit "BitBucket account" push clean

This would show password matches for "atlassian"; create a new password named BitBucket and open $VISUAL to allow you to add your password; then a new commit would be added for the encrypted file (message "BitBucket account"); push commits to origin; and finally clean up intermediate files.
