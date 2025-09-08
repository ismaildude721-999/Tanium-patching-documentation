# Tanium-patching-documentation

# 📑 Documentation: Patching Workstations(user-desktops) with Tanium

## 1. Introduction

This document summarizes the remediation and patching activities performed on **Desktops/workstations** using **Tanium**. The goal was to address vulnerabilities flagged in a Qualys/Tanium report and ensure the systems were updated to the latest secure versions.

---

## 2. Workstations in Scope

* **Target Group**:  LSDWS desktops (e.g., `lsdws055`, `lsdws060`, `lsdws081`, `lsdws091`, etc.).
* **Selection Criteria**: Machines flagged for vulnerabilities in the Excel vulnerability report.

---
## 3.Patching individual workstation/desktop

## 3.1 
<img width="1410" height="672" alt="image" src="https://github.com/user-attachments/assets/4faa8702-8ea6-44b3-9c11-c404e2e0e560" />


## 3. Patches Applied

### 3.1 Windows Cumulative Updates & Registry Fix

* **Action**: Deployed Windows CU patches and applied the **WinVerifyTrust registry key fix**.
* **Command Example**:

  ```powershell
  reg add HKLM\Software\Microsoft\Cryptography\WinVerifyTrust /v EnableCertPaddingCheck /t REG_DWORD /d 1 /f
  ```
* **Result**: All workstations reported *Complete* or *Not Applicable*.

---

### 3.2 Browser Updates

* **Firefox**: Updated to 142.0.1 using silent installer (`Firefox Setup.exe -ms`).
* **Chrome**: Updated to the latest stable release.
* **Result**: All workstations successfully patched.

---

### 3.3 Visual Studio

* **Action**: Patched Visual Studio to **2022 CU15**.
* **Result**: Successfully patched except `lsdws147` (not applicable).

---

### 3.4 NVIDIA GPU Display Drivers

* **Action**: Verified GPU driver versions.
* **Findings**:

  * 8 workstations had **475.14** (compliant).
  * `lsdws081` had **452.56** (requires update).
  * `lsdws091` → no NVIDIA GPU drivers installed.
* **Next Step**: Create Tanium package to deploy `NVIDIA_Display_Driver.exe -s -noreboot` for `lsdws081`.

---

### 3.5 Azure Data Studio

* **Action**: Created Tanium package for **Azure Data Studio 1.52.0 (System Installer)**.
* **Command**:

  ```cmd
  cmd.exe /c azuredatastudio-windows-system-installer-x64-1.52.0.exe /VERYSILENT /NORESTART /ALLUSERS
  ```
* **Issue**: Old **system version 1.37.0** still detected on some workstations (likely due to side-by-side installs).
* **Resolution Plan**:

  * Re-deploy package with `/ALLUSERS`.
  * If unresolved, uninstall 1.37.0 before deploying 1.52.0.

---

## 4. Verification

* **Tanium Reporting → Installed Applications** was used to confirm versions.
* **Deployments → Summary by Endpoint** verified completion status.
* Endpoints marked *Not Applicable* indicated already compliant or no software present.

---

## 5. Remaining Tasks

* **NVIDIA GPU Driver**: Patch `lsdws081` from 452.56 → 475.14.
* **Azure Data Studio**: Remove/overwrite 1.37.0 with 1.52.0 on flagged workstations.
* **Verification Command in Tanium**:

  ```tanium
  Get Computer Name and Installed Application[Azure Data Studio] and Application Version from all machines
  ```

---

## 6. Conclusion

* Completed patches: **Windows CU, WinVerifyTrust, Firefox, Chrome, Visual Studio, Birthday Attack, GPU drivers (8 workstations)**.
* Outstanding patches: **Azure Data Studio (system 1.37.0) and GPU driver update for lsdws081**.
* Next action: Deploy updated packages to finalize compliance across all 11 workstations.
