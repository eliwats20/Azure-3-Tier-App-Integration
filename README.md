# 🏗️ Azure 3‑Tier Web Application Architecture  
*A secure, enterprise‑style cloud deployment using App Services, Azure SQL, VNets, NSGs, and Private Endpoints.*

---

## 📌 Project Overview

This project demonstrates a fully deployed **3‑tier cloud architecture** on Microsoft Azure, designed to replicate real enterprise environments. The architecture includes:

- **Frontend Web App (Public App Service)**
- **Backend API (Private App Service)**
- **Azure SQL Database (Private Endpoint Only)**
- **Virtual Network with Subnets**
- **Network Security Groups (NSGs)**
- **Log Analytics Workspace + Diagnostic Settings**
- **Optional: Azure Key Vault (Architectural Only)**

The goal was to build a **secure, isolated, production‑style environment** using Azure best practices — even within the limitations of an Azure for Students tenant.

---

## 🧩 Architecture Diagram  
![diagram](./Images/3-Tier%20Azure%20Architecture.png)

---

## 🧱 Architecture Components

### **Frontend App Service (Web Tier)**
- Publicly accessible  
- Hosts the static frontend  
- Sends API calls to the backend  
- Connected to Log Analytics for monitoring  

### **Backend App Service (Application Tier)**
- Integrated into the VNet using Regional VNet Integration  
- Not publicly accessible  
- Communicates with SQL Database through a private endpoint  
- Logs sent to Log Analytics  

### **Azure SQL Database (Data Tier)**
- Public access disabled  
- Private endpoint created inside the Data Subnet  
- Only reachable from backend App Service  
- SQL auditing + diagnostics enabled  

### **Virtual Network**
- `snet-web`  
- `snet-app`  
- `snet-db`  
- `snet-backend-pep`
- `keyvault-pep`

### **Network Security Groups**
- Restrict traffic between tiers  
- Enforce least‑privilege access  
- Block all unnecessary inbound/outbound traffic  

### **Log Analytics Workspace**
- Centralized logging for:
  - Frontend App Service  
  - Backend App Service  
  - SQL Database  

### **Azure Key Vault (Optional Component)**
- Deployed with private endpoint  
- Due to tenant restrictions, secret access was not possible  
- Still included architecturally to demonstrate secure secret storage patterns  

---

## 🔐 Security Highlights

This project follows real‑world enterprise security patterns:

- Zero‑trust architecture  
- Private endpoints for SQL (and Key Vault if included)  
- No public access to backend or database  
- NSGs enforcing tier‑to‑tier communication  
- App Service VNet Integration  
- Diagnostic logs for all tiers  
- SQL auditing enabled  

---

## 📡 Traffic Flow

1. User accesses the **Frontend App Service** (public).  
2. Frontend sends API requests to the **Backend App Service**.  
3. Backend communicates with **SQL Database** through a **private endpoint**.  
4. Logs from all tiers flow into **Log Analytics Workspace**.

---

## 🛠️ Deployment Steps (Summary)

### **1. Create Resource Group**
Organized all project resources in a single RG.
<img width="475" height="443" alt="image" src="https://github.com/user-attachments/assets/18821f3f-a411-450c-93af-aaeb78af7a95" />


### **2. Build the Virtual Network**
- Created VNet  
- Added subnets for frontend, backend, data, and private endpoints
<img width="472" height="425" alt="image" src="https://github.com/user-attachments/assets/7621e144-3dd1-44c2-a25e-f3d912cebe88" />
<img width="475" height="417" alt="image" src="https://github.com/user-attachments/assets/d37c4397-df38-4d06-bc72-15448bfeec42" />


### **3. Deploy App Services**
- Frontend App Service (public)  
- Backend App Service (private via VNet integration)
<img width="476" height="444" alt="image" src="https://github.com/user-attachments/assets/8f359612-ca81-49ca-a293-a77934f1d3d6" />


### **4. Deploy SQL Database**
- Disabled public access  
- Created private endpoint in Data Subnet  
<img width="471" height="411" alt="image" src="https://github.com/user-attachments/assets/8ca62a8e-3690-4594-8cde-2d919899bb64" />
<img width="474" height="416" alt="image" src="https://github.com/user-attachments/assets/426c11de-ff89-4764-88b6-f7730fd4083f" />


### **5. Configure NSGs**
- Allowed only required traffic between tiers  
- Blocked all other inbound/outbound traffic
<img width="476" height="418" alt="image" src="https://github.com/user-attachments/assets/2d690a61-ac30-41b6-ac1d-29ea11992e1f" />



### **6. Configure Diagnostic Settings**
Enabled logs for:
- Frontend App Service  
- Backend App Service  
- SQL Database
<img width="470" height="449" alt="image" src="https://github.com/user-attachments/assets/daf56075-821e-4811-856f-074dc2392edf" />


All logs sent to Log Analytics Workspace.

### **7. (Optional) Deploy Key Vault**
- Added private endpoint  
- Could not store secrets due to tenant restrictions  
- Still included for architectural completeness
<img width="475" height="414" alt="image" src="https://github.com/user-attachments/assets/9b3f3ce1-3fa9-463c-8cbb-9af387f842b8" />


---

## 📊 Monitoring Setup

Even without dashboards, monitoring is fully configured:

- App Service HTTP logs  
- Application logs  
- Platform logs  
- SQL auditing  
- SQL performance logs  
- IP security logs  
- All logs centralized in Log Analytics
<img width="472" height="450" alt="image" src="https://github.com/user-attachments/assets/1bdfc23f-6998-46ef-aacb-0277d80cea66" />


---

## 🧠 What I Learned / Achieved

- Built a complete 3‑tier cloud architecture  
- Implemented secure networking using VNets and NSGs  
- Configured private endpoints for SQL  
- Integrated App Services with VNets  
- Set up centralized monitoring with Log Analytics  
- Understood real‑world Azure restrictions and workarounds  
- Practiced designing enterprise‑grade cloud environments  

---

## ⚠️ Challenges Faced

### **Azure for Students Tenant Restrictions**
- Could not assign RBAC roles to Key Vault  
- Could not store or retrieve secrets  
- Some identity features were blocked  

**Solution:**  
Kept Key Vault architecturally, documented the limitation, and continued with the rest of the design.

### **Private Endpoint Blocking Access**
Once private endpoints were enabled:
- Could not access SQL or Key Vault from local machine  
- Had to rely on backend App Service for connectivity  

**Solution:**  
Documented the behavior and validated connectivity through the backend.

### **Diagnostic Settings Confusion**
Initially created diagnostic settings from the workspace instead of the resource.

**Solution:**  
Re‑created diagnostic settings inside each App Service and SQL Database.

### CI/CD Pipeline Attempt (Failed)
- Attempted to set up a GitHub Actions CI/CD pipeline  
- Pipeline failed because the project does not include a full backend web server  
- Static frontend + minimal backend API did not justify a full deployment pipeline  

**Solution:**  
Documented the attempt and chose manual deployment for this small‑scale project.

---

## 🏁 Conclusion

This project successfully demonstrates the design and deployment of a secure, scalable, enterprise‑style 3‑tier architecture on Azure. Despite tenant limitations, the core principles of cloud networking, security, monitoring, and architecture were fully implemented.

This project showcases real‑world cloud engineering skills and serves as a strong portfolio piece for Azure, cloud, and DevOps roles.
