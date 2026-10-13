# ServiceNow Hardware Asset Management (HAM): EOS/EOL Lifecycle Governance & Data Remediation

## 📌 Project Overview
This project demonstrates end-to-end IT Asset Governance in **ServiceNow** by addressing unmanaged End-of-Life (EOL) and End-of-Support (EOS) hardware risks. 

Using **System Import Sets** and **Transform Maps**, over 75+ laptop and server hardware product models (`cmdb_hardware_product_model`) were audited, normalized, and updated with accurate manufacturer lifecycle dates to establish proactive governance and executive risk visibility.

---

## 🎯 Business Problem & Key Objectives
* **Problem:** Critical computer models in the ServiceNow CMDB/HAM instance lacked EOL/EOS dates, creating compliance, support, and security vulnerabilities across the hardware fleet.
* **Objective:** Establish a repeatable bulk-update pipeline via Transform Maps to enrich Hardware Model records with verified vendor support cutoffs.

---

## 🛠️ Technical Solution & Workflow

### 1. Data Enrichment & Auditing
* Exported unnormalized/missing product models from `cmdb_hardware_product_model`.
* Standardized dates across Dell, HP, Lenovo, Apple, Microsoft, and Gateway hardware lines.

### 2. Transform Map Configuration & Data Mapping
Created a custom Transform Map (`sherry transform map`) mapping staging table attributes to target `cmdb_hardware_product_model` fields:
* `u_model_number` ➔ `model_number` (**Coalesce Key = true**)
* `u_end_of_life` ➔ `u_end_of_life`
* `u_end_of_support` ➔ `u_end_of_support`
* `u_manufacturer` ➔ `manufacturer`
* `u_normalization_status` ➔ `normalized_status`

![Transform Map Mapping](screenshots/01_transform_map_setup.png)

### 3. Data Transformation & Database Indexing
* Indexed `model_number` for optimal query speed during coalesce execution.
* Loaded dataset via System Import Sets and executed the transform script.

---

## ✅ Verified Results

* **100% Data Remediation:** Populated accurate EOL/EOS dates across active laptop/server models in the target instance.
* **Proactive Refresh Readiness:** Enabled automated 12-, 6-, and 3-month lead-time triggers for IT operations and procurement.

![Successful Transform Results](screenshots/03_successful_transform_results.png)

---

## 📁 Repository Contents
* `cmdb_hardware_product_model_updated.xlsx`: Complete dataset with vendor EOL/EOS timelines.
* `Hardware_Asset_Management_EOL.csv`: Import-ready CSV dataset.
* `/screenshots`: Visual evidence of field mapping and transformed ServiceNow records.
