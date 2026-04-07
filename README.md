# SDN Port Status Monitoring Tool

## 📌 Problem Statement
In Software Defined Networking (SDN), monitoring the status of switch ports is critical for ensuring network reliability and performance. Link failures or port issues can disrupt communication between hosts.

This project implements a Port Status Monitoring Tool using the OS-Ken controller to:
- Monitor switch port status in real time
- Detect link failures (port DOWN)
- Detect link recovery (port UP)
- Display port statistics (packets, bytes, errors)
- Maintain connectivity awareness in the network

## 🛠️ Technologies Used
- Python 3
- OS-Ken SDN Controller
- Mininet
- Open vSwitch (OVS)
- OpenFlow 1.3

## ⚙️ Setup Instructions

### 1. Install Dependencies
```bash
sudo apt update
sudo apt install mininet openvswitch-switch python3-pip -y
pip3 install os-ken
```

### 2. Clone Repository
```bash
git clone https://github.com/kalalvinayak23/CN-Orange-problem.git
cd CN-Orange-problem
```

### 3. Run Controller
```bash
osken-manager port_status_monitor.py
```

### 4. Start Mininet Topology
```bash
sudo mn --topo single,2 --controller=remote,ip=127.0.0.1,port=6653 --switch=ovs,protocols=OpenFlow13
```

## 🚀 Execution Steps

### Test Connectivity
```bash
pingall
```

### Check Flow Table
```bash
sudo ovs-ofctl -O OpenFlow13 dump-flows s1
```

### Run Traffic Test
```bash
h2 iperf -s &
h1 iperf -c 10.0.0.2
```

### Simulate Port Failure
```bash
sh ip link set s1-eth2 down
pingall
```

### Restore Port
```bash
sh ip link set s1-eth2 up
pingall
```

## 📊 Expected Output

- Switch connects to controller
- Port statistics are displayed
- Flow rules are installed
- Ping works normally
- Ping fails when port is down
- Ping recovers when port is up

## 📸 Proof of Execution

Include screenshots of:
- Controller logs
- Flow table output
- Ping success (0% loss)
- Ping failure (100% loss)
- Ping recovery
- iperf results

## 📂 Project Structure
```
CN-Orange-problem/
│── port_status_monitor.py
│── README.md
│── .gitignore
```


## ✅ Conclusion
This project successfully demonstrates real-time SDN port monitoring, link failure detection, and recovery using OS-Ken and Mininet.
