- Listens on TCP Port 143 by default
- Alternative to POP3 
- Allows the ability to have emails/states-of-the-mailbox synchronised across multiple devices

Basic Commands
- `LOGIN <username> <password>`
	- Authenticates the User
- `SELECT <mailbox>`
	- Selects the mailbox to work with
- `FETCH <mail_number> <data_item_name>`
	- ie `fetch 3 body[]`
	- Fetches message(email) number 3, and its header and body
- `MOVE <sequence_set> <mailbox>`
	- Moves the specified email/message to another mailbox
- `COPY <sequence_set> <data_item_name>`
	- Copies the indicated email/message to another mailbox
- `LOGOUT`

