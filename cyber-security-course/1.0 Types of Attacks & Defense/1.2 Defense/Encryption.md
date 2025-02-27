https://tryhackme.com/room/cryptographyintro

Caesar Cipher
- Substitution cipher
- Substitutes each letter without changing their order
- Shifting letters by a fixed number of places to the left or the right of the alphabet
- 0 and 26 wouldn't make any change in the English alphabet
- A keyspace of 25, meaning 25 different keys that a user can choose from

Transposition Cipher
- Changes the  order of the letters
- Writing the message down one column at a time, then reading it by rows
- Key in this example would be 42351 and the original message is in the first table, ciphered is in the second:
	![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/d1c99f9bf3e305eb4b50cb8c30be430d.png)

For an encryption algorithm to be considered secure - it should be infeasible to recover the original message. (a hard problem is needed - a problem that cannot be solved in polynomial time)

Consider the mono-alphabet substitution cipher
- Each letter is mapped to a new letter
- Issue is that in English, most there would be common letters - the letter frequency of what is seen - letters such as `a`, `t`, and so on. An alphabet substitution cipher will be able to break it in feasible time.

Some terminology:
- Cryptographic Algorithm, or Cipher
	- The algorithm which defines the encryption and decryption processes
- Key
	- The key which will convert plaintext into ciphertext and vice versa
- Plaintext
	- Original unencrypted message/data
- Ciphertext
	- Encrypted message/data

Symmetric Algorithms
- Use the same key for encryption and decryption
- Communicating parties must agree on a secret key before being able to exchange any messages
- NIST (National Institute of Standard and Technology) published the Data Encryption Standard (DES) in 1977.
	- It used a key size of 56-bits
	- It was broken in 1997
	- In 1998 it was broken within 56 hours.
- NIST then published the Advanced Encryption Standard (AED) in 2001
	- https://csrc.nist.gov/pubs/fips/197/final
	- Key sizes of 129, 192, and 256-bits
	- AES repeats the following four transformations multiple times
		- `SubBytes(State)` 
			- This transformation looks up each byte in a given subsitution table (S-box) and substitutes it with the respective value
			- The `state` is 16-bytes (128-bits) saved in a 4x4 array
		- `ShiftRows(state)`
			- The second row is shifted by one place, the third row is shifted by two places, and the fourth row is shifted by three places
		- `MixColumns(state)`
			- Each column is multiplied by a fixed matrix (4x4 array)
		- `AddRoundKey(state)`
			- A round key is added to the state using the XOR operation
				![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/049bad7deb4e6dd426335d7c3477f10a.png)
	- The total number of transformation rounds depends on the key size.
	- Some more symmetric encryption algorithms (that are deemed secure):
		- AES, AES192, AES256
			- AES with their respective key sizes of 128, 192, 256
		- IDEA
			- International Data Encryption Algorithm
		- 3DES
			- Triple DES
			- Deprecated in 2023 and disallowed in 2024
		- CAST5
			- Also known as CAST-128
			- Could potentially be named after its authors
				- Carlisle Adams and Stafford Tavares
		- BLOWFISH
			- Designed by Bruce Schneier
		- TWOFISH
			- Designed by Bruce Schneier and derived from Blowfish
		- CAMELLIA128, 192, and 256
			- Designed by Mitsubishi Electric and NTT in Japan
			- Name derived from the flower camellia japonica
	- These are all Block Cipher Symmetric Algorithms

Block Cipher
- Converts the input (plaintext) into blocks and encrypts each block
- A block is usually 128-bits
- Referring to the image below (these are from THM btw) - plaintext "TANGO HOTEL MIKE" is to be encrypted - this being a total of 16-characters
	- The first step is to represent these characters in binary, if using ASCII - "T" would be `0x54` in hex. And so on for each of the characters translated into Hex from ASCII
	- Every two hexadecimal digits are 8bits and represent one byte
	- A block of 128 bits is practically 16-bytes and is represented in a 4x4 array
	- The 128-bit block is fed as one unit to the encryption method
		![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/2d69973a4fbf8220e64c3e896841b21d.png)

Stream Ciphers
- This cipher encrypts plaintext byte by byte
- Considering the encryption of "TANGO HOTEL MIKE" again
	- Each character will need to be converted to its binary representation, if using ASCII, as before, "T" will be `0x54` in hexadecimal. 
		![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5f04259cf9bf5b57aed2c476/room-content/6c0edb0faf15df0c6675c6829fddae01.png)
- The CIA Triad can be achieved through encryption 
- There are problems that Symmetric Algorithms face, however. 
	- Scalability (with more users joining the communication circle/group)
		- Each pair of recipients/senders will need their own private key
		- Communication between 100 users would require almost 5000 different keys!
			- (99+98+97+96... and so on)
	- Negotiating the private keys in a secure manner, how is this achieved?
	- If one system gets compromised, new keys will need to be generated and used with other recipients
	- This is where asymmetric encryption plays a part
		- 100 users would only need to share a total of 100 keys to communicate securely

Two Tools for Symmetric Encryption (there are more, of course)
- GNU Privacy Guard
	- https://gnupg.org/
	- Known as GPG or GnuPG
	- Implements OpenPGP (Pretty Good Privacy) standard
	- A file can be encrypted with GPG by the following command for example:
		- `gpg --symmetric --cipher-algo <cipher-to-use> message.txt`
		- CIPHER is the name of the encryption algorithm
			- Supported ciphers can be checked with the `gpg --version` command
		- Encrypted file will be saved as `message.txt.gpg`
	- The default output is in the binary OpenPGP format, however, if you want to create an ASCII armoured output, which can be opened in any text editor, you chould add the option `--armor` to the command
		- `gpg --symmetric --cipher-algo <cipher-to-use> message.txt`
	- The message can be decrypted using the following command:
		- `gpg --output original-message.txt --decrypt message.gpg`
- OpenSSL Project
	- https://www.openssl.org/
	- A file can be encrypted with the following command:
		- `openssl aes-256-cbc -e -in message.txt -out encrypted_message`
	- It can be decrypted using this command:
		- `openssl aes-256-cbc -d -in encrypted_message -out _original_message.txt`
	- To make the encryption more resilient to brute-force attacks, the `-pbkdf2` option can be added to the commands
		- Password-Based Key Derivation Function 2 (PBKDF2)
	- The number of iterations on the password to derive the encryption key can be used as well `-iter <number>`
	- Decryption commands will need to include the PBKDF2 and Iteration cycles if enabled when encrypted

Asymmetric Encryption
- Asymmetric encryption makes it possible to exchange encrypted messages without a secure channel - just a reliable channel is needed
- A key pair is generated - a public key and a private key
	- The public key is shareable with the world (although mainly with the parties that the sending party would be wanting to communicate with)
	- The private key would have to be kept securely - wherein no one can access it
	- There is no method of deriving the private key from the public key
- So say if Alice sends Bob a message using Bob's public key. Only bob can decrypt it as Bob is the only one who has Bob's private key.
	- And vice versa, Bob would then use Alice's public key to send Alice a message and only Alice would be able to decrypt it
- Authenticity, Integrity and Non-repudiation
	- A sender would encrypt the message they are wanting to send with their own private key, which can be decrypted by recipients using the sender's public key
		- This shows that the message did in fact come from the sender and wasn't manipulated in some way or has come from someone else. The sender can also not deny sending the message as it would have been signed off (encrypted) with their private key. 

RSA (Rivest, Shamir, Aldeman)
- Two prime numbers are chosen (p and q)
	- Then calculate: N = p * q
- Two integers are chosen (e and d)
	- e * d = 1 mod xor(N)
	- where xor(N) = N - p - q + 1
	- This step will generate the public key (N,e) and the private key (N,d)
- The sender can encrypt a value 'x' by calculating y = e ^ e mod N
- The recipient can decrypt y by calculating x = y ^ d mod N
- Note `_y__d_ = _x__e__d_ = _x__k__ϕ_(_N_) + 1 = (_x__ϕ_(_N_))_k_ × _x_ = _x_` - why a restriction is put on the choice of e and d
- RSA relies on secure random number generation - as with other asymmetric encryption algorithms
	- Example
		```
		1. Bob chooses two prime numbers: _p_ = 157 and _q_ = 199. He calculates _N_ = 31243.
		2. With _ϕ_(_N_) = _N_ − _p_ − _q_ + 1 = 31243 − 157 − 199 + 1 = 30888, Bob selects _e_ = 163 and _d_ = 379 where _e_ × _d_ = 163 × 379 = 61777 and 61777 mod 30888 = 1. The public key is (31243,163) and the private key is (31243,379).
		3. Let’s say that the value to encrypt is _x_ = 13, then Alice would calculate and send _y_ = _x__e_ mod _N_ = 13163 mod 31243 = 16342.
		4. Bob will decrypt the received value by calculating _x_ = _y__d_ mod _N_ = 16341379 mod 31243 = 13.
		```
- OpenSSL can generate a key pair
	- `openssl genrsa -out private-key.pem 2048`
		- Outputting a private key
	- `openssl rsa -in private-key.pem -pubout -out public-key.pem `
		- Generating a public key based off the inputted private key
	- `openssl rsa -in private-key.pem -text -noout`
		- If you want to see the variables used to create the private key
	- If we have a public key of a recipient of whom we want to communicate, then we can encrypt our message with:
		- `openssl pkeyutl -encrypt -in plaintext.txt -out ciphertext -inkey public-key.pem -pubin`
	- The recipient can decrypt with their private key
		- `openssl pkeyutl -decrypt -in ciphertext -inkey private-key.pem -out decrypted.txt`

Diffie-Hellman Key Exchange
- 