- Allows threat actors to access files and directories outside a web application's intended directory structure. 
- Leading to unauth'd access to sensitive data
- Traversal sequence characters such as:
	- `../../../`
		- NOTE - these can be URL encoded 
			- `%2E` - symbolising the `.` character
			- `%2F` - symbolising the `/` character
		- URL encoded input can sometimes bypass firewalls and other monitoring tools
	- `/etc/passwd`
	- `/etc/shadow` 