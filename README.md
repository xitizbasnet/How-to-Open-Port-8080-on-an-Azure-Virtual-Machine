# How to Open Port 8080 on an Azure Virtual Machine

This guide provides a comprehensive, step-by-step walkthrough to **open TCP port 8080** on an Azure Virtual Machine (VM). It covers both **Azure Network Security Group (NSG)** configuration and **OS-level firewall settings** (Windows & Linux). Perfect for developers, DevOps engineers, and system admins deploying web apps or APIs on Azure.

---

## 📌 Prerequisites

- An active **Microsoft Azure subscription**
- Access to an existing **Azure VM**
- Basic knowledge of **networking** and **firewall rules**

---

## 🛠️ Step 1: Configure Azure Network Security Group (NSG)

1. **Log in to Azure Portal**  
   👉 [https://portal.azure.com](https://portal.azure.com)

2. **Navigate to Virtual Machines**  
   - Go to **"Virtual Machines"** from the left-hand menu  
   - Select your target VM

3. **Open the Networking Settings**  
   - In the VM menu, click on **"Networking"**  
   - Identify the **Network Security Group (NSG)** attached to the network interface or subnet

4. **Edit the NSG Inbound Rules**  
   - Click on the **NSG name**
   - Select **"Inbound security rules"**
   - Click **"+ Add"** and configure the rule:

     | Field               | Value              |
     |--------------------|--------------------|
     | Source             | Any (or IP Range)  |
     | Source port ranges | *                  |
     | Destination        | Any                |
     | Destination port   | `8080`             |
     | Protocol           | TCP                |
     | Action             | Allow              |
     | Priority           | 1000 (or suitable) |
     | Name               | Allow-Port-8080    |

   - ✅ Click **"Add"**

---

## 💻 Step 2: Configure the VM's Firewall

### 🪟 For Windows VM

5. **Connect via RDP**  
   - From the VM Overview page → **Connect > RDP**  
   - Download the `.rdp` file and log in using VM credentials

6. **Open Firewall Settings**  
   - Press `Win + R`, type `wf.msc`, press Enter

7. **Create New Inbound Rule**  
   - Go to **Inbound Rules > New Rule**  
   - Select **Port**, click **Next**  
   - Choose **TCP**, specify port `8080`  
   - Select **Allow the connection**  
   - Apply to all profiles (Domain, Private, Public)  
   - Name it `Allow Port 8080`, click **Finish**

### 🐧 For Linux VM

5. **Connect via SSH**  
   Use your terminal or Azure Cloud Shell:
   ```bash
   ssh username@<your-vm-public-ip>

6. **Open the Port in Firewall**

   **Ubuntu / Debian (UFW):**

   ```bash
   sudo ufw allow 8080/tcp
   sudo ufw reload
   ```

   **CentOS / RHEL (firewalld):**

   ```bash
   sudo firewall-cmd --permanent --add-port=8080/tcp
   sudo firewall-cmd --reload
   ```

---

## ✅ Step 3: Verify the Port is Open

Use any of the following to test:

* **Browser**:

  ```
  http://<your-vm-public-ip>:8080
  ```

* **Telnet (from local machine)**:

  ```bash
  telnet <your-vm-public-ip> 8080
  ```

* **Online tools** like [https://canyouseeme.org](https://canyouseeme.org)

---

## 📚 Use Cases

* Hosting web applications
* Running backend APIs
* Serving dashboards (e.g., Grafana, Jupyter)
* Docker container port exposure

---

## 🧠 Pro Tips

* 🔒 **Limit source IP** in NSG rules to restrict access for better security
* 📋 Keep your **NSG priorities** organized to avoid rule conflicts
* 🚫 Disable the port once it's no longer needed to minimize attack surface

---

## 📎 License

This guide is provided under the [MIT License](LICENSE).

---

## 🙋‍♂️ Author

**Name**: Xitiz Basnet
**Role**: Cloud | DevOps | System Engineer
**GitHub**: [github.com/xitizbasnet](https://github.com/xitizbasnet)
**LinkedIn**: [linkedin.com/in/xitizbasnet](https://linkedin.com/in/xitizbasnet)

---

> 💬 *Feel free to fork, contribute, or raise an issue if you find anything unclear or outdated!*

---
