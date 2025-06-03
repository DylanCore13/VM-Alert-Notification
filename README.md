# VM-Alert-Notification

![image](https://github.com/user-attachments/assets/fd1492f6-b281-4c89-ab10-076fda79236c)

<h2>Description</h2> 

This project will showcase proactive IT support skills by implementing an Azure Monitor alert to detect high CPU utilization on an Azure Virtual Machine. It will demonstrate how help desk teams can be automatically notified of potential performance issues before user impact.

<h2>Skills Demonstrated</h2>

- Azure Monitoring (Azure Monitor)
- Proactive Incident Detection
- Alert Rule Configuration
- Notification Setup (Azure Action Groups)
- Basic Performance Metric Understanding
- Cloud VM Lifecycle Awareness

<h2>Azure Services Used</h2>

- Azure Virtual Machines 
- Azure Monitor
- Azure Action Groups 
- Azure Resource Groups


<h2>Part 1: Ensure Your Azure VM is Running</h2>

- Log in to Azure Portal, then start your VM from a previous lab/activity or create a new one, new resource group and VM, both in same AZ

![image](https://github.com/user-attachments/assets/b8f26813-f15c-4521-8eb2-3db2c093301b)


<h2>Part 2: Create an Action Group (for Notifications)</h2>

<h1>An Action Group defines who gets notified and how (email, SMS, webhook, etc.).</h1>

- Create Action Group:
- In the Azure Portal search bar, type "Action groups" and select it.
 - Click "+ Create". Then go to Basics Tab then Project details
- Subscription: Your subscription.
- Resource group: The one you created 
- Instance details:
- Action group name: VMPerformanceAlerts
- Display name: VM Performance Alerts
- Click "Next: Notifications >".
- Notifications Tab:
- Click "+ Add notification".
- Notification type: Email/SMS message/Push/Voice
- Name: EmailMe
- Email: Check "Email" and enter your personal email address.
- Click "OK".
- Click "Next: Actions >" (you can skip actions for this simple lab).
- Click "Next: Review + create >", then "Create".

