# Tanium-patching-documentation

# 📑 Documentation: Patching Workstations(user-desktops) with Tanium

## 1. Introduction

This document summarizes the remediation and patching activities performed on **Desktops/workstations** using **Tanium**. The goal was to address vulnerabilities flagged in a Qualys/Tanium report and ensure the systems were updated to the latest secure versions.

---

## 2. Workstations in Scope

* **Target Group**:  LSDWS desktops (e.g., `lsdws055`, `lsdws060`, `lsdws081`, `lsdws091`, etc.).
* **Selection Criteria**: Machines flagged for vulnerabilities in the Excel vulnerability report.

---
## 3.Patching individual workstation/desktop EX: fixing birthday attack

## 3.1 patching desktop (lsdws060.firstagain.local)  ###firstagain.local = domain name on the org

<img width="1410" height="672" alt="image" src="https://github.com/user-attachments/assets/4faa8702-8ea6-44b3-9c11-c404e2e0e560" />


<img width="1414" height="674" alt="image" src="https://github.com/user-attachments/assets/6094d461-6baa-42a7-a816-453853a8c84a" />


<img width="1418" height="276" alt="image" src="https://github.com/user-attachments/assets/92865ef6-6434-4aaa-8d3a-4063ed047bd8" />


<img width="1056" height="563" alt="image" src="https://github.com/user-attachments/assets/272fd791-20a0-4a51-91dd-cfc860204665" />


<img width="1351" height="550" alt="image" src="https://github.com/user-attachments/assets/c0bbfb85-d51c-4b91-af6f-de8d2590b1ec" />


<img width="1389" height="331" alt="image" src="https://github.com/user-attachments/assets/d4f149f7-945b-4c8d-b3de-4576cdfba823" />

## 4. patching group of desktops/workstation 

### 4.1  Windows Cumulative Updates 

<img width="1390" height="288" alt="image" src="https://github.com/user-attachments/assets/e4e16fb8-0303-4920-9039-81c569a9d7d6" />


patching only the lsws workstations = you can filter which desktops you want to patch by typing in the filter search bar 


<img width="1386" height="591" alt="image" src="https://github.com/user-attachments/assets/32e3943c-da4b-486c-bb6b-9c56a7bbebcc" />

<img width="1369" height="431" alt="image" src="https://github.com/user-attachments/assets/2215ba1d-f7c9-47e2-832d-994d03df97a0" />


this patch is the latest for windows update 


<img width="560" height="340" alt="image" src="https://github.com/user-attachments/assets/f6df9032-d817-442f-bae3-58c067b53de6" />

>>continue to preview

>>deploy

<img width="1371" height="328" alt="image" src="https://github.com/user-attachments/assets/28f186e6-1792-4618-a6c1-183ba1f60510" />

If in case it expires or fails try to reissue again





## 5. Deploying package to a group of workstations

1. In Tanium Console, navigate to **Modules → Deploy → Software**.

2. Enter a **package Name** in the filter (example: 'Chromex64' 140.0.7339.81). and select **Deploy Package**

3. Select **Computer Groups** OR **Question Critera** ("select the group to patch",or "Enter a specific Question")

4. select **Preview to continue**

5. So the chrome v140.0.-- will be applied to the selected group

<img width="1411" height="792" alt="image" src="https://github.com/user-attachments/assets/bcf4c253-a3b3-4582-907e-b1f677e5fd73" />

<img width="1345" height="394" alt="image" src="https://github.com/user-attachments/assets/f4818709-d599-4b65-ae06-51c9507e8e8b" />
<img width="1281" height="374" alt="image" src="https://github.com/user-attachments/assets/d2577dd0-ba41-4a05-8fda-b35e1ec4aa32" />

<img width="512" height="269" alt="image" src="https://github.com/user-attachments/assets/7cd9ae7a-9208-4b23-83ba-fd83784169f4" />


## 6. Creating and Deploying Packages in Tanium

### 6.1 Create a New Package

1. In Tanium Console, navigate to **Administration → Packages → New Package**.

2. Enter a **Package Name** (example: `Azure Data Studio (System Installer) 1.52.0`).

3. Select the **Content Set** (commonly *LightStream* or your team’s custom set).

4. In the **Command** field, add the installation command. Example:

   ```cmd
   cmd.exe /c azuredatastudio-windows-system-installer-x64-1.52.0.exe /VERYSILENT /NORESTART
   ```

5. Adjust **Timeouts**:

   * Command Timeout → 10 minutes
   * Download Timeout → 20 minutes

6. Upload the installer file under **Files** (e.g., `azuredatastudio-windows-system-installer-x64-1.52.0.exe`).

7. Save the package.

---

### 6.2 Deploy the Package

1. Go to **Deploy → Deployment Package**.
2. Select the package you created (e.g., *Azure Data Studio (System Installer) 1.52.0*).
3. Choose the **Target Group** (e.g., specific workstations `LSDWS008, LSDWS081…`).
4. Set the **Schedule** (immediate or later).
5. Click **Deploy Action**.

---

### 6.3 Monitor Deployment

* Open **Deployments → Action Status**.
* You will see endpoints in different states:

  * *Waiting / Downloading / Running*
  * *Complete / Not Applicable / Failed*
* Example screenshot:

```markdown
<img src="https://github.com/<your-username>/<your-repo>/assets/screenshot.png" width="700">
```

---

### 6.4 Common Issues

* **Not Applicable** → Package already installed or version is current.
* **Failed** → Check installer command syntax, file upload, or timeout settings.
* **Policy Block (Error 1260)** → Local group policy restrictions, escalate to sysadmin











