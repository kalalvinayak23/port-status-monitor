# Port Status Monitoring using Ryu Controller

## 📌 Problem Statement
This project demonstrates port status monitoring in Software Defined Networking (SDN) using a custom Ryu (os-ken) controller. The controller collects port statistics and detects link up/down events dynamically in a Mininet environment.

---

## ⚙️ Requirements
- Ubuntu / Linux
- Python 3
- Mininet
- Open vSwitch
- Ryu (os-ken)

---

## 📂 Project Structure
```
port-status-monitor/
│── port_status_monitor.py
│── README.md
│── screenshots/
```

---

## 🚀 Steps to Run

### 1. Run Ryu Controller
```bash
osken-manager ./port_status_monitor.py
```

---

### 2. Start Mininet Topology
```bash
sudo mn --topo single,2 --controller=remote,ip=127.0.0.1,port=6653 --switch=ovs,protocols=OpenFlow13
```

---

### 3. Test Connectivity
```bash
pingall
```

---

### 4. Generate Traffic using iPerf
```bash
h2 iperf -s &
h1 iperf -c 10.0.0.2
```

---

### 5. Check Flow Table
```bash
sh ovs-ofctl -O OpenFlow13 dump-flows s1
```

---

### 6. Check Switch Details
```bash
sh ovs-ofctl -O OpenFlow13 show s1
```

---

### 7. Bring Port Down
```bash
sh ip link set s1-eth2 down
```

---

### 8. Test Connectivity (Failure Expected)
```bash
pingall
```

---

### 9. Observe Port Status Change Logs
(Seen in controller terminal automatically)

---

### 10. Bring Port Up
```bash
sh ip link set s1-eth2 up
```

---

### 11. Verify Recovery
```bash
pingall
```

---

## 📸 Screenshots

### Screenshot 1: Ryu Controller Running
<img width="1440" height="900" alt="1" src="https://github.com/user-attachments/assets/0a01c433-8878-44ac-8c23-1839a143b29b" />


### Screenshot 2: Mininet Started
<img width="1440" height="900" alt="2" src="https://github.com/user-attachments/assets/c831483b-c2b0-4803-b4c2-7fcbb601ffda" />

### Screenshot 3: Initial Ping Success
<img width="1440" height="900" alt="3" src="https://github.com/user-attachments/assets/e7be8d08-f5ac-43b4-8d16-cb97d42f2b01" />

### Screenshot 4: iPerf Traffic Test
<img width="1440" height="900" alt="4" src="https://github.com/user-attachments/assets/d03db21e-ba39-421c-a48c-211df8bf412c" />

### Screenshot 5: Flow Table (dump-flows)
<img width="1440" height="900" alt="5" src="https://github.com/user-attachments/assets/12e7168a-b1c6-4c9b-9177-869b5e44374f" />

### Screenshot 6: Switch Details (show s1)
<img width="1440" height="900" alt="6" src="https://github.com/user-attachments/assets/c6143074-4d54-46bd-bd7e-2cb1f3195b9e" />

### Screenshot 7: Port Down Command
<img width="1440" height="900" alt="7" src="https://github.com/user-attachments/assets/d0974685-40ff-4bac-aef8-838afe1d4472" />

### Screenshot 8: Ping Failure After Port Down
<img width="958" height="204" alt="8" src="https://github.com/user-attachments/assets/7a395b87-6793-4ae2-a2f1-a6afc21bce01" />

### Screenshot 9: Port Status Change Logs
<img width="1440" height="900" alt="9" src="https://github.com/user-attachments/assets/f8bffc5d-7e5b-4d92-8d71-f7c395670031" />

### Screenshot 10: Port Up Command
<img width="1440" height="900" alt="10" src="https://github.com/user-attachments/assets/bf8ae9de-2d9a-47e9-bbe6-c006d29d1acf" />

### Screenshot 11: Continuous Port Statistics Monitoring
<img width="1440" height="900" alt="11" src="https://github.com/user-attachments/assets/cd32180e-39fc-4d97-a55c-3ce765daaec4" />

---

## 📊 Observations
- Controller continuously receives port statistics.
- RX and TX packet counters increase during traffic.
- When port is brought down:
  - Link failure is detected.
  - Ping fails.
- When port is brought up:
  - Connectivity is restored.
  - Ping succeeds again.
    
## 📊 Expected Output
- Ping succeeds when all links are active
- Ping fails when port `s1-eth2` is brought down
- Ping succeeds again after the port is restored
- Controller logs show port status changes
- Flow table entries are installed in the switch
- Port statistics are displayed continuously
---

## ✅ Conclusion
This project successfully demonstrates:
- Real-time port monitoring
- Detection of link failures (DOWN state)
- Recovery after link restoration (UP state)
- Continuous traffic statistics collection using SDN controller

---

## 📚 References
1. Mininet Documentation - http://mininet.org/
2. Open vSwitch Documentation - https://docs.openvswitch.org/
3. OS-Ken Documentation - https://docs.openstack.org/os-ken/latest/
4. OpenFlow Specification - https://opennetworking.org/



