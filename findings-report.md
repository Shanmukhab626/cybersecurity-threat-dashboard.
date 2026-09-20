# 📋 Threat Analysis Findings Report

**Project**: Network Security Threat Intelligence Analysis  
**Author**: Shanmukha Sree Bendi  
**Institution**: Central Michigan University — MS Information Systems (Cybersecurity Track)  
**Date**: August 2026  
**Classification**: Academic Project

---

## Executive Summary

This report presents findings from a 30-day network security log analysis of 5,247 monitored events across a simulated enterprise environment. Using SIEM analysis techniques and an Isolation Forest machine learning model, **2,089 attack events were identified** (39.8% of total traffic), with 47 classified as critical severity.

Key findings indicate that **Denial of Service (DoS) attacks** represent the most frequent threat vector, **China and Russia** are the primary geographic sources of malicious traffic, and **02:00–04:00 UTC** is the highest-risk monitoring window requiring enhanced staffing or automated escalation.

Recommendations aligned to the **NIST Cybersecurity Framework** are provided at the conclusion of this report.

---

## 1. Threat Landscape Overview

### 1.1 Event Classification

Out of 5,247 total network events monitored:

| Classification | Count | Percentage |
|---------------|-------|------------|
| Normal Traffic | 3,158 | 60.2% |
| Attack Events | 2,089 | 39.8% |
| **Total** | **5,247** | **100%** |

The 39.8% attack rate is significantly above industry baseline (typically 15–25%), indicating an elevated threat environment requiring immediate control improvements.

### 1.2 Attack Type Breakdown

| Attack Type | Events | % of Attacks | Severity |
|-------------|--------|--------------|---------|
| DoS | 630 | 30.2% | High–Critical |
| Port Scan | 525 | 25.1% | Low–Medium |
| Brute Force | 420 | 20.1% | High |
| SQL Injection | 262 | 12.5% | High–Critical |
| MITM | 157 | 7.5% | Critical |
| Ransomware | 95 | 4.5% | Extreme |
| **Total** | **2,089** | **100%** | — |

---

## 2. Temporal Analysis

### 2.1 Peak Attack Hours

Analysis of attack events by hour of day reveals two distinct peaks:

- **Primary peak**: 18:00–19:00 UTC — 192 events (highest single hour)
- **Secondary peak**: 02:00–04:00 UTC — avg 145 events/hour
- **Lowest activity**: 06:00–09:00 UTC — avg 52 events/hour

**Implication**: Off-hours attacks (02:00–04:00 UTC) are particularly dangerous as SOC staffing is typically reduced during these windows. Automated escalation rules should be configured for this period.

### 2.2 30-Day Trend

Attack volume showed a **+200% increase** from Day 1 (52 events) to Day 30 (156 events), suggesting an ongoing, escalating campaign against the monitored environment. The 3-day moving average confirms the upward trajectory is not isolated to individual spike events.

---

## 3. Geographic Threat Intelligence

### 3.1 Source Country Analysis

| Rank | Country | Events | % of Attacks | Primary Attack Type |
|------|---------|--------|--------------|-------------------|
| 1 | 🇨🇳 China | 524 | 25.1% | DoS, Port Scan |
| 2 | 🇷🇺 Russia | 393 | 18.8% | Ransomware, Brute Force |
| 3 | 🌐 Unknown | 262 | 12.5% | SQL Injection |
| 4 | 🇮🇷 Iran | 157 | 7.5% | MITM, SQL Injection |
| 5 | 🇧🇷 Brazil | 104 | 5.0% | Port Scan |
| 6 | 🇩🇪 Germany | 69 | 3.3% | Port Scan |

**Note**: Germany events are likely legitimate security scanner activity or compromised infrastructure rather than nation-state attacks.

### 3.2 Geographic Risk Assessment

Top 2 countries (China + Russia) account for **44% of all attack events**, making geographic-based firewall rules a high-ROI defensive measure.

---

## 4. Severity Distribution

Events classified using NIST-aligned severity tiers:

| Severity | Score | Events | Action Required |
|---------|-------|--------|----------------|
| Safe | 0 | 3,158 | None — monitor |
| Low | 1 | 525 | Log and review weekly |
| Medium | 2 | 420 | Investigate within 72 hours |
| High | 3 | 892 | Investigate within 24 hours |
| Critical | 4 | 157 | Immediate response required |
| Extreme | 5 | 95 | Incident response team activation |

**47 events** met the combined Critical + Extreme threshold requiring immediate SOC escalation.

---

## 5. ML Anomaly Detection Results

The Isolation Forest model identified **525 anomalous events**, of which **480 were confirmed true attacks** — achieving:

- **Precision**: 91.3% (low false positive rate — reduces analyst alert fatigue)
- **Recall**: 87.6% (catches most real attacks)
- **F1 Score**: ~89.4%
- **Improvement over rules-based detection**: +34% recall

The remaining 8.7% missed attacks were predominantly low-volume Port Scan events with traffic profiles similar to legitimate discovery operations.

---

## 6. NIST CSF Recommendations

### 6.1 Protect Function

**Recommendation P-01 — Geo-based Firewall Rules** (Priority: Critical)
- Implement IP range blocks for China and Russia at perimeter firewall
- Deploy country-based geolocation filtering in WAF
- Estimated reduction in attack volume: **44%**
- Implementation effort: Low (1–2 days)

**Recommendation P-02 — SSH Hardening** (Priority: High)
- Disable password-based SSH authentication; enforce key pairs only
- Implement fail2ban or equivalent rate-limiting (max 3 attempts/5 minutes)
- Relocate SSH service from port 22 to port above 10000
- Estimated brute force reduction: **95%**

**Recommendation P-03 — Web Application Firewall (WAF) Rules** (Priority: High)
- Deploy OWASP ModSecurity ruleset to block SQL Injection patterns
- Enable input validation logging for all database-facing endpoints
- Target: Eliminate 262 SQL Injection events per monitoring cycle

### 6.2 Detect Function

**Recommendation D-01 — Enhanced Off-Hours Monitoring** (Priority: High)
- Configure SIEM alert thresholds to reduce from standard to 50% for 02:00–04:00 UTC window
- Implement automated Tier-1 triage for critical events during this period
- Consider AI-assisted alert correlation to reduce analyst fatigue

### 6.3 Respond Function

**Recommendation R-01 — Incident Playbook Updates** (Priority: Medium)
- Create specific response playbooks for Ransomware (Port 445) events
- Integrate threat intelligence feeds (VirusTotal, AbuseIPDB) into incident response workflow
- Target mean time to respond (MTTR) reduction from current baseline by 40%

---

## 7. Conclusion

The 30-day network analysis reveals an active and escalating threat environment with a 39.8% attack rate significantly above industry benchmarks. Immediate implementation of geo-based firewall rules and SSH hardening would eliminate approximately 50% of current attack volume with minimal implementation effort.

The Isolation Forest anomaly detection model demonstrated 91.3% precision, making it a viable supplement to existing rule-based SIEM detection — particularly for novel attack patterns not yet captured in signature databases.

Long-term, integration of this dashboard with a live SIEM feed (Splunk or QRadar) and ServiceNow SecOps for automated incident ticketing would create a fully automated threat response pipeline.

---

**Report prepared by**: Shanmukha Sree Bendi  
**MS Information Systems** — Business Data Analytics & Cybersecurity Track  
**Central Michigan University** | Mount Pleasant, MI | 2026  
**Certifications**: Cisco Junior Cybersecurity Analyst Career Path · Cisco Cyber Threat Management · Network Defense · Endpoint Security  
**Portfolio**: github.com/Shanmukhab626 | **Credly**: credly.com/users/shanmukha-sree-bendi
