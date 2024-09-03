This page will be for mucking around and the like:



`c:\Windows\System32\config\`

	- r
		- 4
	- w
		- 2
	- x
		- 1
	- rwx
		- 7
	- rw
		- 6
	- rx
		- 5
	- wx
		- 3

- If you get a "No matching host key found. Their offer: ssh-rsa,ssh-dss" thrown at you when trying to connect via ssh, try something like:
	- `-oHostKeyAlgorithms=+ssh-rsa` in your command
	- Reason-being here is that OpenSSH have deprecated rsa ssh-rsa

- `export PATH=$PATH:/'dir'`