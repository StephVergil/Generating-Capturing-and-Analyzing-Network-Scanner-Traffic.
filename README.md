# Generating, Capturing, and Analyzing Network Scanner Traffic

This project explores the use of network scanner traffic generation tools like Nmap, TCPDump, and Mininet, combined with the network analysis capabilities of Zeek. By capturing and analyzing traffic, the lab provides insights into scanning behaviors and their impact on networks. The exercises include various scanning techniques, live traffic capture, and in-depth log analysis.

---

## Objectives
- Generate network scanner traffic using Nmap with various scanning techniques.
- Capture live traffic using TCPDump and process it with Zeek for detailed analysis.
- Identify and analyze the effects of different scanning methods on network behavior.
- Extract actionable insights from logs to better understand scanner patterns.

---

## Tools Used
- **Zeek**: For live traffic capture, processing, and log generation.
- **Nmap**: To simulate network scanning techniques and generate traffic.
- **Mininet**: For creating a virtual network topology.
- **TCPDump**: For raw packet capture and file generation.

---

## Key Steps

### **1. Setting Up the Environment**
- **Starting Zeek**: Begin traffic monitoring with:
  ```bash
  cd $ZEEK_INSTALL/bin && sudo ./zeekctl start
  ```
- **Launching Mininet**: Load and run the virtual network topology:
  ```bash
  sudo mn --custom Topology.mn --topo mytopo --mac --switch ovsk --controller remote
  ```

### **2. Capturing Traffic**
- Use TCPDump on the Zeek instance to capture live traffic:
  ```bash
  tcpdump -i zeek2-eth0 -s 0 -w scantraffic.pcap
  ```
- Save the captured traffic in `.pcap` format for later analysis.

### **3. Generating Network Scans**
- Execute various Nmap scanning techniques on the target network:
  - **TCP SYN Scan**:
    ```bash
    nmap -sS 10.0.0.2
    ```
  - **TCP Connect Scan**:
    ```bash
    nmap -sT 10.0.0.2
    ```
  - **TCP NULL Scan**:
    ```bash
    nmap -sN 10.0.0.2
    ```
  - **TCP Xmas Scan**:
    ```bash
    nmap -sX 10.0.0.2
    ```

### **4. Analyzing Captured Traffic with Zeek**
- Process the captured `.pcap` file with Zeek:
  ```bash
  zeek -C -r scantraffic.pcap
  ```
- Extract insights from the logs:
  - **Top Source IPs**:
    ```bash
    zeek-cut id.orig_h < conn.log | sort | uniq -c | sort -rn | head -n 10
    ```
  - **Top Destination Ports**:
    ```bash
    zeek-cut id.resp_p < conn.log | sort | uniq -c | sort -rn | head -n 10
    ```
- Review logs such as `conn.log` to identify scanner behavior and patterns.

### **5. Cleanup and Shutdown**
- Remove temporary log files:
  ```bash
  ./../Lab-Scripts/lab_clean.sh
  ```
- Stop Zeek services:
  ```bash
  cd $ZEEK_INSTALL/bin && sudo ./zeekctl stop
  ```

---

## Results
The analysis highlighted the distinct behavior of various Nmap scanning techniques and their impact on network traffic. Key findings included:
- Identification of top source IPs generating scan traffic.
- Discovery of commonly targeted destination ports.
- Comprehensive logs detailing connection attempts, packet types, and protocol usage.

The logs provided actionable insights into network scanner activity, aiding in monitoring and defense strategies.

---

## Project Resources
- **Project Link**: [Generating, Capturing, and Analyzing Network Scanner Traffic](https://github.com/StephVergil/Generating-Capturing-and-Analyzing-Network-Scanner-Traffic./blob/main/vNetLab%2004.docx.pdf)
- [Zeek Documentation](https://docs.zeek.org/)
- [Nmap Manual](https://nmap.org/)
- [TCPDump Guide](https://www.tcpdump.org/)

---

## Conclusion
This lab underscores the value of leveraging tools like Nmap, Zeek, and TCPDump to generate, capture, and analyze network scanner traffic. By examining scanner behaviors and their effects on networks, security professionals can develop robust monitoring and response mechanisms, enhancing overall network security.

---

## Disclaimer
This project was conducted in a controlled environment. Unauthorized use of these tools or techniques outside such an environment may violate ethical guidelines and legal regulations.
