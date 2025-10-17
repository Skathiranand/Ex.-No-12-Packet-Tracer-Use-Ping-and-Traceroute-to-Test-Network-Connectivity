# Ex. No: 12 – Packet Tracer: Use Ping and Traceroute to Test Network Connectivity
# Date: 17-10-2025
# Name: Kathir Anand S
# Reg No: 212223100018
________________________________________<br>
# Objective
To test and restore IPv4 and IPv6 network connectivity using diagnostic commands (ping and tracert), identify faults, and verify proper routing between end devices in a dual-stack (IPv4 + IPv6) topology.<br>
Tasks:<br>
•	Use ipconfig and ipv6config to collect addressing information.<br>
•	Use ping and tracert to test connectivity.<br>
•	Locate and fix connectivity issues.<br>
•	Verify successful restoration of both IPv4 and IPv6 communication.<br>
________________________________________<br>
# Apparatus / Tools Required
• Cisco Packet Tracer<br>
• 3 Routers (R1, R2, R3 – 2911 or equivalent)<br>
• 4 PCs (PC1–PC4)<br>
• Copper straight-through and serial DCE/DTE cables<br>
________________________________________<br>
# Network Topology Diagram
(Insert your Packet Tracer screenshot showing R1 ↔ R2 ↔ R3 with PCs PC1–PC4 connected.)<br>
________________________________________<br>
Addressing Table<br>
|Device	|Interface	 |IPv4 Address / Subnet Mask	  |IPv6 Address / Prefix	|Default Gateway|
|-------|------------|------------------------------|-----------------------|---------------|
|R1	    |G0/0	       |10.10.1.97 / 255.255.255.224	|2001:db8:1:1::1/64	|N/A|
|R1	    |S0/0/1      |10.10.1.6 / 255.255.255.252	  |2001:db8:1:2::2/64	|N/A|
|R2	    |S0/0/0	     |10.10.1.5 / 255.255.255.252	  |2001:db8:1:2::1/64	|N/A|
|R2	    |S0/0/1	     |10.10.1.9 / 255.255.255.252	  |2001:db8:1:3::1/64	|N/A|
|R3    	|G0/0	       |10.10.1.17 / 255.255.255.240	|2001:db8:1:4::1/64 |N/A|
|R3    	|S0/0/1      |10.10.1.10 / 255.255.255.252  |2001:db8:1:3::2/64	|N/A|
|PC1  	|NIC(DHCP/Manual IPv4)|	10.10.1.98 / 255.255.255.252|      N/A      |R1 G0/0|
|PC2	  |NIC(DHCP/Manual IPv6)|	N/A	|2001:DB8:1:1::2|R1 G0/0|
|PC3	  |NIC(DHCP/Manual IPv4)|10.10.1.18 / 255.255.255.252 |      N/A      |R3 G0/0|
|PC4	  |NIC(DHCP/Manual IPv6)| N/A |2001:DB8:1:1::2|R3 G0/0|
________________________________________
# Procedure for Students – Use Ping and Traceroute (13.2.7)
Download the Activity File<br>
Ensure the file 13.2.7-packet-tracer---use-ping-and-traceroute-to-test-network-connectivity.pka is saved in an accessible folder (e.g., Downloads or Documents).<br>
________________________________________
# Open Cisco Packet Tracer
Launch Cisco Packet Tracer → Click File → Open...<br>
Select the .pka file and click Open.<br>
________________________________________<br>
# Start the Activity
The pre-configured topology (R1–R3 and PCs PC1–PC4) will load automatically.<br>
Follow the right-hand Instruction Panel for activity steps.<br>
________________________________________
# Part 1: Test and Restore IPv4 Connectivity<br>
# Step 1: Verify IPv4 Configuration<br>
1.	Click PC1, open Command Prompt, and type:<br>
2.	ipconfig /all<br>
Note IPv4 address, mask, and gateway.<br>
3.	Repeat on PC3 and record data in the Addressing Table.<br>
________________________________________<br>
# Step 2: Test and Locate IPv4 Issues
1.	From PC1, ping PC3:<br>
2.	ping <PC3 IPv4 address><br>
Observe failure (expected).<br>
3.	From PC1, trace the route:<br>
4.	tracert <PC3 IPv4 address><br>
Record the last reachable hop.<br>
5.	Repeat the same from PC3 to PC1.<br>
________________________________________<br>
# Step 3: Analyze and Diagnose
•	On R1, run:<br>
•	show ip interface brief<br>
•	show ip route<br>
Identify incorrect interfaces or missing routes.<br>
•	Repeat on R2 and R3.<br>
Compare configurations with documentation to locate the misconfigured interface or subnet.<br>
________________________________________<br>
# Step 4: Implement Fix
Reconfigure the faulty interface or routing entry. Example:<br>
configure terminal<br>
interface s0/0/1<br>
 ip address 10.10.1.6 255.255.255.252<br>
 no shutdown<br>
end<br>
copy running-config startup-config<br>
________________________________________<br>
# Step 5: Verify IPv4 Restoration
From PC1:<br>
ping <PC3 IPv4 address><br>
From PC3:<br>
ping <PC1 IPv4 address><br>
Both pings should now succeed.<br>
________________________________________
# Part 2: Test and Restore IPv6 Connectivity
# Step 1: Verify IPv6 Configuration
On PC2 and PC4, use:<br>
ipv6config /all<br>
Record IPv6 address, prefix, and gateway.<br>
________________________________________
# Step 2: Test and Trace IPv6 Connectivity
1.	From PC2, ping PC4:<br>
2.	ping 2001:db8:1:4::a<br>
Expected: Failure initially.<br>
3.	Trace route:<br>
4.	tracert 2001:db8:1:4::a<br>
Record last reachable IPv6 address.<br>
________________________________________
# Step 3: Diagnose and Correct IPv6 Faults
•	On routers, use:<br>
•	show ipv6 interface brief<br>
•	show ipv6 route<br>
Verify that interfaces are up and prefixes match documentation.<br>
•	Identify and correct errors (e.g., missing IPv6 address, shutdown interface).<br>
________________________________________
# Step 4: Implement and Verify IPv6 Restoration
1.	Correct any configuration errors using CLI.<br>
2.	Confirm end-to-end IPv6 connectivity with ping and tracert.<br>
________________________________________
# Verification and Testing Summary
Command	Purpose<br>
ipconfig /all	View IPv4 details<br>
ipv6config /all	View IPv6 details<br>
ping	Test reachability<br>
tracert	Trace route hops<br>
show ip interface brief	Verify IPv4 interface status<br>
show ipv6 interface brief	Verify IPv6 interface status<br>
________________________________________
# Output (Attach Screenshots)
• Command outputs (ipconfig, ipv6config, ping, tracert) for PCs.<br>
• Router interface and routing tables.<br>
• Successful ping results after fixes.<br>
________________________________________<br>
# Result
IPv4 and IPv6 connectivity issues were diagnosed and resolved using ping and tracert commands. Routers and PCs achieved full dual-stack communication after correcting configuration errors, confirming network restoration and routing accuracy.<br>
