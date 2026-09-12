# Legacy Inventory — Pages & Live Site Reachability

## 1. Live Site HTTP Reachability Test Results

* **Target URL:** `https://www.amlakbashi.com/`
* **Resolved IP:** `185.143.234.238`
* **HTTP Test Command:** `curl -I -L -v https://www.amlakbashi.com/`
* **Classification Status:** **`INACCESSIBLE`** (Egress Connection Timeout / Sandbox Egress Policy)

### Verbatim Error Log Output
```
*   Trying 185.143.234.238:443...
* connect to 185.143.234.238 port 443 from 192.168.0.2 port 39358 failed: Connection timed out
* Failed to connect to www.amlakbashi.com port 443 after 269939 ms: Couldn't connect to server
* Closing connection
curl: (28) Failed to connect to www.amlakbashi.com port 443 after 269939 ms: Couldn't connect to server
```

---

## 2. Technical Findings & Reachability Diagnostics

* **DNS Resolution (`[FACT]`):** Domain `www.amlakbashi.com` successfully resolved to IPv4 address `185.143.234.238`.
* **Network Egress (`[FACT]`):** TCP connection attempts to port 443 timed out after 269 seconds. Outbound network traffic from the sandbox container (`192.168.0.2`) to host `185.143.234.238` is blocked by container egress policy or host firewall rules.
* **Live Site Inventory Impact (`[FACT]`):** Live crawling from within this agent sandbox container cannot complete without egress firewall rule adjustment or static HTML archive exports.
