**UGO:**



* Represents the different categories of users who can interact with files and directories, and thus, have associated permissions to perform actions on them.
* **U (User):** This refers to the owner of the file or directory. Typically, this is the user who initially created the file.
* **G (Group):** This refers to the group that the file or directory belongs to. Other users within that same group will have the permissions assigned to the group.
* **O (Others):** This refers to all other users on the system who are neither the owner nor part of the owning group.



---



**Permissions assigned to UGO**



Permissions define what actions users within each category (User, Group, Others) can perform on a file or directory. The three main types of permissions are:



* r (Read): Allows viewing the contents of a file or listing the contents of a directory.
* w (Write): Allows modifying the contents of a file or creating/deleting files within a directory.
* x (Execute): Allows running a file (if it's an executable program) or accessing/traversing into a directory.



---



* To change permissions, we use the **chmod** command.
* The permissions for the user, group and others can be modified separately using either symbolic notation (letters) or numeric notation (octal values).



SYMBOLIC METHOD:



* Uses lettrs to represent user classes (u, g, o, or a for all) and permissions (r, w, x).
* Uses (+) to add permissions, (-) to remove permissions, and (=) to explicitly set permissions.



Eg:



* chmod u+x filename
* chmod g-w filename
* chmod ugo=rx filename
* chmod a=r filename



NUMERIC METHOD:



* Read (r) = 4
* Write (w) = 2
* Execute (x) = 1



7 (rwx) : Read(4) + write(2) + Execute(1)

6 (rw-) : Read(4) + Write(2)

4 (r--) : Read(4)



A 3-digit octal number is used to represent the permissions for the user, group and others respectively.



Eg:



* **chmod 755 filename** sets rwx for the user and r-x r-x for group and others.



---



* UGO ensures that users have the appropriate level of access to perform their tasks while preventing unauthorized access or accidental modifications.



---



**Execute permission (x)**



For files:



* Allows us to run the file as a program or a script. Applies to compiled binaries, shell scrips, python programs etc.



For directories:



* Allows to traverse (enter) the directory using commands like 'cd'.
* Allows us to access files within that directory, even if we don't have read permission on the directory itself (if we know the filenames.)
* Without execute permission, our ability to interact with files within it is severely limited.
* 
