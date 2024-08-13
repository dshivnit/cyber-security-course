- Plaintext
	- Data before any encryption or hashing
	- Often text, but not always as it could be a photograph, a file, or something else
- Encoding
	- This isn't encryption
	- Just a form of data representation like base64 or hexadecimal
	- Completely reversible
- Hash
	- The output of a hash function
	- To produce the hash value of some data
	- "to hash"
	- You can make a potato into hash browns, but you can't make hash browns back into a potato
- There are no keys when it comes to hashing
- Hashing will take some input data of any size, and create a summary, or a "digest" of that data. The output is a fixed size. It's hard to predict what the output will be for any input and the the same goes vice versa. 
- Good and efficient hashing algorithms will be relatively fast to compute, and slow to reverse.
- The smallest change in the input data should cause a large change in the overall output of what is in the output (the hash)
- The output of a hash function is normally in raw bytes, which are then encoded (common encoding schemes are base64 or hex)

- Used in passwords
	- Online
	- Local on computers
	- and so on

- Hash Collision
	- When two different inputs give the same output
		- yikes
	- Functions are designed to avoid this to the best of their abilities
	- Due to the 'pigeonhole effect' - collisions are not avoidable
		- Pigeonhole Effect
			- "If you put three pigeons in two pigeonholes, at least two of the pigeons end up in the same hole"

- MD5 and SHA1 have been attacked and made technically insecure due to engineering hash collisions
	- Don't use these to hash passwords or data please. :3

- Calculating how many hashes would be in an output:
	- 2^(x) 
	- Where x is the number of bits in the hash
	- 8-bit hash output = 2^8 = 256 possible hashes

- Hashing for Password Verification
	- Most systems will need to verify a User's password
	- The storage of these passwords should never be in plaintext (it's funny though, you'll still find some systems out there that do this... Well not funny but, things can be overlooked by some sometimes and that needs to be fixed.)

- Rainbow Table
	- A lookup table of hashes to plaintexts
	- So one can quickly find out what a password a user had just from the hash (lol)
	- Trades time taken to crack a hash for hard disk space, this is not to say that they do not take time to create though
	- One way to prevent password hashes from ending up in a Rainbow Table that would work, is to SALT them (= 

- Salt
	- Randomly generated and stored in a database and is unique to each user/entry in the system
	- This also prevents the same hash being produced if two Users were to choose the same password to use, as a salt would be added
	- You could, however, still just use the one salt for all passwords if you wanted to..
	- Added either at the start of the password before it's hashed, or the end of the password before it is hashed
	- Hash functions like BCRYPT and SHA512crypt do this automatically 
	- Salts don't need to be kept private

- HMAC
	- Hash-based Message Authentication Code
	- Cryptographic authentication technique that uses a hash function and a secret key
- CTPH
	- Context Triggered Piecewise Hash
- SSDeep
	- Fuzzy hash
	- Type of CTPH
- Streebog
	- Hash function defined in the Russian national standard


---
- Tools:
	- hashid
	- johntheripper
	- hashcat