# Virtual Machine Alert Notification lab

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

- Log in to Azure Portal, then start your VM from a previous lab/activity or create a new one, new resource group and VM, both in same AZ/location

![image](https://github.com/user-attachments/assets/b8f26813-f15c-4521-8eb2-3db2c093301b)


<h2>Part 2: Create an Action Group (for Notifications)</h2>

<h1>An Action Group defines who gets notified and how (email, SMS, webhook, etc.).</h1>

- Navigate to Azure Monitor first:

    - In the Azure Portal search bar, type "Monitor" and select "Monitor" (the service with the speedometer icon).
      - In the left-hand menu of the Monitor blade, under "Alerts", select "Action groups".
        - Create Action Group:

      ![image](https://github.com/user-attachments/assets/44ba932b-725c-4f0c-8643-2615220ac654)

- On the "Action groups" page, click "+ Create".
- Basics Tab:
- Project details:
- Subscription: Choose your Azure subscription.
- Resource group: Select HelpDeskVMRG (or the resource group where your VM is located).
- Instance details:
- Action group name: VMPerformanceAlerts (This must be unique within the resource group).
- Display name: VM Performance Alerts (This is the friendly name you'll see).

![image](https://github.com/user-attachments/assets/a685ff55-f797-4724-b28a-515b8defc37b)


- Click "Next: Notifications >".
- Notifications Tab:
- Click "+ Add notification".
- Notification type: Select Email/SMS message/Push/Voice
- Name: EmailMe (or a descriptive name for this notification)
- Email: Check "Email" and enter your personal email address.
- Click "OK".
- Click "Next: Actions >" (you can skip this for this simple lab, it's for triggering automated tasks like Azure Functions or Logic Apps).
- Click "Next: Review + create >", then "Create".


![image](https://github.com/user-attachments/assets/6e0d701a-7a9b-4f69-82a8-adb27ebdf1c4)



<h2>Part 3: Create an Alert Rule for VM Performance</h2>

<h3>Now, you'll create the actual alert that uses the action group.</h3>

- Navigate to your VM:
- In the Azure Portal search bar, type "Virtual machines" and select it.
- Click on your HelpDeskVM (or the name of your VM).
- Create Alert Rule:
- In the left-hand menu, under "Monitoring", click "Alerts".
- Click "+ Create" -> "Alert rule".

![image](https://github.com/user-attachments/assets/8c16fe9a-7e0e-418b-9ccd-417db25a54fe)

  
- Scope Tab: Your VM should already be selected. Click "Next: Condition >".

![image](https://github.com/user-attachments/assets/50ac5fa6-30a0-4460-84dd-82128c5ce05e)


- Condition Tab (Define the alert logic):
- Click "+ Add condition".
- Signal name: Search for Percentage CPU and select it.
- Logic:
- Threshold: Static
- Operator(Value is): Greater than
- Aggregation type: Average
- Threshold value: 80 (This means trigger if average CPU goes above 80%).
- Unit: %
- Check frequency: Every 1 minute
- Period: Over the last 5 minutes (This means average CPU over the last 5 mins).
- Click "Done".

  ![image](https://github.com/user-attachments/assets/f67ff85c-225c-4ac8-9caa-2fff734d283d)

- Click "Next: Actions >".
- Actions Tab (Link to your Action Group):
- Select "Select action groups".
- Check the VMPerformanceAlerts action group you just created.
- Click "Select".


  ![image](https://github.com/user-attachments/assets/f401d20f-5001-45a5-87e2-1f6ea3121480)

- Click "Next: Details >".
- Details Tab:
- Alert rule name: High CPU Alert - HelpDeskVM
- Description: Alerts when HelpDeskVM CPU utilization exceeds 80% for 5 minutes.
- Severity: Sev 2 (High) (Help desk would typically act on this).
- Enable alert rule upon creation: Leave checked.
- Click "Next: Tags >" (optional).
- Click "Next: Review + create >", then "Create".

![image](https://github.com/user-attachments/assets/4e22bca8-ee56-4a30-96dd-11675f7b7cbd)




<h2>Part 4: Test the Alert (Optional but Recommended)</h2>

- Log into your VM via RDP.

![image](https://github.com/user-attachments/assets/457dca1e-6644-4f86-a2b1-5f19d3e1db8d)


<h2>Generate CPU Load</h2>

   <h3>- Goal: Intentionally make your VM's CPU utilization go above the 80% threshold you set.</h3>
   
- For Windows VM:

- Open Task Manager (Ctrl + Shift + Esc). Go to the "Performance" tab and observe the CPU graph.

  ![image](https://github.com/user-attachments/assets/dfb6a0a7-914f-4029-82e5-9b42c789bdc7)

  
- Open several applications simultaneously (e.g., multiple browser tabs, a few Notepad instances, Calculator, Paint, etc.).
  
- For a more consistent load, you can run a simple, harmless CPU-intensive command in Command Prompt. Type cmd in the Windows search bar, open Command Prompt, then type (and press Enter):

for /l %i in (1,0,2) do @echo %i

This command will create an infinite loop, driving up your CPU. Make sure to close this Command Prompt window once you've triggered the alert!

![image](https://github.com/user-attachments/assets/de1412b3-42ee-410f-bd6e-41aa3434cff3)



- Linux VM (if you used one):
  - Connect via SSH.
  - Install stress-ng: sudo apt install stress-ng
  - Run a stress test: stress-ng --cpu 4 --timeout 60s (stresses 4 CPUs for 60 seconds). Adjust --cpu to your VM's core count.


  
- Observe Alert:
- After a few minutes of high CPU, check your email inbox (the one you configured in the Action Group).
- You should receive an email notification from Azure Monitor about the "High CPU Alert - AlertVM."
- Stop CPU Load: Close the applications or commands that were stressing the CPU. Your CPU utilization should drop, and after a few minutes, you might receive a "Resolved" alert notification!!!!
  


![image](https://github.com/user-attachments/assets/e20e026b-ba87-4b1d-8c6c-acd47edec061)


![image](https://github.com/user-attachments/assets/78c04e75-ba78-4e35-946b-e8fecd8ec053)



![image](https://github.com/user-attachments/assets/a19d4fb3-199d-4c33-8bd9-0034e7bd29ee)


![image](https://github.com/user-attachments/assets/9209883e-a366-4161-9ccf-730273d5a0cb)


Final Critical Clean Up Steps (DO NOT FORGET!):

To ensure you don't incur unexpected Azure costs:

Clean up any resources associated with this lab!!!!!

