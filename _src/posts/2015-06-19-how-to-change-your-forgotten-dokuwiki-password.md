    Title: How To Change Your Forgotten DokuWiki Password
    Date: 2015-06-19T00:06:26
    Tags: dokuwiki, passwords, php 

If you have forgotten your [DokuWiki](https://dokuwiki.org) password, it is possible to set a new password by clicking the _Set New Password_ link on the Login page then following the instructions. DokuWiki will email a new password to you. But what if the email never arrives?

<!-- more -->

The DokuWiki user names and passwords are stored in the file _path-to-dokuwiki-installation/inc/users.auth.php_ in the following format:

    login:passwordhash:Real Name:email:groups,comma,seperated

You cannot simply replace _passwordhash_ with your new password, because the password needs to be hashed first. To hash your password, you can execute the same code that DokiWiki uses, with the interactive mode of PHP.

Enter directory _path-to-docukiwiki-installation/inc_:

    $ cd path-to-docukiwiki-installation/inc

Start PHP interactive mode:

    $ php -a

Import the file that contains the hashing code:

    > require("PassHash.class.php");

Hash your new password:

    > $hasher = new PassHash();
    > echo $hasher->hash_smd5('newpassword');

Copy the output of the last command, and replace the old passwordhash in _path-to-dokuwiki-installation/inc/users.auth.php_ with the new one. Save the file.

Now you can login with your new password.
