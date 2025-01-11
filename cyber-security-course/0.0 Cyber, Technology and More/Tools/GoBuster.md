https://github.com/OJ/gobuster
- Enumerates:
	- web directories
	- sub-domains
	- vhosts
	- Amazon s3 buckets
	- Google Cloud Storage
	via the use of brute force
- Uses specific wordlists and handles incoming responses
- Reconnaissance and scanning phases
- Modes:
	- dir
		- directories and files
		- `gobuster dir --help`
			- **THIS IS REAL IMPORTANT as it will give you additional flags from the usual `-h` list of flags**
	- dns
		- subdomains with wildcard support
	- vhost
		- Virtual hosts on web-servers
	- s3
		- Open Amazon S3 Buckets
	- gcs
		- Open Google Cloud Storage
	- fuzz
		- Basic fuzzing
	- tftp
		- TFTP files

- Example of `dir` usage:
	```bash
	gobuster dir -u "http://www.example.thm/" -w /usr/share/wordlists/dirb/small.txt -t 64
	```
	- I won't describe each bit here, research and further self-learning is good :) 
	```shell
	gobuster dir -u http://10.10.10.10 -w /usr/share/wordlists/seclists/Discovery/Web-Content/directory-list-2.3-medium.txt -x .txt,.php,.html,.js,.cfg -t 64 -r --no-errors
	```

https://linuxcommandlibrary.com/man/gobuster

- Domain Sub-domains
	- Just because something is patched in the regular domain doesn't necessarily mean that it is also patched in one of its sub-domains..
	- There could be a potential vulnerability sitting in one of them (sub-domains being them)
	- `gobuster dns --help`
- Example of `dns` usage:
	- `gobuster dns -d something.com -w <path-to-wordlist>`

- Example of `vhost` usage:
	- Gobuster can brute force virtual hosts that are running on a web-server
	- Sometimes they can look like subdomains, don't be fooled!
	- They are IP-based and running on the same server
	- Sub-domains are set up in DNS
	- The difference between `vhost` and `dns` mode is the way how Gobuster will scan:
		- `vhost` - navigate to the URL created by combining the configured HOSTNAME (`-u` flag) with an entry of a wordlist
		- `dns` - will do a DNS lookup to the FQDN created by combining the configured domain name (`-d` flag) with an entry in a given wordlist
	- `gobuster vhost --help`
	- `-u`
		- Specifies the base URL for enumerating possible virtual hosts
	- `-m`
		- Specifies which HTTP method to use
	- Example:
		```shell
		go buster vhost -u "http://10.10.10.10" --domain whatever.com -w <path-to-wordlist-file>
		```
		```shell
		gobuster vhost -u "http://10.10.10.10" --domain whatever.com -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt --append.domain --exclude-length 250-320
		```