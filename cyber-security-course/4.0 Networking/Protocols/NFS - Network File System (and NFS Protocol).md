- NFS
	- Network File System
	- Allows a system to share directories and files with others over a network
	- By "mounting"
		- Either all, or shared directories/subdirs contents in a File Server (well, the File System on a File Server)
	- Privilege/access dependent
	- Usual process flow:
		- User/Client will request to mount a $share on a File Server (going to call it FS for a little bit because I'm being lazy)
		- FS will then check to see if said Client and/or User has the required permissions to do so and will process accordingly
			- File Handle:
				- The FS will then return what is called a File Handle which itemises and identifies each file and directory that is on the server (in relation to the perms of the Client/User)
		- If an entity wants to access a file using NFS, then a RPC (Remote Procedure Call) call is sent to the NFSD (Network File System Daemon) on the FS - takes parameters such as:
			- File handle
				- Used to represent files and directory
			- Name of the file in question
			- Users UID (User ID)
			- Users Group ID
	- RPC
		- Remote Procedure Call
		- Used to communicate between the Client and the Server
	- Runs between all platforms
		- MacOS
		- Linux
		- Unix
		- and the big "WIN"
		- Works both ways between systems for the most part
	- Tools:
		- nfs-common
			-  Used by both Clients and Servers
			- Client side > can issue a command to choose a location to house the $SHARE to
		- /usr/sbin/showmount -e *ip_address_of_server* 
			- Will enumerate what shares are visible on the File Server 
		- sudo mount -t nfs IP:share /tmp/mount/ -nolock
			for example ^
			- -t 
				- Defines what kind of system we are mounting to, in this case it will be an NFS system
			- IP:share
				- the IP address of the Server were are looking at, along with the name of the share
					- '/tmp/mount'
						- wise to chuck it into tmp if you're not planning on using that share permanently
			- -nolock
				- toggle to use no NLM (Network Lock Manager) lock
			- reads like this in example
			  sudo mount -t nfs 1.2.3.4:sharefolder /tmp/mount/ -nolock
		-  SUID
			- Set User ID
			- 