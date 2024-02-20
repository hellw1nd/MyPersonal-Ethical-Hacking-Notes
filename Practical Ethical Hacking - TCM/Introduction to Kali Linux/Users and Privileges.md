`ls -la` - list long all
![[Pasted image 20240112181927.png]]


### So we will explore more about the user privileges.
- let's echo 'hello' in the home directory  
	-┌──(kali㉿kali)-[~]
	└─$ echo 'Hello' > test.txt


![[Pasted image 20240114090337.png]]
- we can change the Privileges by using chmod +anything we want (name of file) - chmod +rwx test.txt
- instead of using +rwxr that so much complicated if we can't remember what permission we want to enable on a file system we can use chmod 777 (name of file) chmod 777 test.txt

![[Pasted image 20240114090821.png]]

![[Pasted image 20240114091235.png]]
- so for every dash represent a placeholder in binary like r-w-x it means that we have 7 total coz this is how it works 0-0-0 so we assume that for every letter in the place holder are equivalent to its value we will count like 4-2-1 = 7 (r = 4, w = 2 and x = 1) so 777 means full permission
##### In the `ls -la` output, the "rwx" refers to the permissions associated with a file or directory. The permissions are displayed for three different entities: the owner, the group, and other users. Each entity has three permission categories: read (r), write (w), and execute (x). Here's a breakdown of what each permission category represents:

- Read (r): Allows the entity to read or view the contents of a file or the names of files within a directory.
- Write (w): Enables the entity to modify or write to a file or add, delete, or rename files within a directory.
- Execute (x): Grants the entity the permission to execute a file or enter a directory. For directories, execute permission is required to access its contents.

In the `ls -la` output, the permissions are displayed as a series of nine characters. The first character represents the file type (e.g., `-` for a regular file, `d` for a directory). The next three characters represent the owner's permissions, followed by the group's permissions, and then the permissions for other users.

For example, let's consider an `ls -la` output line:

-rwxr-x--- 1 user group 4096 May 10 12:34 myfile.txt 

In this example, the permissions are broken down as follows:

- `-rwxr-x---`: The first character indicates that it is a regular file. The following three characters (`rwx`) represent the owner's permissions (read, write, and execute). The next three characters (`r-x`) represent the group's permissions (read and execute). The last three characters (`---`) represent the permissions for other users (no permissions).
- `1`: Indicates the number of hard links to the file.
- `user`: Refers to the owner of the file.
- `group`: Refers to the group assigned to the file.
- `4096`: Indicates the file size in bytes.
- `May 10 12:34`: Specifies the date and time of the last modification.
- `myfile.txt`: Represents the name of the file.

It's worth noting that if a permission is not granted for a particular entity, a hyphen (`-`) is displayed in its place. Additionally, the output can include additional information such as special permissions, ownership, and timestamps.  

Here are explanations and examples of the commands mentioned in this video. Please note, Teachable blocks the mention of some of the sensitive paths shown in the video, so we cannot display them in text format here:

`chmod` (Change Mode):

- - Explanation: Changes the permissions of a file or directory.
    - Example: Running `chmod +x script.sh` would add the execute permission to the file "script.sh", allowing it to be executed as a script.

`adduser`:

- - Explanation: Creates a new user account.
    - Example: Running `adduser john` would create a new user account with the username "john" and prompt for additional user information.

`su` (Switch User):

- - Explanation: Allows a user to switch to another user account.
    - Example: Running `su jane` would switch to the user account "jane" after entering the password for that account.

`/etc/sudoers`:

- - Explanation: Displays the content of the "/etc/sudoers" file, which contains configuration information for the `sudo` command.
    - Example: Running `/etc/sudoers` would display the configuration directives for `sudo` access and permissions.

`sudo -l`:

- - Explanation: Lists the commands a user is allowed to run with `sudo` privileges.
    - Example: Running `sudo -l` would display the commands and permissions available to the current user with `sudo` access.

Please note that some of these commands require administrative privileges, and caution should be exercised when modifying system files or working with user accounts.