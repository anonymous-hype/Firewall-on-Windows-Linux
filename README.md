# Windows Firewall Configuration

**Objective:** Configure Windows Firewall to block insecure Telnet (port 23) and allow secure SSH (port 22) traffic.

**Tools Used:**
- Windows Defender Firewall with Advanced Security (`wf.msc`)
- Command Prompt (for testing)
- Telnet Client (for validation)

---

## 🛠️ Detailed Steps

### 1. Accessing Windows Firewall
1. Press `Win + R`, type `wf.msc`, and hit **Enter** to open the advanced firewall interface.
2. Verified current inbound/outbound rules under:
   - **Inbound Rules** (for incoming traffic)
   - **Outbound Rules** (for outgoing traffic)

### 2. Blocking Telnet (Port 23)
1. **Created a new inbound rule:**
   - Right-clicked **Inbound Rules** → **New Rule**
   - Selected **Port** → **TCP** → Specific port `23`
   - Chose **Block the connection**
   - Applied to all profiles (Domain, Private, Public)
   - Named rule: `BLOCK_TELNET_INBOUND`

2. **Testing the rule:**
   - Opened Command Prompt as Administrator
   - Ran: `telnet localhost 23`
   - **Expected result:** Connection failure (confirmed rule works)

### 3. Allowing SSH (Port 22)
1. **Created a new allow rule:**
   - Same process as above, but:
     - Port `22` (TCP)
     - Selected **Allow the connection**
   - Named rule: `ALLOW_SSH_INBOUND`

### 4. Verification
- Used `netsh` to export firewall rules for documentation:
  ```cmd
  netsh advfirewall show allprofiles > firewall_rules.txt
