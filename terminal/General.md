# File Permisions

**User:** The username of the person who owns the file/directory. By default, the user who creates the file/directory will become its owner.

**Group:** The user group that owns the file/directory. All users who belong to the group that owns the file/directory will have the same access permissions to the file/directory.

**Other:** A user who isn’t the owner of the file/directory and doesn’t belong to the same group the file/directory does. In other words, if you set a permission for the “other” category, it will affect everyone else by default. For this reason, people often talk about setting the “world” permission when they mean setting the permissions for “other."

If you want to view the users on your system, you can view the `/etc/passwd` file by running the following command:

```
cat /etc/passwd
```

Similarly, you can view the groups on your system by viewing the `/etc/group` file, by running the following command:

```
cat /etc/group
```

Linux use 3 types of permissions as follows,

```
1. Read
2. Write
3. Execute
```

1. **Read permission:-**

For a file, the read permission means the file can be opened and read.

For a directory, the read permission means the user can list the contents of the directory.

**2. Write permission:-**

For a file, write permission means the user can modify the file, and write new data to the file.

For a directory, the write permission means the user is allowed to modify the content of the directory. The user can add, remove or rename files belongs to the particular directory.

**3. Execute permission:-**

For a file, execute permission means the user can execute the file as a program or a shell script.

For a directory, the execute permission allows the user to access files in the directory and enter it, with the cd command but you are not allowed to list the content.

***Viewing Permissions\***

You can view the permission of the current directory by typing the following command:

```
ls -l 
```

***Identifying Permissions\***

**r** = read permission
**w** = write permission
**x** = execute permission
**-** = no permission

![Image for post](https://miro.medium.com/max/60/1*H8WEamrDw3tUZ67rGTgyyA.png?q=20)

![Image for post](https://miro.medium.com/max/304/1*H8WEamrDw3tUZ67rGTgyyA.png)

Linux has given values for the above permissions for the ease of use as below.

```
r = 4
w = 2
x = 1
```

***Changing file/directory permissions with ‘chmod’ command\***

We can change the permission given to a file or a directory using ‘chmod’ command.

```
chmod <permission-number> <file-name>
```

Permission number can be calculated using the values assigned for r,w, and x. Basic permission number contains 3 digits. There are some special cases which we use 4 digits number as the permission number. Here we are only discussing the basic permissions.

```
ex: chmod 777 hello.txt
```

7 permission means all read, write and execute permissions are given. Therefore 777 means all read, write and execute permissions are given to the user, group and other owners. Therefore the file contains no privacy.

Assume we need to give following permission to a file.

# rwxrw-r- -\

This means the user has all read, write and execute permissions. Group has read and write permission and the other has read permission only.

Let's calculate the permission number for the above scenario.

***User : r + w + x => 4 + 2 + 1 = 7\***

***Group : r+ w => 4 + 2 = 6\***

***Other : e => 4 = 4\***

Therefore the ultimate 3 digit number is 764. If we need to give above permissions to a file or a directory, following command can be used as calculated.

```
chmod 764 hello.txt
```

Just remember how to calculate this 3 digit number :).



# How to Unzip a ZIP File With the unzip Command

To extract the files from a ZIP file, use the unzip command, and provide the name of the ZIP file. Note that you *do* need to provide the “.zip” extension.

```
unzip source_code.zip
```

![the unzip command in a terminal window](https://www.howtogeek.com/wp-content/uploads/2019/05/xzip_12.png.pagespeed.gp+jp+jw+pj+ws+js+rj+rp+rw+ri+cp+md.ic.xDVuqjvbEm.png)

As the files are extracted they are listed to the terminal window.

![output of unzip in a terminal window](https://www.howtogeek.com/wp-content/uploads/2019/05/xzip_13.png.pagespeed.gp+jp+jw+pj+ws+js+rj+rp+rw+ri+cp+md.ic.FGz1sFCJoS.png)

ZIP files don’t carry details of file ownership. All of the files that are extracted have the owner set to the user who is extracting them.

Just like `zip`, `unzip` has a `-q` (quiet) option, so that you do not need to see the file listing as the files are extracted.

```
unzip -q source_code.zip
```

![unzip -q option in a terminal window](https://www.howtogeek.com/wp-content/uploads/2019/05/xzip_15.png.pagespeed.gp+jp+jw+pj+ws+js+rj+rp+rw+ri+cp+md.ic.oUqVuTKZRh.png)

## unzip - Extracting Files to a Target Directory

To have the files extracted in a specific directory, use the `-d` (directory) option, and provide the path to the directory you wish the archive to be extracted into.

```
unzip -q source_code.zip -d ./development
```

![unzip to a target directory in a terminal window](https://www.howtogeek.com/wp-content/uploads/2019/05/xzip_16.png.pagespeed.gp+jp+jw+pj+ws+js+rj+rp+rw+ri+cp+md.ic.otwmuF9CjV.png)

## Extract Password Protected ZIP Files

If a ZIP file has been created with a password, `unzip` will ask you for the password. If you do not provide the correct password, `unzip` will not extract the files.

```
unzip -q source_code.zip
```

![the unzip with password command in a terminal window](https://www.howtogeek.com/wp-content/uploads/2019/05/xzip_11.png.pagespeed.gp+jp+jw+pj+ws+js+rj+rp+rw+ri+cp+md.ic.OZqOCa7Ssn.png)

If you don’t care about your password being seen by others—nor about it being stored in your command history—you can provide the password on the command line with the `-P` (password) option. (You must use a capital “P.”)

```
unzip -P fifty.treacle.cutlass -q source_code.zip
```

![unzipping with password option in a terminal window](https://www.howtogeek.com/wp-content/uploads/2019/05/xzip_18.png.pagespeed.gp+jp+jw+pj+ws+js+rj+rp+rw+ri+cp+md.ic.YnJHTHUy_7.png)

# **Extracting .tar.gz files**

1) If your *tar* file is compressed using a *gzip* compressor, use this command to uncompress it.

> $ tar xvzf file.tar.gz

Where,

**x:** This option tells *tar* to extract the files.

**v:** The “v” stands for “verbose.” This option will list all of the files one by one in the archive.

**z:** The *z option* is very important and tells the *tar* command to uncompress the file (*gzip*).

**f:** This options tells *tar* that you are going to give it a file name to work with.

A tarball is a group or archive of files that are bundled together using the tar command and have the .tar file extension.

Eg:

[![How To Extract .tar.gz Files using Linux Command Line](https://www.interserver.net/tips/wp-content/uploads/2017/01/How-To-Extract-.tar.gz-Files-using-Linux-Command-Line1.png)](https://www.interserver.net/tips/wp-content/uploads/2017/01/How-To-Extract-.tar.gz-Files-using-Linux-Command-Line1.png)

 

2)  To uncompress tar.gz file into a different directory, use the command below:

> $ tar xvzf file.tar.gz -C /path/to/somedirectory

Where the -C argument is used to specify the path to place the file.  By defaults files will be extracted into the current directory. To  change the directory, we use -C option.

Eg:

[![How To Extract .tar.gz Files using Linux Command Line](https://www.interserver.net/tips/wp-content/uploads/2017/01/How-To-Extract-.tar.gz-Files-using-Linux-Command-Line2.png)](https://www.interserver.net/tips/wp-content/uploads/2017/01/How-To-Extract-.tar.gz-Files-using-Linux-Command-Line2.png)

 

 

3) To extract test.doc file from the file.tar.gz tarball, use the following command:

> $ tar -xvzf file.tar.gz test.doc

Eg:

[![How To Extract .tar.gz Files using Linux Command Line](https://www.interserver.net/tips/wp-content/uploads/2017/01/How-To-Extract-.tar.gz-Files-using-Linux-Command-Line4.png)](https://www.interserver.net/tips/wp-content/uploads/2017/01/How-To-Extract-.tar.gz-Files-using-Linux-Command-Line4.png)

 

4) To view a detailed table of content by listing all files in archive, you can use the following command:

> $ tar -tvf file.tar.gz

Eg:

[![How To Extract .tar.gz Files using Linux Command Line](https://www.interserver.net/tips/wp-content/uploads/2017/01/How-To-Extract-.tar.gz-Files-using-Linux-Command-Line5.png)](https://www.interserver.net/tips/wp-content/uploads/2017/01/How-To-Extract-.tar.gz-Files-using-Linux-Command-Line5.png)