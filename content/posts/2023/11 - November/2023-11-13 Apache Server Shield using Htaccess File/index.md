---
title: "Shield for Apache Server using htaccess/htpasswd"
date: 2023-11-13
tags: ["#Other"]
---


# Intuition
In some cases, drupal shield may not be available, or is very risky to use; I've ran into occasions where I've enabled drupal shield, and get compeltely blocked out of the system. (Trust me, I've tried putting numerous different "disable shield" command in the `settings.php`, and in those occasions none of them worked !).

That brings me to the good old apache method of htpasswd of which: is used to create and update the flat-files used to store usernames and password for basic authentication of HTTP users. If htpasswd cannot access a file, such as not being able to write to the output file or not being able to read the file in order to update it, it returns an error status and makes no changes."

As long I have the access to the server filebase, I can always make a change to the `.htpasswd` and `.htaccess`, remove the relevant the lines or change the username/password when I need to. As a resulte, I've been using htaccess as a manual replacement for the "Drupal Shield" whenever I smell sighs of danger :O.


# Add username/password to `.htpasswd` file
(or create `.htpasswd` file with username/password)

In case you don't have the `htpasswd` file, you can create it with linux `htpasswd` command along with the `-c` parameter (which means create file); For example, `htpasswd -c ../public_html/.htpasswd simon_who`, then you will be prompted to enter the password, press "enter" and you will get a new `.htpasswd` file, with just one line of "username" and "hashed password" together (Note: `htpasswd` encrypts passwords using either bcrypt, a version of MD5 modified for Apache, SHA1, or the system's crypt() routine. Files managed by htpasswd may contain a mixture of different encoding types of passwords; some user records may have bcrypt or MD5-encrypted passwords while others in the same file may have passwords encrypted with crypt().)

```
> htpasswd -c ../public_html/.htpasswd simon_who
> Enter Password:
>      simon_who_super_secret_password
> cat ../public_html/.htpasswd
>      simon_who:{SHA}b1ZEA/D3********UXtw1nDQJN43OENE=
```

In case you already have the `htpasswd` file, you may use the `htpasswd` command by itself, and it will append your new user to the exsiting file without effecting the other users.

```
> htpasswd -c ../public_html/.htpasswd jerry_smi
> Enter Password:
>      jerry_smi_super_secret_password
> cat ../public_html/.htpasswd
>      simon_who:{SHA}b1ZEA/D3********UXtw1nDQJN43OENE=
>      jerry_smi:{SHA}d3LAS/D3********KLJ8990cu0asdSDK=

```

# Reference the `.htpasswd` file through `.htaccess` file
Once we have the the `.htpasswd` file setup, we will need to reference it from the `.htaccess` file in order to take effect, add the following lines into the htacecss file:
```
AuthType Basic                                 # Defines the type of authentication the web server will use, ‘Basic’ is perfectly adequate for what we need.
AuthName "My Protected Folder"                 # Sets the title of the username/password box that will popup when someone tries to view your protected page.
AuthUserFile ../public_html/.htpasswd          # Tells the web server where to find the username/password file.
require valid-user                             # Tells the web server who in your .htpasswd file can access your folder, by using valid-user everyone in the file can view the folder.
```

----

## Reference
- [LINK-1: How to password protect a website folder using .htaccess](https://www.lcn.com/support/articles/how-to-password-protect-a-folder-on-your-website-with-htaccess/)
- [LINK-2: Generate htaccess password (htpasswd) from the command line](https://docs.gaslamp.media/generate-htaccess-password-htpasswd-from-the-command-line/)
- [LINK-3: Password protecting your site with an .htaccess file (NOT RECOMMENDED)](https://help.dreamhost.com/hc/en-us/articles/216363187-Password-protecting-your-site-with-an-htaccess-file)
- [LINK-4: htpasswd - Manage user files for basic authentication](https://httpd.apache.org/docs/2.4/programs/htpasswd.html)