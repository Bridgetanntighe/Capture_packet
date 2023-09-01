<h1>Capturing a packet  </h1>
 - Identify network interfaces<br>
 - Use the <i>tcpdump</i> command to capture network data for inspection<br>
 - Interpret the information that tcpdump outputs regarding a packet <br>
 - Save and load packet data for later analysis<br>

<h2>Task 1. Identify network interfaces</h2>
<img src="https://github.com/Bridgetanntighe/FilterSQLTheory/assets/134883216/599ec85a-ae6b-4c79-b19d-044eb9086e69" height="50%" width="50%" alt="Active Directory Lab"/>

<h2>Task 2. Inspect the network traffic of a network interface with tcpdump</h2>
This command will run <i>tcpdump</i> with the following options:

<i>-i eth0</i>: Capture data specifically from the eth0 interface.<br>
<i>-v</i>: Display detailed packet data.<br>
<i>-c5</i>: Capture 5 packets of data.<br>
<img src="https://github.com/Bridgetanntighe/FilterSQLTheory/assets/134883216/b408219e-0cce-4e2d-a9fb-a9ba9ced3666" height="60%" width="60%" alt="Active Directory Lab"/> <br>
<br>
In the example data at the start of the packet output, tcpdump reported that it was listening on the eth0 interface, and it provided information on the link type and the capture size in bytes:<br>
<img src="https://github.com/Bridgetanntighe/FilterSQLTheory/assets/134883216/c8faeba7-c444-4b31-9b83-7555c1aceded" height="80%" width="80%" alt="Active Directory Lab"/> <br>
<br>
On the next line, the first field is the packet's timestamp, followed by the protocol type, IP:<br>
<img src="https://github.com/Bridgetanntighe/FilterSQLTheory/assets/134883216/b1ad9c5c-9fd1-4496-874a-700e9020546a" height="20%" width="20%" alt="Active Directory Lab"/> <br>
<br>
The verbose option, <i>-v</i>, has provided more details about the IP packet fields, such as TOS, TTL, offset, flags, internal protocol type (in this case, TCP (6)), and the length of the outer IP packet in bytes:<br>
<img src="https://github.com/Bridgetanntighe/FilterSQLTheory/assets/134883216/0c006927-f018-4971-ba9a-55fd48b52fbb" height="80%" width="80%" alt="Active Directory Lab"/> <br>

<h2>Task 3. Capture network traffic with tcpdump</h2>
 Here, I used a filter and other <i>tcpdump</i> configuration options to save a small sample that contains only web (TCP port 80) network packet data.
<img src="https://github.com/Bridgetanntighe/FilterSQLTheory/assets/134883216/f2fc639c-9514-4b91-8b46-cfd28481f723" height="80%" width="80%" alt="Active Directory Lab"/><br>
This command will run <i>tcpdump</i> in the background with the following options:<br>
<i>-i</i> eth0: Capture data from the eth0 interface.<br>
<i>-nn</i>: Do not attempt to resolve IP addresses or ports to names.This is best practice from a security perspective, as the lookup data may not be valid. It also prevents malicious actors from being alerted to an investigation.<br>
<i>-c9</i>: Capture 9 packets of data and then exit.<br>
<i>port 80</i>: Filter only port 80 traffic. This is the default HTTP port.<br>
<i>-w capture.pcap</i>: Save the captured data to the named file.<br>
<i>&</i>: This is an instruction to the Bash shell to run the command in the background.<br>
<br>
Below I will use <i>curl</i> to generate some HTTP(port 80) traffic:
<img src="https://github.com/Bridgetanntighe/FilterSQLTheory/assets/134883216/aa822a5a-910f-4b21-b81f-cc7310b185f3"height="80%"  width="80%" alt="Active Directory Lab"/><br>
When the <i>curl</i> command is used like this to open a website, it generates some HTTP (TCP port 80) traffic that can be captured.<br>
<br>
<img src="https://github.com/Bridgetanntighe/FilterSQLTheory/assets/134883216/ecd16473-a54f-42a4-9934-d15d4d36a2a2"height="80%"  width="80%" alt="Active Directory Lab"/><br>


<h2>Task 4. Filter the captured packet data</h2>
In this task, the tcpdump will filter data from the packet capture file saved previously.<br>
<img src="https://github.com/Bridgetanntighe/FilterSQLTheory/assets/134883216/56c68d74-c620-43ac-a7d5-f0b98add855b" height="80%" width="80%" alt="Active Directory Lab"/><br>
This command will run tcpdump with the following options:<br>
<i>-nn</i>: Disable port and protocol name lookup.<br>
<i>-r</i>: Read capture data from the named file.<br>
<i>-v</i>: Display detailed packet data.<br>
<br>
As in the previous example, you can see the IP packet information along with information about the data that the packet contains.<br>
We will use the tcpdump command to filter the extended packet data from the capture.pcap capture file:<br>
<img src="https://github.com/Bridgetanntighe/FilterSQLTheory/assets/134883216/0eb50687-3842-4a5d-8819-1a292b1b7496%" height="60%" width="60%"alt="Active Directory Lab"/><br>
This command will run <i>tcpdump</i> with the following options:<br>
<i>nn</i>: Disable port and protocol name lookup.<br>
<i>-r</i>: Read capture data from the named file.<br>
<i>-X</i>: Display the hexadecimal and ASCII output format packet data. Security analysts can analyze hexadecimal and ASCII output to detect patterns or anomalies during malware analysis or forensic analysis.<br>
<br>
