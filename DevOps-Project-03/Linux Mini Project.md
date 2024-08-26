# Fun with Linux for Cloud & DevOps Engineers

![linux](https://imgur.com/VpPW8PM.png)

***New to Linux? Below assignment covering all the required basics of Linux to be familiar for an DevOps engineer.***

![Linux](https://imgur.com/xedzuwy.png)

## Skills

Below skills are required to complete the deployment steps:

Linux User Management, Permissions, Directory Structure, File Systems, File Management

Certainly! You can perform all the deployment steps outlined in your assignment directly on your local Linux system without needing AWS EC2 or any other cloud services. Below is a comprehensive guide along with the necessary commands to help you complete each task. 

## **Prerequisites**

1. **Linux System**: Ensure you have a Linux distribution installed (e.g., Ubuntu, CentOS, Fedora).
2. **Superuser Access**: You need `root` privileges or access to `sudo` to perform administrative tasks.
3. **Terminal Access**: Access to the terminal to execute commands.

## **Deployment Steps**

### **1. Log in as Super User**

Open your terminal and switch to the `root` user:

```bash
sudo -i
```

Alternatively, if you're already the root user, you can skip this step.

### **2. Create Users and Set Passwords**

Create three users: `user1`, `user2`, and `user3`.

```bash
adduser user1
# You will be prompted to set a password and provide additional information.

adduser user2
adduser user3
```

Set passwords for each user (if not prompted during user creation):

```bash
passwd user1
passwd user2
passwd user3
```

### **3. Create Groups**

Create two groups: `devops` and `aws`.

```bash
groupadd devops
groupadd aws
```

### **4. Modify User Groups**

- **Change Primary Group of `user2` and `user3` to `devops`:**

```bash
usermod -g devops user2
usermod -g devops user3
```

- **Add `aws` as a Secondary Group to `user1`:**

```bash
usermod -aG aws user1
```

*Note: The `-aG` option appends the group without removing existing secondary groups.*

### **5. Create File and Directory Structure**

Since the original instructions mention a diagram for the directory structure, we'll make reasonable assumptions based on the tasks. Here's an example structure based on the commands mentioned:

```
/
├── dir1
│   └── f1
├── dir2
│   └── dir1
│       └── dir2
├── dir3
├── dir4
├── dir5
├── dir6
│   └── dir4
├── dir7
│   └── dir10
├── dir8
├── opt
│   └── dir14
│       └── dir10
├── f2
├── f3
└── f4
```

Create the directories and files:

```bash
mkdir -p /dir1
touch /dir1/f1

mkdir -p /dir2/dir1/dir2

mkdir /dir3
mkdir /dir4
mkdir /dir5
mkdir -p /dir6/dir4
mkdir /dir7/dir10
mkdir /dir8
mkdir -p /opt/dir14/dir10

touch /f2
```

### **6. Change Group Ownership**

Change the group of `/dir1`, `/dir7/dir10`, and `/f2` to `devops`:

```bash
chgrp devops /dir1
chgrp devops /dir7/dir10
chgrp devops /f2
```

### **7. Change Ownership**

Change the ownership of `/dir1`, `/dir7/dir10`, and `/f2` to `user1`:

```bash
chown user1:devops /dir1
chown user1:devops /dir7/dir10
chown user1:devops /f2
```

### **8. Perform Actions as `user1`**

#### **a. Create Users `user4` and `user5`**

Switch to `user1`:

```bash
su - user1
```

Create `user4` and `user5` (Note: As `user1` might not have sudo privileges by default, you may need to switch back to root or ensure `user1` has the necessary permissions. For simplicity, perform these steps as `root`):

```bash
exit  # Return to root
adduser user4
adduser user5
passwd user4
passwd user5
```

#### **b. Create Groups `app` and `database`**

```bash
groupadd app
groupadd database
```

### **9. Perform Actions as `user4`**

Switch to `user4`:

```bash
su - user4
```

#### **a. Create Directory `/dir6/dir4`**

```bash
mkdir -p /dir6/dir4
```

#### **b. Create File `/f3`**

```bash
touch /f3
```

#### **c. Move File from `/dir1/f1` to `/dir2/dir1/dir2`**

```bash
mv /dir1/f1 /dir2/dir1/dir2/
```

#### **d. Rename `/f2` to `/f4`**

```bash
mv /f2 /f4
```

*Note: Depending on permissions, you might need `sudo` to perform these actions. If `user4` lacks permissions, you may need to execute these commands as `root`.*

### **10. Perform Actions as `user1`**

Switch back to `user1`:

```bash
exit  # Return to root
su - user1
```

#### **a. Create Directory `/home/user2/dir1`**

```bash
mkdir -p /home/user2/dir1
```

*Ensure `user1` has the necessary permissions to create directories in `user2`'s home.*

#### **b. Change to `/dir2/dir1/dir2/dir10` and Create File Using Relative Path**

Navigate to `/dir2/dir1/dir2/dir10`:

```bash
cd /dir2/dir1/dir2/dir10
```

Create file `/opt/dir14/dir10/f1` using a relative path. Assuming relative to current directory:

Since `/opt/dir14/dir10/f1` is an absolute path, to use relative path from `/dir2/dir1/dir2/dir10`:

Calculate relative path from current directory to `/opt/dir14/dir10/f1`.

Assuming `/opt/dir14/dir10` is a sibling to `/dir2`, then:

But better to use a loopback or symlink. To simplify, perform:

```bash
touch ../../../../opt/dir14/dir10/f1
```

Alternatively:

```bash
cd /dir2/dir1/dir2/dir10
touch ../../../opt/dir14/dir10/f1
```

But relative path needs to be clarified. For accuracy:

From `/dir2/dir1/dir2/dir10`, the relative path to `/opt/dir14/dir10/f1` is:

- From `/dir2/dir1/dir2/dir10` to `/opt/dir14/dir10/f1`:
  - Navigate up to `/`:

```bash
touch ../../../../opt/dir14/dir10/f1
```

This command navigates up four levels:

- `/dir2/dir1/dir2/dir10` → `/dir2/dir1/dir2` → `/dir2/dir1` → `/dir2` → `/`

Then to `/opt/dir14/dir10/f1`.

#### **c. Move File from `/opt/dir14/dir10/f1` to `user1` Home Directory**

Assuming `user1`'s home directory is `/home/user1`:

```bash
mv /opt/dir14/dir10/f1 /home/user1/
```

### **11. Delete Directory `/dir4` Recursively**

```bash
rm -rf /dir4
```

### **12. Delete All Child Files and Directories Under `/opt/dir14` Using a Single Command**

```bash
rm -rf /opt/dir14/*
```

### **13. Write Text to `/f3`**

```bash
echo "Linux assessment for an DevOps Engineer!! Learn with Fun!!" > /f3
```

### **14. Perform Actions as `user2`**

Switch to `user2`:

```bash
exit  # Return to root
su - user2
```

#### **a. Create File `/dir1/f2`**

```bash
touch /dir1/f2
```

#### **b. Delete `/dir6` and `/dir8`**

```bash
rm -rf /dir6
rm -rf /dir8
```

#### **c. Replace "DevOps" with "devops" in `/f3` Without Using an Editor**

Use `sed` for in-place substitution:

```bash
sed -i 's/DevOps/devops/g' /f3
```

#### **d. Copy Line 1 and Paste 10 Times in `/f3` Using `vi` Editor**

Since the requirement is to use `vi`, here's how:

1. Open `/f3` in `vi`:

    ```bash
    vi /f3
    ```

2. In `vi`:

    - Press `Esc` to ensure you're in command mode.
    - Copy the first line into a buffer:

        ```vi
        :1y
        ```

    - Paste it 10 times:

        ```vi
        :.,$y | 10p
        ```

    Alternatively, more straightforward:

    - Move to the first line.
    - Yank the line:

        ```vi
        yy
        ```

    - Paste it 10 times by pressing `p` ten times or use a command:

        ```vi
        10p
        ```

    - Save and exit:

        ```vi
        :wq
        ```

3. Alternatively, from the command line, you can use `awk` or `sed` to automate it, but since the requirement is to use `vi`, manual steps are necessary.

#### **e. Search and Replace "Engineer" with "engineer" in `/f3` Using a Single Command**

Use `sed` for in-place substitution:

```bash
sed -i 's/Engineer/engineer/g' /f3
```

#### **f. Delete `/f3`**

```bash
rm /f3
```

### **15. Perform Actions as `root` User**

Switch back to `root`:

```bash
exit  # Return to user2
sudo -i
```

#### **a. Search for File Name `f3` and List Absolute Paths**

Use `find` command:

```bash
find / -type f -name f3 2>/dev/null
```

*Explanation:*
- `/`: Start searching from the root directory.
- `-type f`: Look for files.
- `-name f3`: File name exactly `f3`.
- `2>/dev/null`: Suppress permission denied errors.

#### **b. Show the Count of the Number of Files in the Directory `/`**

Use `find` to count all files (including directories and special files):

```bash
find / | wc -l
```

*Note:* This counts all files and directories recursively under `/`.

If you only want to count files (excluding directories):

```bash
find / -type f 2>/dev/null | wc -l
```

#### **c. Print the Last Line of the File `/etc/passwd`**

Use `tail`:

```bash
tail -n 1 /etc/passwd
```

### **16. Create and Manage a New File System**

Since AWS EBS volumes are not applicable to a local system, you can simulate this by creating a loopback device or using a new partition. Here's how to create a loopback file to act as a separate file system.

#### **a. Create a 5GB Loopback File**

```bash
dd if=/dev/zero of=/root/loopback.img bs=1M count=5120
```

*Explanation:*
- `if=/dev/zero`: Input file is a stream of zeros.
- `of=/root/loopback.img`: Output file.
- `bs=1M`: Block size 1 Megabyte.
- `count=5120`: Total size 5120 MB (5 GB).

#### **b. Create a File System on the Loopback File**

Choose a file system type, e.g., `ext4`.

```bash
mkfs.ext4 /root/loopback.img
```

#### **c. Mount the File System on `/data` Directory**

1. Create the `/data` directory if it doesn't exist:

    ```bash
    mkdir /data
    ```

2. Mount the loopback file:

    ```bash
    mount -o loop /root/loopback.img /data
    ```

#### **d. Verify File System Utilization**

```bash
df -h | grep /data
```

You should see an entry for `/data` with the appropriate size.

#### **e. Create File `f1` in `/data` File System**

```bash
touch /data/f1
```

### **17. Perform Actions as `user5`**

Switch to `user5`:

```bash
exit  # Return to root
su - user5
```

#### **a. Delete Directories and Files**

```bash
rm -rf /dir1
rm -rf /dir2
rm -rf /dir3
rm -rf /dir5
rm -rf /dir7
rm /f1
rm /f4
rm -rf /opt/dir14
```

*Note:* Ensure `user5` has the necessary permissions to delete these directories and files. If not, perform these deletions as `root`.

### **18. Perform Final Cleanup as `root` User**

Switch back to `root`:

```bash
exit  # Return to user5
sudo -i
```

#### **a. Delete Users**

```bash
userdel -r user1
userdel -r user2
userdel -r user3
userdel -r user4
userdel -r user5
```

*Explanation:*
- `-r`: Removes the home directory and mail spool.

#### **b. Delete Groups**

```bash
groupdel app
groupdel aws
groupdel database
groupdel devops
```

#### **c. Delete Home Directories (If Any Still Exist)**

This step is redundant if you used `userdel -r` above, but to ensure:

```bash
rm -rf /home/user1
rm -rf /home/user2
rm -rf /home/user3
rm -rf /home/user4
rm -rf /home/user5
```

#### **d. Unmount `/data` File System**

```bash
umount /data
```

#### **e. Delete `/data` Directory**

```bash
rmdir /data
```

### **19. Clean Up the Loopback File**

To remove the loopback file created earlier:

```bash
rm /root/loopback.img
```

*Note:* Ensure that `/data` is unmounted before deleting the loopback file.

### **20. Verify All Steps**

Review your system to ensure all users, groups, directories, and files have been appropriately created and deleted as per the steps.

---

## **Summary of Commands**

For convenience, here’s a summarized list of commands based on the above steps:

```bash
# Switch to root
sudo -i

# Create users
adduser user1
adduser user2
adduser user3
passwd user1
passwd user2
passwd user3

# Create groups
groupadd devops
groupadd aws

# Modify user groups
usermod -g devops user2
usermod -g devops user3
usermod -aG aws user1

# Create directories and files
mkdir -p /dir1
touch /dir1/f1
mkdir -p /dir2/dir1/dir2
mkdir /dir3
mkdir /dir4
mkdir /dir5
mkdir -p /dir6/dir4
mkdir /dir7/dir10
mkdir /dir8
mkdir -p /opt/dir14/dir10
touch /f2

# Change group ownership
chgrp devops /dir1
chgrp devops /dir7/dir10
chgrp devops /f2

# Change ownership
chown user1:devops /dir1
chown user1:devops /dir7/dir10
chown user1:devops /f2

# Create additional users and groups as root
adduser user4
adduser user5
passwd user4
passwd user5
groupadd app
groupadd database

# Switch to user4 and perform tasks
su - user4
mkdir -p /dir6/dir4
touch /f3
mv /dir1/f1 /dir2/dir1/dir2/
mv /f2 /f4
exit

# Switch to user1 and perform tasks
su - user1
mkdir -p /home/user2/dir1
cd /dir2/dir1/dir2/dir10
touch ../../../../opt/dir14/dir10/f1
mv /opt/dir14/dir10/f1 /home/user1/
rm -rf /dir4
rm -rf /opt/dir14/*
echo "Linux assessment for an DevOps Engineer!! Learn with Fun!!" > /f3
exit

# Switch to user2 and perform tasks
su - user2
touch /dir1/f2
rm -rf /dir6
rm -rf /dir8
sed -i 's/DevOps/devops/g' /f3
# Perform vi operations manually as described
sed -i 's/Engineer/engineer/g' /f3
rm /f3
exit

# Switch to root and perform final tasks
sudo -i
find / -type f -name f3 2>/dev/null
find / | wc -l
tail -n 1 /etc/passwd

# Create and manage a loopback file system
dd if=/dev/zero of=/root/loopback.img bs=1M count=5120
mkfs.ext4 /root/loopback.img
mkdir /data
mount -o loop /root/loopback.img /data
df -h | grep /data
touch /data/f1

# Switch to user5 and perform deletions
su - user5
rm -rf /dir1
rm -rf /dir2
rm -rf /dir3
rm -rf /dir5
rm -rf /dir7
rm /f1
rm /f4
rm -rf /opt/dir14
exit

# Switch back to root for final cleanup
sudo -i
userdel -r user1
userdel -r user2
userdel -r user3
userdel -r user4
userdel -r user5
groupdel app
groupdel aws
groupdel database
groupdel devops
rm -rf /home/user1 /home/user2 /home/user3 /home/user4 /home/user5
umount /data
rmdir /data
rm /root/loopback.img
```

## **Notes and Considerations**

1. **Permissions**: Ensure that users have the necessary permissions to perform the tasks. If a user lacks permissions, some commands may fail. You might need to grant `sudo` privileges to certain users if required.

2. **Safety**: Be cautious with `rm -rf` commands, especially when running as `root`, as they can irreversibly delete important data. Double-check paths before executing these commands.

3. **Directory Structure Assumptions**: The exact directory structure was inferred based on the tasks. Adjust the `mkdir` commands if your assignment specifies a different structure.

4. **Loopback File System**: Since AWS EBS volumes are not applicable, the loopback file system is used to simulate an additional storage device. This approach allows you to practice mounting and managing file systems locally.

5. **Using `vi` for Multiple Paste Operations**: The `vi` operations require manual interaction. If you prefer automation, consider using scripts or other command-line tools, but ensure you meet the assignment requirements.

6. **Cleaning Up**: Always ensure that you clean up resources (like loopback files and mounted file systems) to maintain system integrity and free up disk space.

7. **User Management**: The `userdel -r` command removes both the user and their home directory. If you skip the `-r` option, you'll need to manually delete the home directories.

8. **Mount Persistence**: The loopback mount is temporary and will not persist across reboots. If you need persistence, consider adding an entry to `/etc/fstab`, but this is optional for your assignment.

9. **Simulating AWS EBS Operations**: The loopback approach is a basic simulation. For more advanced storage management, you could explore using Logical Volume Manager (LVM) or setting up separate partitions.

10. **Error Handling**: If any command fails, review the error message to understand the issue, which might be related to permissions, incorrect paths, or syntax errors.

## **Conclusion**

By following the steps outlined above, you can successfully perform user management, group management, file and directory operations, and file system management on your local Linux system. This hands-on approach will help you understand essential Linux administration tasks typically required for a DevOps Engineer role.



#### Author by [Devops Institute Mumbai]()
