# 🔬 Analysis Methodology

## Project: Cybersecurity Threat Intelligence Dashboard
**Author**: Shanmukha Sree Bendi | Central Michigan University | 2026

---

## 1. Data Collection & Scope

### Dataset Overview
- **Source**: Synthetic network traffic log dataset generated to simulate real enterprise SIEM output
- **Total Records**: 5,247 network events
- **Time Period**: 30-day monitoring window (July 2026)
- **Features Captured**:
  - Timestamp, Source IP, Destination Port, Source Port
  - Protocol (TCP/UDP/ICMP)
  - Bytes Transferred, Session Duration
  - Source Country, Attack Type Label
  - Severity Score (0–5)

---

## 2. Data Preprocessing

### Steps Applied
1. **Timestamp parsing** — Converted raw timestamps to datetime format for hourly and daily aggregation
2. **IP normalization** — Standardized IP address formatting for geographic lookup
3. **Null handling** — Flagged unknown source countries as 'Unknown' category
4. **Feature engineering**:
   - Derived `hour` and `day_of_week` from timestamps for temporal analysis
   - Created binary `is_attack` flag (0 = Normal, 1 = Attack)
   - Mapped severity scores to categorical labels (Safe → Extreme)
5. **Protocol encoding** — Label encoded Protocol field for ML model input

---

## 3. Exploratory Data Analysis (EDA)

### Approach
- **Attack distribution**: Value counts and percentage breakdown by attack type
- **Temporal patterns**: Grouped events by hour and day to identify peak attack windows
- **Geographic analysis**: Aggregated attacks by source country for threat mapping
- **Severity classification**: Distributed events across 6 NIST-aligned severity tiers
- **Bytes analysis**: Box plot analysis of data transferred per attack type to identify anomalies

### Key EDA Findings
| Finding | Detail |
|---------|--------|
| Peak attack hour | 18:00–19:00 UTC (192 events) |
| Most common attack | DoS — 30.2% of attack events |
| Highest data exfiltration | Ransomware — avg 80KB per event |
| Most targeted port | Port 80 (HTTP) — 45% of DoS attacks |
| Lowest precision attack | Port Scan — very low bytes, hard to detect |

---

## 4. Machine Learning — Isolation Forest

### Why Isolation Forest?
Isolation Forest is well-suited for network anomaly detection because:
- Works on **unlabeled or partially labeled data** (realistic in real SOC environments)
- Efficient on **high-dimensional** network log data
- Does not assume a normal distribution
- Fast inference — suitable for near-real-time detection

### Model Configuration
```
Algorithm:     Isolation Forest
Estimators:    500 trees
Contamination: 0.10 (10% expected anomaly rate)
Random State:  42 (reproducibility)
Features:      [bytes_sent, duration_sec, dst_port, src_port, severity, protocol_enc]
```

### Performance Metrics
| Metric | Score |
|--------|-------|
| Precision | 91.3% |
| Recall | 87.6% |
| Anomalies Flagged | ~525 events |
| True Attacks Caught | ~480 events |
| Comparison vs Rules-Based | +34% recall improvement |

---

## 5. Visualization Design

### Dashboard Components
| Visual | Purpose |
|--------|---------|
| Donut chart | Attack type proportion at a glance |
| Hourly bar chart | Identify peak attack windows for staffing decisions |
| 30-day trend line | Track attack volume growth/decline over time |
| Country horizontal bars | Geographic risk prioritization |
| Severity bar chart | Resource allocation by urgency |
| Threat events table | Incident-level detail for SOC analyst review |

### Design Principles Applied
- **Dark theme** — Reduces eye strain for SOC analysts working extended shifts
- **Color coding** — Red (critical) → Orange (high) → Yellow (medium) → Green (safe)
- **Live clock** — Simulates real-time monitoring environment
- **LIVE badge** — Indicates active monitoring status

---

## 6. NIST CSF Alignment

Findings were mapped to NIST Cybersecurity Framework functions:

| NIST Function | Project Application |
|--------------|-------------------|
| **Identify** | Asset and vulnerability mapping via port analysis |
| **Protect** | Firewall and endpoint hardening recommendations |
| **Detect** | Isolation Forest anomaly detection, SIEM log analysis |
| **Respond** | Incident classification by severity and type |
| **Recover** | Prioritization framework for remediation sequencing |

---

## 7. Limitations & Future Work

### Current Limitations
- Dataset is synthetic — real-world logs would include additional noise and edge cases
- Geographic attribution based on IP ranges is approximate
- Model requires periodic retraining as attack patterns evolve

### Proposed Future Enhancements
- Integrate with live Splunk or QRadar SIEM feed via API
- Add threat intelligence enrichment (VirusTotal, AbuseIPDB lookup)
- Implement automated alert escalation workflow in ServiceNow SecOps module
- Extend to include endpoint detection data (EDR integration)

---

*Methodology document | Shanmukha Sree Bendi | CMU MS Information Systems | 2026*
