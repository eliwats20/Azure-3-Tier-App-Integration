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
- `frontend-subnet`  
- `backend-subnet`  
- `data-subnet`  
- `private-endpoint-subnet`  

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

### **2. Build the Virtual Network**
- Created VNet  
- Added subnets for frontend, backend, data, and private endpoints  

### **3. Deploy App Services**
- Frontend App Service (public)  
- Backend App Service (private via VNet integration)  

### **4. Deploy SQL Database**
- Disabled public access  
- Created private endpoint in Data Subnet  

### **5. Configure NSGs**
- Allowed only required traffic between tiers  
- Blocked all other inbound/outbound traffic  

### **6. Configure Diagnostic Settings**
Enabled logs for:
- Frontend App Service  
- Backend App Service  
- SQL Database  

All logs sent to Log Analytics Workspace.

### **7. (Optional) Deploy Key Vault**
- Added private endpoint  
- Could not store secrets due to tenant restrictions  
- Still included for architectural completeness  

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

---

## 📸 Screenshots  
*(Add your screenshots here)*

Suggested screenshots:
- Resource Group overview  
- VNet + Subnets  
- NSGs  
- App Services  
- SQL private endpoint  
- Diagnostic settings  
- Log Analytics workspace  

---

## 🏁 Conclusion

This project successfully demonstrates the design and deployment of a secure, scalable, enterprise‑style 3‑tier architecture on Azure. Despite tenant limitations, the core principles of cloud networking, security, monitoring, and architecture were fully implemented.

This project showcases real‑world cloud engineering skills and serves as a strong portfolio piece for Azure, cloud, and DevOps roles.
