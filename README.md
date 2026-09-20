# 🛡️ Cybersecurity Threat Intelligence Dashboard

[![Live Dashboard](https://img.shields.io/badge/Live%20Dashboard-View%20Here-00C8FF?style=for-the-badge)](https://shanmukhab626.github.io/cybersecurity-threat-dashboard)
[![CMU](https://img.shields.io/badge/Central%20Michigan%20University-MS%20Information%20Systems-maroon?style=for-the-badge)](https://www.cmich.edu)
[![NIST](https://img.shields.io/badge/Framework-NIST%20CSF-blue?style=for-the-badge)](https://www.nist.gov/cyberframework)

> **Academic Project** · MS Information Systems (Cybersecurity Track) · Central Michigan University · 2026

---

## 📌 Project Overview

This project presents a **network security threat intelligence dashboard** that analyzes 5,247 network log events to detect attack patterns, identify peak threat windows, and classify incidents by severity — aligned with the **NIST Cybersecurity Framework**.

The dashboard simulates a real-world **SOC (Security Operations Center)** analyst workflow, from raw log ingestion to actionable threat recommendations.

🔗 **[View Live Dashboard →](https://shanmukhab626.github.io/cybersecurity-threat-dashboard)**

---

## 📊 Key Findings

| Metric | Result |
|--------|--------|
| Total Events Analyzed | 5,247 |
| Attacks Detected | 2,089 (39.8%) |
| Critical Alerts | 47 |
| Top Attack Type | DoS (30.2% of attacks) |
| Peak Attack Window | 02:00 – 04:00 UTC |
| Top Threat Country | China (524 events) |
| ML Model Precision | 91.3% |
| ML Model Recall | 87.6% |

---

## 🔍 Attack Distribution

| Attack Type | Events | % of Attacks |
|-------------|--------|--------------|
| DoS (Denial of Service) | 630 | 30.2% |
| Port Scan | 525 | 25.1% |
| Brute Force | 420 | 20.1% |
| SQL Injection | 262 | 12.5% |
| MITM | 157 | 7.5% |
| Ransomware | 95 | 4.5% |

---

## 🤖 Machine Learning — Anomaly Detection

An **Isolation Forest** model was implemented for unsupervised anomaly detection:

- **Algorithm**: Isolation Forest (scikit-learn)
- **Features used**: bytes transferred, session duration, destination port, source port, event severity
- **Contamination rate**: 10%
- **Estimators**: 500 trees
- **Precision**: 91.3%
- **Recall**: 87.6%
- **Result**: Outperforms rule-based detection by +34% in recall

---

## 🌍 Geographic Threat Analysis

| Country | Attack Events | Threat Level |
|---------|--------------|--------------|
| 🇨🇳 China | 524 | Critical |
| 🇷🇺 Russia | 393 | Critical |
| 🌐 Unknown | 262 | High |
| 🇮🇷 Iran | 157 | High |
| 🇧🇷 Brazil | 104 | Medium |
| 🇩🇪 Germany | 69 | Low |

---

## 🔐 NIST Framework Recommendations

Based on data analysis findings, the following NIST CSF-aligned controls are recommended:

### 🔴 Critical — Firewall Rule Updates
- Block inbound traffic from top attacking IP ranges
- Implement geo-blocking for high-risk regions
- **Estimated impact**: Reduce DoS exposure by 63%

### 🟠 High — Port 22 (SSH) Hardening
- Enforce key-based authentication only
- Rate-limit login attempts to prevent brute force
- Move SSH to non-standard port

### 🟡 Medium — Peak Hour Monitoring
- Attack volume peaks 02:00–04:00 UTC
- Implement enhanced IDS/IPS alert thresholds during off-hours
- Configure automated incident escalation

---

## 🛠️ Tools & Technologies

| Category | Tools |
|----------|-------|
| Dashboard | HTML5, CSS3, JavaScript, Chart.js |
| Data Analysis | SIEM log analysis, Statistical analysis |
| ML Model | Isolation Forest (anomaly detection) |
| Framework | NIST Cybersecurity Framework |
| Visualization | Chart.js, Custom SOC UI |
| Data | Synthetic network log dataset (5,247 events) |

---

## 📁 Repository Structure

```
cybersecurity-threat-dashboard/
│
├── index.html              # Live interactive dashboard
├── README.md               # Project documentation
├── methodology.md          # Analysis methodology & approach
├── findings-report.md      # Full threat analysis report
└── data/
    └── network_logs_sample.csv   # Sample dataset
```

---

## 👩‍💻 Author

**Shanmukha Sree Bendi**
MS Information Systems | Business Data Analytics & Cybersecurity
Central Michigan University, Mount Pleasant, MI

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=flat&logo=linkedin)](https://linkedin.com/in/shanmukha-sree)
[![Credly](https://img.shields.io/badge/Credly-14%20Badges-FF6B00?style=flat)](https://credly.com/users/shanmukha-sree-bendi)

---

*This project was completed as part of the MS Information Systems Cybersecurity Track at Central Michigan University, 2026.*
