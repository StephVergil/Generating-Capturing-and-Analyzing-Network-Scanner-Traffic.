# Generating, Capturing, and Analyzing Network Scanner Traffic

This project focuses on generating network scanner traffic, capturing it using Zeek, and analyzing the data to gain insights into the behavior of network scanners like Nmap. The exercises involve various scanning techniques, live traffic capture, and log analysis. The objectives include configuring Zeek for live traffic capture, generating network scanner traffic using Nmap, analyzing captured data, and understanding the impact of different scanning techniques on the network.

### Tools Used
**Zeek**: For live traffic capture and log generation.  
**Mininet**: For creating a virtual network topology.  
**Nmap**: To simulate different network scanning techniques.  
**TCPDump**: For raw packet capture and file generation.

### Key Steps
1. **Starting a New Instance of Zeek**: Use the `zeekctl` tool to start Zeek:
   `cd $ZEEK_INSTALL/bin && sudo ./zeekctl start`
2. **Launching Mininet**: Open MiniEdit, load the `Topology.mn` file, and run the virtual machines.
3. **Capturing Traffic with Zeek**: Set up `zeek2` for live packet capture:
   `cd Zeek-Labs/TCP-Traffic/ && tcpdump -i zeek2-eth0 -s 0 -w scantraffic.pcap`
4. **Generating Network Scans**: Execute various Nmap scanning techniques:
   - **TCP SYN Scan**: `nmap -sS 10.0.0.2`
   - **TCP Connect Scan**: `nmap -sT 10.0.0.2`
   - **TCP NULL Scan**: `nmap -sN 10.0.0.2`
   - **TCP Xmas Scan**: `nmap -sX 10.0.0.2`
5. **Analyzing Captured Traffic**: Use Zeek to process the `.pcap` file:
   `zeek -C -r scantraffic.pcap`
   Extract insights:
   - **Top Source IPs**: `zeek-cut id.orig_h < conn.log | sort | uniq -c | sort -rn | head -n 10`
   - **Top Destination Ports**: `zeek-cut id.resp_p < conn.log | sort | uniq -c | sort -rn | head -n 10`

### Results
The analysis demonstrated the behavior of various Nmap scanning techniques, such as TCP SYN and Xmas scans, and their impact on network traffic. The top source IPs generating traffic and the top destination ports targeted were identified. Zeek logs provided detailed insights into network activity.

### Project Resources
- **Project Link**: [Generating, Capturing, and Analyzing Network Scanner Traffic](https://github.com/StephVergil/Generating-Capturing-and-Analyzing-Network-Scanner-Traffic./blob/main/vNetLab%2004.docx.pdf)  
- [Zeek Documentation](https://docs.zeek.org/)  
- [Nmap Manual](https://nmap.org/)  
- [TCPDump Guide](https://www.tcpdump.org/)

### Conclusion
This lab highlights the process of generating, capturing, and analyzing network scanner traffic. By leveraging tools like Zeek and Nmap, valuable insights into network behavior and scanning impacts are achieved, aiding in better monitoring and response strategies.

### Disclaimer
This project was conducted in a controlled environment. Unauthorized use of these techniques or tools outside of a lab may violate ethical guidelines and legal regulations.
