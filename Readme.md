Platinum Pass
=============

Encrypted password management script by Julian Thatcher

Manages passwords.txt.gpg. The user will be asked to input their symmetric key for encryption and decryption.
If passwords.txt is already present, decryption will not occur.

Operations:

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

 This would show password matches for "atlassian"; create a new password
 named BitBucket and open $VISUAL to allow you to add your password; then
 a new commit would be added for the encrypted file
 (message "BitBucket account"); push commits to origin; and finally clean
 up intermediate files.
