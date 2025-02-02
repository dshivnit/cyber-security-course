https://tryhackme.com/r/room/tsharkthebasics

- Open-source command-line network traffic analzser
- Created by the Wireshark developers and has most of the features of Wireshark
- Commonly used as a command-line version of Wireshark
- Can also be used like tcpdump
- Preferred for comprehensive packet assessments

- Suitable for data carving, in-depth packet analysis, and automation with scripts
- Produced/processed data can be pipelined to additional tools
- Most common tools:
	- `capinfos`
		- Provides details of a specified capture file
		- Suggested to view the summary of the capture file before starting an investigation
	- `grep`
		- Helps search plain-text data
	- `cut`
		- Helps cut parts of lines from a specified data source
	- `uniq`
		- Filters repeated lines/values
	- `nl`
		- Views the number of shown lines
	- `sed`
		- A stream editor
	- `awk`
		- Scripting language that helps pattern search and processing

Command-Line Interface and Parameters
- `-D`
	- List available sniffing interfaces
- `-i`
	- Choose an interface to capture traffic with
- `<no-parameter>`
	- Sniff the traffic like tcpdump
	- tshark will use the first available interface when none is selected
- `-r`
	- Read a capture file
- `-c`
	- Packet count
	- Stop capturing after a specified number of packets
- `-w`
	- Write/output function
	- Write the sniffed traffic to a file
	- You can also save a particular filtered read of a pcap file to another file so that you can cross-reference or pull out the information that you are specifically needing from a .pcap file
		- `tshark -r sample.pcap -c 25 -w sample-first-25p.pcap`
- `-V`
	- Verbose
	- Provide detailed information for each packet
	- Similar to the Packet Details Pane in Wireshark
- `-q`
	- Silent mode
	- Suppress the packet outputs on the terminal
- `-x`
	- Display packet bytes
	- Show packet details in hex and ASCII dump for each packet

Capture Condition Parameters
	Tshark can be configured to count packets and stop at a specific point or run in a loop structure. Most common parameters are below:
- `-a` - Define capture conditions for a single run/loop. STOP after completing the condition - also known as Autostop
	- Duration
		- Sniff the ttraffic and stop after x seconds. Create a new file and output to it
		- `tshark -w sample.pcap -a duration:1`
	- Filesize
		- Define the maximum capture file size. Stop after reaching x file size (KB)
		- `tshark -w sample.cap -a filesize:10`
	- Files
		- Define the maximum number of output files, stop after x files
		- `tshark -w test.pcap -a filesize:10 -a files:3`
- `-b` - Ring buffer control options. Define capture conditions for multiple runs/loops (INFINITE LOOP)
	- Duration
		- Sniff the traffic for x seconds, create a new file and write output to it
		- `tshark -w test.pcap -b duration:1`
	- Filesize
		- Define the maximum capture file size. Create a new file and write output to it after reaching the filesize limit, x, in KB
		- `tshark -w test.pcap -b filesize:10`
	- Files
		- Define the maximum number of output files. Rewrite the first/oldest file after creating x files
		- `tshark -w test.pcap -b filesize:10 -b files:3`
- tshark supports combining AUTOSTOP (`-a`) parameters with RING BUFFER CONTROL (`-b`) parameters. You can combine the parameters according to the use-case and requirements.
- Use the infinite loop carefully, remember to use at least one autostop parameter to stop the infinite loop
	- `tshark -w autostop-sample.pcap -a duration:2 -a filesize:5 -a files:5`

- Capture Filters (live capture)
- https://gitlab.com/wireshark/wireshark/-/wikis/CaptureFilters#useful-filters
- https://www.wireshark.org/docs/man-pages/pcap-filter.html
	- `-f`
		- Capture filters
		- Same as BPF (Berkley Packet Filter) syntax and Wireshark capture filters
		- Type
			- Target match type - you can filter IP addresses, hostnames, IP ranges, and port numbers. Note that if you don't set a qualifer, the "host" qualifier will be used by default
			- Filtering a host
				- `tshark -f "host 10.10.10.10"`
			- Filtering a network range
				- `tshark -f "net 10.10.10.0/24"`
			- Filtering a Port
				- `tshark -f "port 80"`
			- Filtering a Port Range
				- `tshark -f "portrange 80-100"`
		- Direction
			- Target direction/flow
			- Note that if you don't use the direction operator, it will equal to "either" and cover both directions
			- `src | dst`
			- Filtering source address
				- `tshark -f "src host 10.10.10.10"`
			- Filtering destination address
				- `tshark -f "dst host 10.10.10.20"`
			- `tshark -f "dst host 10.10.10.20" -f "src host 10.10.10.10"`
		- Protocol
			- Target protocol
			- `arp | ether | ip | ip6 | tcp | udp`
			- Filtering TCP
				- `tshark -f "tcp"`
			- Filtering MAC address
				- `tshark -f "ether host F8:D8:C5:A2:5D:81`
			- You can also filter protocols with IP protocol assigned by the IANA (Internet Assigned Numbers Authority)
			- Filtering IP Protocols 1 (ICMP)
				- `tshark -f "ip proto 1"
				- https://www.iana.org/assignments/protocol-numbers/protocol-numbers.xhtml`
		- Host Filtering
			- Capturing traffic to or from a host
			- Traffic generation with curl (cURL) - this command sends a default HTTP query to a specified address. 
				- `curl tryhackme.com`
			- TShark capture filter for a host
				- `tshark -f "host tryhackme.com"`
		- IP Filtering
			- Capturing traffic to or from a specific port
			- We will use the Netcat tool to create noise on specific ports
			- Traffic generation with Netcat - here `nc` is instructed to provide details (verbosity), and timeout is set to 5 seconds
				- `nc 10.10.10.10 4444 -vw 5`
			- TShark capture filter for specific IP address
				- `tshark -f "host 10.10.10.10"`
		- Port Filtering
			- Capturing traffic to or from a specific port. We will use netcat to crate noise on specific ports
			- Traffic generation with netcat - here netcat is instructed to provide details (verbosity) and timeout is also set to five seconds
				- `nc 10.10.10.10 4444 -vw 5`
			- TShark capture filter for port 4444
				- `tshark -f "port 4444"`
		- Protocol Filtering
			- Capturing traffic from a specified protocol - also using netcat in this instance
			- `nc` is instructed to use UDP, verbosity and timeout after five seconds
				- `nc -u 10.10.10.10 4444 -vw 5`
			- TShark capture filter for UDP
				- `tshark -f "udp"`
- Display Filters
	- `-Y`
		- Display filters.
		- Same as Wireshark's display filters!!!!!!
			- https://www.wireshark.org/docs/dfref/
			- (note that Wireshark presents a drop down menu with possible commands when using the filter-query bar - which is quite efficient - however the above link provides what you need as well)
		- Use **single quotes** to avoid space and bash expansion problems
		- Protocol: IP
			- Filtering an IP without specifying a destination
				- `tshark -Y 'ip.addr == 10.10.10.10'`
			- Filtering a network range
				- `tshark -Y 'ip.addr == 10.10.10.0/24'`
			- Filtering a source IP
				- `tshark -Y 'ip.src == 10.10.10.10`
			- Filtering a destination IP
				- `tshark -Y ip.dst == 10.10.10.20`
		- Protocol: TCP 
			- Filtering TCP port
				- `tshark -Y 'tcp.port == 80'`
			- Filtering source TCP port
				- `tshark -Y 'tcp.srcport == 80'`
		- Protocol: HTTP
			- Filtering HTTP packets
				- `tshark -Y 'http'`
			- Filtering HTTP packets with response code "200"
				- `tshark -Y 'http.response.code == 200'`
		- Protocol: DNS
			- Filtering DNS packets
				- `tshark -Y 'dns'`
			- Filtering all DNS "A" packets
				- `tshark -Y 'dns.qry.type == 1'`
	- Tip - use `nl` when filtering packets from a .pcap* (if you want)
	- You can save the results of your filter-queries into a txt file for processing
	- Also don't forget about piping `wc -l` which is handy (imo)
	- `Dup` will identify a duplicate packet


- Packet Hierarchy Statistics (`phs` option)
- `-z something,something -q` 
	-- will show you a list of all the options available
	- Once this command is used, the result will start with the PHS header
		- `--color`
			- Wireshark-like
			- `tshark --colour -r capture.pcap`
		- `-z`
			- **Statistics**
			- Multiple options available under this parameter
				- `tshark -z help`
			- Sample usage
				- `tshark -z filter`
			- Each time you filter the statistics, packets are shown first, then the statistics provided. 
			- `-q`
				- You can suppress packets and focus on the statistics by using the -q parameter
- Colourised Output
	- Just like Wireshark
		- `tshark --color -r capture-file.pcap`
- **Statistics | Protocol Hierarchy**
	- General overview
		- `tshark -r cap-file.pcapng -z io,phs -q`
	- Focusing on a particular protocol more - in this instance UDP
		- `tshark -r cap-file.pcapng -z io,phs,udp -q`
- **Statistics | Packet Lengths Tree**
	- Helps to get an overview of the general distribution of packets by size in a tree view
	- Allows analysts to detect anomalously big and small packets at an easy glance
	- `-z plen,tree -q`
		- `tshark -r cap-file.pcapng -z plen,tree -q`
- Statistics | Endpoints
	- Gives an overview of the unique endpoints
	- Shows the number of packets associated with each endpoint
	- `-z endpoints,ip -q`
		- `tshark -r cap-file.pcapng -z endpoints,ip -q`
	- if you type in `endpoints,something` then tshark will show you a report of what entries are allowed (as you would have put in a wrong filter type 'something' -- good way to see the list of possibilities :) ) 
	- endpoints,bluetooth
     endpoints,eth
     endpoints,fc
     endpoints,fddi
     endpoints,ip
     endpoints,ipv6
     endpoints,ipx
     endpoints,jxta
     endpoints,mptcp
     endpoints,ncp
     endpoints,rsvp
     endpoints,sctp
     endpoints,sll
     endpoints,tcp
     endpoints,tr
     endpoints,udp
     endpoints,usb
     endpoints,wlan
     endpoints,wpan
     endpoints,zbee_nwk
- Statistics | Conversations
	- `-z conv,ip -q`
- Specific Filters for Particular Protocols
	- Statistics | IPv4 and IPv6
	- Viewing all hosts on the network
		- `-z ip_hosts,tree -q`
		- `-z ipv6_hosts,tree -q`
	- Handy one - source and destination addresses
		- `-z ip_srcdst,tree -q`
		- `-z ipv6_srcdst,tree -q`
	- Destinations, outgoing traffic
		- `-z dests,tree -q`
		- `-z ipv6_dests,tree -q`
	- DNS
		- `-z dns,tree -q`
	- HTTP
		- `-z http,tree -q`
		- `-z http2,tree -q`
		- `-z http_srv,tree -q`
		- `-z http_req,tree -q`
		- `-z http_seq,tree -q`
- Stream, Objects and Credentials
	- Follow Stream
		- `-z follow`
		- Protocols
			- `tcp`
			- `udp`
			- `http`
			- `http2`
		- View Modes
			- `hex`
			- `ascii`
		- Stream Number
			- `0`
			- `1`
			- `2`
			- `...`
		- Additional Parameter
			- `-q` (quiet the output down)
		- `-z follow,tcp,ascii,0 -q`
			- This is very comprehensive!!
			- `tshark -Y 'ip.addr=63.208.228.223' -r demo.pcapng -z follow,tcp,ascii,0 -q`
				- Gives you all of the returns from the web-server above with the HTML get responses
				- In a sequential stream
		- `-z follow,udp,ascii,0 -q`
		- `-z follow,http,ascii,0 -q`
	- Export Objects
		- Extract files from DICOM, HTTP, IMF, SMB and TFTP
		- `--export-objects http,/path/to/folder -q`
	- Credentials
		- `-z credentials -q`

- Advanced Filtering | Contains, Matches, and Extract Fields
	- Contains
		- Case-sensitive
		- Search a value inside packets
		- Similar to Wireshark's "find" option
	- Matches
		- Case-sensitive
		- Supports regex
		- Search a pattern inside packets
		- Complex queries have a margin of error
	- NOTE: These operators cannot be used with fields consisting of 'integer' values
	- Extract
		- Extract specific parts of data from packets
		- Collect and correlate various fields from the packets
		- Assists in managing the query output on the terminal!
		- Main Filter
			- `-T`
		- Target Field
			- `-e <field-name>`
		- Show Field Name
			- `-E header=y`
		- Example:
			- `tshark -r cap-file.pcapng -T fields -e ip.src -e ip.dst -E header=y -c 5`
				- `-c` list the first five results.
	- Contains
		- Example:
			- `tshark -r capfile.pcap -Y 'http.server contains "Apache"'`
			- lower works here too
			- `tshark -r capfile.pcap -Y 'lower(http.server) contains "apache"'`
	- Matches
		- Example:
			- `tshark -r capture.pcap -Y 'http.request.method matches "(GET|POST)"'`

Example:
- `tshark -r filecap-pcap -Y 'lower(http.request.method) matches "(GET|POST)" -T fields -e ip.src -e ip.dst -E header=y'`
- `thsark -r netcapture.pcap -Y 'frame.number==27'` -V
	- Will list frame 27's details and only 27 from the entire pcap! :) 

- Remember how to extract:
	- hostnames
		- `tshark -r filename.pcap -T fields -e dhcp.option.hostname`
		- `tshark -r filename.pcap -T fields -e dhcp.option.hostname | awk NF | sort -r | uniq -c | sort -r`
			- `awk NF` - removes empty lines.
			- Will give you all hostnames found and the amount of times they were found as well
	- DNS queries
		- `tshark -r capture-file.pcap -T fields -e dns.qry.name | awk NF | sort -r | uniq -c | sort -r`
	- User Agents
		- `tshark -r capture-file.pcap -T fields http.user_agent | awk NF | sort -r | uniq -c | sort -r`
- After viewing statistics and creating an investigation plan
- https://www.wireshark.org/docs/dfref/
- 