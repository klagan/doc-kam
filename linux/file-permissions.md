# File permissions

Changing Permissions

chmod 705 <directory_name>

705 = r_x read and execute

The chmod command is used to change the permissions of a file or directory. To use it, you specify the desired permission settings and the file or files that you wish to modify. There are two ways to specify the permissions, but I am only going to teach one way.
It is easy to think of the permission settings as a series of bits (which is how the computer thinks about them). Here's how it works:
rwx rwx rwx = 111 111 111
rw- rw- rw- = 110 110 110
rwx --- --- = 111 000 000

and so on...

rwx = 111 in binary = 7
rw- = 110 in binary = 6
r-x = 101 in binary = 5
r-- = 100 in binary = 4

Now, if you represent each of the three sets of permissions (owner, group, and other) as a single digit, you have a pretty convenient way of expressing the possible permissions settings. For example, if we wanted to set some_file to have read and write permission for the owner, but wanted to keep the file private from others, we would:
[me@linuxbox me]$ chmod 600 some_file

Source: http://linuxcommand.org/lc3_lts0090.php


ls -la       — list with permissions

sudo chown -R 777 root:www-data /var/www

sudo adduser yourusername group
sudo adduser root www-data

To change all the directories to 755 (drwxr-xr-x):
find /opt/lampp/htdocs -type d -exec chmod 755 {} \;
To change all the files to 644 (-rw-r--r--):
find /opt/lampp/htdocs -type f -exec chmod 644 {} \;

find /var/www -type f -exec chmod 777 {} \;