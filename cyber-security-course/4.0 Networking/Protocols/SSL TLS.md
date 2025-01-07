TLS wraps around most protocols these days to ensure data integrity, authenticity and confidentiality
- Consider HTTP (now HTTPS), FTP (now FTPS), IMAP (now IMAPS), SMTP (now SMTPS) and so on

The general process
- Client Hello Message
	- Contains the TLS version and the cypher suite that the client can support, in addition to some random bytes
- Server Hello Message
	- Server highlights its certificate in its response to the client's hello (with its own hello)
	- Highlights the chosen cypher suite (dependent on what the client can support, and the server can as well)
	- Along with some random bytes
- Authentication
	- The client authenticates the servers authenticity through the servers certificate
		- It does this via the Certificate Authority (CA) that issued it
	- These days, web-browsers have known and trusted CAs pre-installed into them with their own certificates - it checks the servers certificate against these CAs
- Premaster Secret
	- The client encrypts some random bytes with the servers public key that was shared earlier (the client gets this pubic key from the certificate that the server had sent it) and sends it to the server
- Decryption of the Premaster Secret
	- The server will then decrypt the premaster with its own private key
- Session Keys Generated
	- Both the client and the server then generate session keys which are based on the random bytes that the client had sent to the server earlier (encrypted with the servers public key), random server bytes, and also the premaster secret
	- Both the client and the server will get to the same result
		- Bear in mind that this session key is never transmitted (it is processed on the client-side, and the server-side - again, never transmitted)
	- Encryption and decryption are thus achieved with this session key
- Ready Messages
	- The client will send a FIN (finished) message using the session key to indicate that the session is ready to initiate
	- A SSL/TLS encrypted connection is achieved

