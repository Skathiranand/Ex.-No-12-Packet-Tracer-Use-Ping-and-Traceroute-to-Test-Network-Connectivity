# Ex. No: 12 – Packet Tracer: Use Ping and Traceroute to Test Network Connectivity
# Date: 17-10-2025
# Name: Kathir Anand S
# RegNo: 212223100018
<br>

# Objective
To test and restore IPv4 and IPv6 network connectivity using diagnostic commands (ping and tracert), identify faults, and verify proper routing between end devices in a dual-stack (IPv4 + IPv6) topology.<br>
Tasks:<br>
•	Use ipconfig and ipv6config to collect addressing information.<br>
•	Use ping and tracert to test connectivity.<br>
•	Locate and fix connectivity issues.<br>
•	Verify successful restoration of both IPv4 and IPv6 communication.<br>
<br>

# Apparatus / Tools Required
• Cisco Packet Tracer<br>
• 3 Routers (R1, R2, R3 – 2911 or equivalent)<br>
• 4 PCs (PC1–PC4)<br>
• Copper straight-through and serial DCE/DTE cables<br>
<br>


<br>

# Addressing Table<br>

|Device	|Interface |	IPv4 Address / Subnet Mask    |	IPv6 Address / Prefix|	Default Gateway|
|-------|----------|--------------------------------|----------------------|-----------------|
|R1	    |G0/0      |	10.10.1.97 / 255.255.255.224  |	2001:db8:1:1::1/64   | N/A |
|R1	    |S0/0/1    |	10.10.1.6 / 255.255.255.252   |	2001:db8:1:2::2/64   | N/A |
|R2     |S0/0/0    |	10.10.1.5 / 255.255.255.252   |	2001:db8:1:2::1/64	 | N/A |
|R2	    |S0/0/1    |	10.10.1.9 / 255.255.255.252   |	2001:db8:1:3::1/64   | N/A |
|R3	    |G0/0      |	10.10.1.17 / 255.255.255.240  |	2001:db8:1:4::1/64   | N/A |
|R3	    |S0/0/1    |	10.10.1.10 / 255.255.255.252  |	2001:db8:1:3::2/64   | N/A |
|PC1    |	NIC	(DHCP/Manual IPv4)|	10.10.1.98 / 255.255.255.252 | N/A |	R1 G0/0 |
|PC2    |	NIC	(DHCP/Manual IPv6)|	N/A | 2001:DB8:1:1::2/64 | R1 G0/0 |
|PC3    |	NIC	(DHCP/Manual IPv4)|	10.10.1.18 / 255.255.255.252 | N/A |	R3 G0/0 |
|PC4    |	NIC	(DHCP/Manual IPv6)|	N/A | 2001:DB8:1:4::2/6 |	R3 G0/0 |

<br>

# Procedure for Students – Use Ping and Traceroute (13.2.7)
Download the Activity File<br>
Ensure the file 13.2.7-packet-tracer---use-ping-and-traceroute-to-test-network-connectivity.pka is saved in an accessible folder (e.g., Downloads or Documents).
<br>

## Open Cisco Packet Tracer
Launch Cisco Packet Tracer → Click File → Open...<br>
Select the .pka file and click Open.
<br>

## Start the Activity
The pre-configured topology (R1–R3 and PCs PC1–PC4) will load automatically.<br>
Follow the right-hand Instruction Panel for activity steps.
<br>

### Part 1: Test and Restore IPv4 Connectivity<br>
### Step 1: Verify IPv4 Configuration<br>
1.	Click PC1, open Command Prompt, and type:<br>
2.	ipconfig /all<br>
Note IPv4 address, mask, and gateway.<br>
3.	Repeat on PC3 and record data in the Addressing Table.<br>

# Step 2: Test and Locate IPv4 Issues
1.	From PC1, ping PC3:<br>
2.	ping <PC3 IPv4 address><br>
Observe failure (expected).<br>
3.	From PC1, trace the route:<br>
4.	tracert <PC3 IPv4 address><br>
Record the last reachable hop.<br>
5.	Repeat the same from PC3 to PC1.<br>

# Step 3: Analyze and Diagnose
•	On R1, run:<br>
•	show ip interface brief<br>
•	show ip route<br>
Identify incorrect interfaces or missing routes.<br>
•	Repeat on R2 and R3.<br>
Compare configurations with documentation to locate the misconfigured interface or subnet.<br>

# Step 4: Implement Fix
Reconfigure the faulty interface or routing entry. Example:<br>
configure terminal<br>
interface s0/0/1<br>
 ip address 10.10.1.6 255.255.255.252<br>
 no shutdown<br>
end<br>
copy running-config startup-config<br>

# Step 5: Verify IPv4 Restoration
From PC1:<br>
ping <PC3 IPv4 address><br>
From PC3:<br>
ping <PC1 IPv4 address><br>
Both pings should now succeed.<br>

# Part 2: Test and Restore IPv6 Connectivity
# Step 1: Verify IPv6 Configuration
On PC2 and PC4, use:<br>
ipv6config /all<br>
Record IPv6 address, prefix, and gateway.<br>

# Step 2: Test and Trace IPv6 Connectivity
1.	From PC2, ping PC4:<br>
2.	ping 2001:db8:1:4::a<br>
Expected: Failure initially.<br>
3.	Trace route:<br>
4.	tracert 2001:db8:1:4::a<br>
Record last reachable IPv6 address.<br>

# Step 3: Diagnose and Correct IPv6 Faults
•	On routers, use:<br>
•	show ipv6 interface brief<br>
•	show ipv6 route<br>
Verify that interfaces are up and prefixes match documentation.<br>
•	Identify and correct errors (e.g., missing IPv6 address, shutdown interface).<br>

# Step 4: Implement and Verify IPv6 Restoration
1.	Correct any configuration errors using CLI.<br>
2.	Confirm end-to-end IPv6 connectivity with ping and tracert.<br>

# Verification and Testing Summary
Command	Purpose<br>
ipconfig /all	View IPv4 details<br>
ipv6config /all	View IPv6 details<br>
ping	Test reachability<br>
tracert	Trace route hops<br>
show ip interface brief	Verify IPv4 interface status<br>
show ipv6 interface brief	Verify IPv6 interface status<br>

# Output

## Ping :
### PC1 to PC3
<img width="582" height="247" alt="Screenshot 2025-11-04 201528" src="https://github.com/user-attachments/assets/c8033e3b-572d-42b2-bb74-5a5707793eed" />

### PC2 to PC4
<img width="606" height="233" alt="Screenshot 2025-11-04 201711" src="https://github.com/user-attachments/assets/84bf070d-620b-4beb-a54d-1a91530f5aa5" />

• Successful ping results after fixes.

## Tracert
### From PC1 to PC3
<img width="525" height="144" alt="Screenshot 2025-11-04 202504" src="https://github.com/user-attachments/assets/93440011-ca76-4a9a-863b-3f63f5a233b3" />

### From PC2 to PC4
<img width="587" height="171" alt="Screenshot 2025-11-04 202910" src="https://github.com/user-attachments/assets/d5d0dcf8-607a-4764-ae99-3e707a47f08e" />

## Ipconfig
### PC1
<img width="668" height="198" alt="Screenshot 2025-11-04 203013" src="https://github.com/user-attachments/assets/beb6fb32-b96b-41f3-8d86-6c65af8f88e3" />

### PC2
<img width="727" height="181" alt="Screenshot 2025-11-04 203139" src="https://github.com/user-attachments/assets/838be531-d0ef-4922-81a1-1ebc72add6f6" />

### PC3
<img width="572" height="210" alt="Screenshot 2025-11-04 204621" src="https://github.com/user-attachments/assets/0054ba40-83b0-4595-a0ba-307765623147" />

### PC4
<img width="679" height="190" alt="Screenshot 2025-11-04 204644" src="https://github.com/user-attachments/assets/abc18532-172f-4e77-a531-a82037e8cc59" />

## Router Inerface Brief
### Router1 
#### IPv4 Interface
<img width="758" height="150" alt="Screenshot 2025-11-04 205026" src="https://github.com/user-attachments/assets/5d27b4ff-68dc-4328-9b2c-8f6e21b55d52" />

#### IPv6 Interface
<img width="608" height="207" alt="Screenshot 2025-11-04 205046" src="https://github.com/user-attachments/assets/e16431ad-be8c-4441-a6ce-1492d6584ccf" />

### Router2
#### IPv4 Interface
<img width="718" height="153" alt="Screenshot 2025-11-04 210523" src="https://github.com/user-attachments/assets/7c73662d-2c8b-4da2-8380-030870f94cdc" />

#### IPv6 Interface
<img width="639" height="206" alt="Screenshot 2025-11-04 210543" src="https://github.com/user-attachments/assets/957afd33-d93a-4e0b-a01f-333c95864adb" />

### Router3
#### IPv4 Interface
<img width="736" height="112" alt="Screenshot 2025-11-04 211235" src="https://github.com/user-attachments/assets/4853587f-64bf-4e07-ac83-09420c960ecf" />

#### IPv6 Interface
<img width="624" height="203" alt="Screenshot 2025-11-04 211309" src="https://github.com/user-attachments/assets/edbd4aa1-e881-4e13-8015-08b9ff30760a" />


## Routing Table
### Router1
#### IPv4
<img width="761" height="297" alt="Screenshot 2025-11-04 211631" src="https://github.com/user-attachments/assets/4b204445-be73-4721-8af4-7476684139dd" />

#### IPv6
<img width="717" height="371" alt="Screenshot 2025-11-04 211652" src="https://github.com/user-attachments/assets/595ed307-6cbe-477a-a52d-2535951c3959" />

### Router2
#### IPv4
<img width="693" height="294" alt="Screenshot 2025-11-04 211848" src="https://github.com/user-attachments/assets/88ceb10a-7fde-4d03-bfb6-68703ea9264e" />

#### IPv6
<img width="735" height="365" alt="Screenshot 2025-11-04 211917" src="https://github.com/user-attachments/assets/a8dc26c6-168e-47a0-9fbb-844aa1054a9c" />

### Router3
#### IPv4
<img width="709" height="292" alt="Screenshot 2025-11-04 212106" src="https://github.com/user-attachments/assets/7820c56d-cd8e-4cf9-8b03-b5be74cdde6d" />

#### IPv6
<img width="783" height="365" alt="Screenshot 2025-11-04 212131" src="https://github.com/user-attachments/assets/5ca7e121-c708-410b-8831-76e23283eee7" />


<br>

# Result
IPv4 and IPv6 connectivity issues were diagnosed and resolved using ping and tracert commands. Routers and PCs achieved full dual-stack communication after correcting configuration errors, confirming network restoration and routing accuracy.<br>
