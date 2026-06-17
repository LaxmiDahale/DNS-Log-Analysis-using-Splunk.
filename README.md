# 🔍 DNS Log Analysis Using Splunk

<p align="center">
  <img src="https://img.shields.io/badge/SIEM-Splunk-green?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Logs-DNS-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Security-Monitoring-red?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Status-Completed-success?style=for-the-badge" />
</p>

## 📌 Project Overview

This project focuses on analyzing DNS (Domain Name System) logs using Splunk Enterprise to monitor network activity, identify suspicious domain requests, and detect potential security threats. DNS logs were ingested, parsed, and visualized to uncover patterns that may indicate malicious activities such as DNS tunneling, malware beaconing, command-and-control (C2) communications, and failed DNS resolutions.

The project demonstrates how Security Operations Center (SOC) analysts can leverage Splunk's Search Processing Language (SPL) to gain visibility into DNS traffic and strengthen threat detection capabilities.

---

## 🎯 Project Objectives

* Ingest DNS logs into Splunk Enterprise
* Parse and extract critical DNS metadata
* Analyze DNS traffic using SPL queries
* Identify suspicious or abnormal DNS activities
* Detect potential indicators of compromise (IOCs)
* Build a foundation for DNS threat hunting and monitoring

---

## 🛠️ Technologies Used

| Technology                       | Purpose             |
| -------------------------------- | ------------------- |
| Splunk Enterprise                | Log Analysis & SIEM |
| Zeek DNS Logs                    | Data Source         |
| JSON                             | Log Format          |
| SPL (Search Processing Language) | Querying & Analysis |

---

## 📂 Dataset Information

The dataset consists of Zeek-style DNS logs in JSON format containing DNS query and response events.

### Key Fields

| Field       | Description               |
| ----------- | ------------------------- |
| ts          | Timestamp of DNS event    |
| uid         | Unique DNS transaction ID |
| id.orig_h   | Client Source IP          |
| id.orig_p   | Client Source Port        |
| id.resp_h   | DNS Server IP             |
| id.resp_p   | DNS Server Port           |
| qclass_name | DNS Query Class           |
| qtype_name  | DNS Query Type            |
| rcode_name  | DNS Response Status       |
| answers     | DNS Response Records      |
| TTLs        | Time-To-Live Values       |

---

## ⚙️ Lab Setup

### Step 1: Upload DNS Logs

1. Open Splunk Web
2. Navigate to:

```text
Settings → Add Data → Upload
```

3. Upload the DNS log file:

```text
dns_logs.json
```

---

### Step 2: Verify Data Ingestion

```spl
index=dns_lab | head 5
```

---

## 🔍 Detection & Analysis Queries

### 1️⃣ Most Frequently Queried Domains

```spl
index=dns_lab
| stats count by query
| sort -count
```

**Use Case:** Detect suspicious domains, malware beaconing, and C2 communication patterns.

---

### 2️⃣ Most Active Client IP Addresses

```spl
index=dns_lab
| stats count by "id.orig_h"
| sort -count
```

**Use Case:** Identify compromised hosts, infected machines, or misconfigured systems generating excessive DNS traffic.

---

### 3️⃣ DNS Query Type Analysis

```spl
index=dns_lab
| stats count by qtype
```

**Use Cases**

| Query Type | Purpose                   |
| ---------- | ------------------------- |
| A          | IPv4 Resolution           |
| AAAA       | IPv6 Resolution           |
| CNAME      | Alias/Redirect Resolution |
| PTR        | Reverse DNS Lookup        |

---

## 📈 Key Findings

✅ Identified the most frequently queried domains

✅ Discovered high-volume DNS-generating client systems

✅ Analyzed DNS record type distribution

✅ Investigated failed DNS resolutions

✅ Established baseline DNS traffic behavior

✅ Observed response trends and lookup patterns

---

## 🚨 Security Insights

The analysis can help detect:

* DNS Tunneling
* Malware Beaconing
* Command-and-Control (C2) Communications
* Excessive Reverse DNS Lookups
* Failed DNS Resolutions (NXDOMAIN)
* Rare or Newly Observed Domains
* High-Latency DNS Responses

---

## 📊 Suggested Dashboards

### DNS Traffic Overview

* Total DNS Queries
* Top Queried Domains
* Top Source IPs
* Query Volume Over Time

### DNS Threat Monitoring

* NXDOMAIN Trends
* Suspicious Domains
* Rare Domain Queries
* High DNS Traffic Sources

### Query Type Dashboard

* A Records
* AAAA Records
* CNAME Records
* PTR Records

---

## 🚨 Suggested Alerts

### High DNS Query Volume

```spl
index=dns_lab
| stats count by id.orig_h
| where count > 1000
```

### NXDOMAIN Spike Detection

```spl
index=dns_lab rcode_name=NXDOMAIN
| timechart count
```

### Rare Domain Detection

```spl
index=dns_lab
| stats count by query
| where count < 3
```

### Excessive PTR Requests

```spl
index=dns_lab qtype=PTR
| stats count by id.orig_h
| sort -count
```

---

## 🚀 Future Enhancements

* GeoIP Enrichment for DNS Responses
* DNS Tunneling Detection using Entropy Analysis
* Threat Intelligence Feed Integration
* Automated Alerting & Reporting
* Correlation with HTTP, Proxy, and Firewall Logs
* Machine Learning-Based Anomaly Detection
* Risk-Based Alert Prioritization

---

## 🎓 Skills Demonstrated

* Security Information and Event Management (SIEM)
* Splunk Administration
* Log Ingestion & Parsing
* SPL Query Development
* Threat Hunting
* Security Monitoring
* DNS Traffic Analysis
* Cyber Threat Detection
* Incident Investigation

---

## ✅ Conclusion

This project demonstrates practical SOC analyst skills by leveraging Splunk Enterprise for DNS log analysis and threat detection. Through data ingestion, SPL query development, dashboard creation, and security monitoring, the project provides valuable insights into network behavior while helping identify indicators of malicious activity.

---

## 👨‍💻 Author

**Laxmi Dahale**

Cybersecurity Enthusiast | SOC Analyst Aspirant | SIEM & Threat Detection Learner

🔗 LinkedIn: [www.linkedin.com/in/laxmi-nagare-a377aa412](http://www.linkedin.com/in/laxmi-nagare-a377aa412)

⭐ If you found this project useful, consider giving it a star!
