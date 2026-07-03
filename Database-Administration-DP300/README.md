# DP-300: Administering Microsoft Azure SQL Solutions Lab Documentation

## 🏗️ Cloud Data Infrastructure & Security Architecture Overview
This deployment validates core competencies in enterprise database administration, high-availability architecture modeling, role-restricted column compliance masking, and automated business continuity failover scenarios within Microsoft Azure SQL databases.

---

## 🚀 Lab Configuration Stages & Verification

### 1. Enterprise Cloud SQL Compute Models
* **Implementation:** Deployed and optimized Azure SQL database environments using diverse compute architectures tailored to corporate workload patterns.
* **Architectures Evaluated:** Configured rapid auto-scaling **Hyperscale** structures, dynamic **Serverless** engines with auto-pause features, and resource-shared **Elastic Pools** to balance compute availability and minimize database operational costs.

2. Automated Point-in-Time Database Recovery (PITR)
* **Implementation:** Engineered strict data loss prevention boundaries to safeguard databases against accidental corruption or data manipulation events.
* **Recovery Pipelines:** Configured and validated granular, non-destructive database restorations using the Azure Command-Line Interface (Azure CLI) to perform precise **Point-in-Time Restores (PITR)** to isolated test targets.

### 3. Dynamic Data Masking & Governance Compliance
* **Implementation:** Enforced data-at-rest governance standards by implementing advanced column-level security structures.
* **Security Rules:** Built and deployed **Dynamic Data Masking (DDM)** rules to intercept database query results, automatically masking sensitive data streams (such as financial metrics or personal identifiers) based on user database roles and security clearance levels.

### 4. Geo-Replication & Disaster Recovery Topologies
* **Implementation:** Engineered zero-data-loss business continuity frameworks across separate geographic cloud data centers.
* **Failover Validation:** Provisioned and managed **Active Geo-Replication** and automated **Failover Groups**. Validated disaster recovery workflows by executing forced failover simulations under active connections to ensure zero-downtime routing transitions.

---

## 🛠️ Database Engineering & Protection Toolsets Verified
* **Cloud Database Frameworks:** Azure SQL Single Database, Hyperscale Tiers, Serverless Tiers, Elastic Pool Management
* **Data Protection & Compliance:** Dynamic Data Masking (DDM), Role-Based Database Security, Access Restrictions
* **Business Continuity & Recovery:** Active Geo-Replication, Failover Groups, Point-in-Time Restore (PITR), Azure CLI Automation Scripts
