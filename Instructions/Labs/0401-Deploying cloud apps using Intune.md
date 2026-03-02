# Lab 12: Deploying cloud apps using Intune

## Summary

In this lab, you create and deploy cloud-based apps using Intune and the Company Portal Website.

> **!IMPORTANT**: Once you launch the track, you’ll have access to a virtual machine (VM) for **40 hours**. The displayed track duration of **4 days 8 hours (104 hours)** indicates the time frame during which you can use your VM. Please plan your lab sessions accordingly. If the VM uptime of **40 hours** is fully exhausted before completing the labs, access will be lost. To avoid this and for detailed instructions on VM usage and stopping/deallocating the VM, refer to the Getting Started page.  

> If the full 40 hours of VM uptime is exhausted, the VM will no longer be accessible, and **the lab duration cannot be extended**.

### Prerequisites

To following lab(s) must be completed before this lab:

- 0101-Managing Identities in Entra ID

- 0102-Synchronizing Identities by using Microsoft Entra Connect

- 0203-Manage Device Enrollment into Intune

- 0204-Enrolling devices into Intune

  > Note: You will also need a mobile phone that can receive text messages used to secure Windows Hello sign in authentication to Azure AD.

## Exercise 1: Add a Microsoft Store App to Intune

### Scenario

You use Microsoft Intune to manage desktops and apps for Contoso Corporation. The Research department often connects to various servers to perform tasks and has asked for the Microsoft Remote Desktop app to be available for Research members to install as needed. The Microsoft Remote Desktop is available from the Microsoft Store, but you decide to add the app to Intune so that users can access it from the Company Portal website. A Research member named Aaron Nicholls has agreed to test the installation process after you have published the app to the portal.

### Task 1: Add Microsoft Remote Desktop to Intune

In this task you will add the Microsoft Remote Desktop (Windows App) to Intune so that Research users can install it from the Company Portal.

1. On **SEA-SVR1**, if necessary, sign in as **Contoso\\Administrator** with the password **Pa55w.rd** and close **Server Manager**.

     ![](../media/H2.png)

    ![](../media/p1t1s1.2.png)

2. On the taskbar, select **Microsoft Edge**.

3. In Microsoft Edge, type **https://intune.microsoft.com** in the address bar, and then press **Enter**.

4. Sign in as user **<inject key="AzureAdUserEmail"></inject>**, and use the tenant Admin password **<inject key="AzureAdUserPassword"></inject>**

5. On the **Microsoft Intune admin center** page select **Apps (1)**, then on the **Apps** page in the navigation pane select **All apps (2)**, and in the details pane select **+ Create (3)**.

   ![](../media/190.png)

8. On the **Select app type** page, click the drop-down menu and then Choose **Microsoft store app (new) (1)**. Click **Select (2)**.

   ![](../media/191.png)

9. On the **Add App** page, click **Search the  Microsoft Store app (new)**, search for and select **Windows App**. Click **Select**.

   ![](../media/192.png)

   ![](../media/1011.png)

10. On the **App information** page, verify the following information and then select **Next(5)**:
    - Name: **Windows App(1)**
    - Publisher: **Microsoft Corporation(2)**
    - Category: **Business(3)**
    - Show this as a featured app in the Company Portal: **Yes(4)**
 
      ![](../media/194.png) 

11. Select **Next** twice and then select **Create**.

    ![](../media/195.png)

12. The Windows App page opens.

    > Take note of the Properties, Device install status, and User install status nodes.

### Task 2: Assign a Group to the App

In this task you will assign the Research group to the app so members can see and install it from the Company Portal.

1. On the **Windows App** page select **Properties (1)**, then in the details pane scroll down to the **Assignments (2)** section and select **Edit (3)**.

   ![](../media/196.png)

3. On the **Assignments** page, select **Add group** in the **Available for enrolled devices**.

    ![](../media/197.png)

4. On the **Select groups** page, search and select the **Research** group and then click **Select**.

    ![](../media/198.png)

5. Select **Review + save** and then select **Save**.

    ![](../media/199.png)

    ![](../media/200.png)

### Task 3: Force policy synchronization from the Intune console

In this task you will force a policy sync on SEA-WS1 to ensure the assigned app and policies update immediately.

1. In the **Microsoft Intune admin center**, select **Devices (1)** and then select **All devices (2)**. In the details pane, select **SEA-WS1 (3)**.

    ![](../media/201.png)

3. On the **SEA-WS1** blade, select **Sync (1)** and when prompted select **Yes (2)**.

    ![](../media/202.png)

   > Intune will contact the device and tell it to synchronize all policies. This may take up to 5 minutes.

### Task 4: Install an app from the Company Portal Website

In this task you will sign in as Aaron Nicholls and install the Windows App from the Company Portal website.

   > **Note**: It can take several minutes for the app to appear in the Company Portal Website. If the app does not appear, wait a few minutes and then refresh the page. If the app still does not appear, verify that you have assigned the app to the correct group and that the device is a member of the group. (This could take up to 30 minutes.)

1. Switch to **HOSTVM** and sign in to **SEA-WS1** VM through desktop shortcut and verify that you are in basic session mode.

     ![](../media/dsk.png)

2. Sign in as **Aaron Nicholls** with the PIN **102938**.

3. On the taskbar, select **Microsoft Edge**.

4. If necessary, at the **Welcome to Microsoft Edge** page, select **Confirm and continue**. Close the Welcome page.

    ![](../media/1013.png)

5. In the address bar browse to **https://portal.manage.microsoft.com** and then press **Enter**.

6. Sign in as **Aaron Nicholls**.

7. On the Contoso web portal, select **Devices**.

    ![](../media/203.png)

    ![](../media/204.png)

8. On the Devices page, select **Tap here to tell us which device you're using or add a new device**.

    ![](../media/205.png)

9. On the **Which device are you using** dialog box, select the option next to **SEA-WS1**, and then select **Select**.

   ![](../media/206.png)

   > Notice that the message now changes to Apps will be installed onto: SEA-WS1

   ![](../media/207.png)

10. **At the top-left corner (1)**, select the navigation button and then select **Apps (2)**.

    ![](../media/208.png)

    > Take note of the Microsoft Remote Desktop app listed on the Apps page. It might take a few minutes for the app to appear.

11. Select **Windows App**.

    ![](../media/209.png)

12. On the Windows App page, select **Install**.

    ![](../media/210.png)

13. On the **Install Microsoft Remote Desktop** dialog box, select **Always allow portal.manage.microsoft.com to open links of this type in the associated app (1)** and then select **Open (2)**.

     ![](../media/211.png)

     >**Note:** It may take a few minutes for the app to install.

     ![](../media/212.png)

14. After the app is installed close all open windows.

15. Select **Start** and verify that **Windows App** is displayed on the Start menu.


**Results**: After completing this exercise, you will have successfully added and installed a Microsoft Store App from Intune.

## Exercise 2: Configure and deploy Microsoft 365 Apps from Intune

### Scenario

All the users of the Research department at Contoso require Microsoft 365 Apps. You've been asked to deploy the 64-bit versions of Microsoft Excel, Outlook, PowerPoint and Word to their Windows devices. You also need to ensure they are configured for the Current Channel for updates.

### Task 1: Verify installed apps on SEA-WS1

In this task you will verify which apps are installed on SEA-WS1 before deploying Microsoft 365 Apps.

1. On **SEA-WS1**, on the taskbar, select **Start (1)** and then select the **Settings (2)** app.

    ![](../media/214.png)

2. In the **Settings** app, select **Apps (1)** and on the **Apps & features (2)** page.

   ![](../media/215.png)

   > Verify that **Microsoft 365 Apps for enterprise - en-us** is not listed.

3. Close all open windows.

### Task 2: Add Microsoft 365 apps to Intune

In this task you will add Microsoft 365 Apps (Excel, Outlook, PowerPoint, and Word) to Intune and assign them to the Research group.

1. On **SEA-SVR1**, in the **Microsoft Intune admin center** select **Apps (1)**, then in the **Apps | Overview** blade select **All Apps (2)**, and in the details pane select **Create (3)**.

   ![](../media/216.png)

3. In the **Select app type** blade, under **Microsoft 365 Apps (1)**, select **Windows 10 and later** , and then click **Select (2)**.

    ![](../media/1014.png)

    ![](../media/217.png)

4. On the **Add Microsoft 365 Apps** blade, configure the following options and select **Next (3)**:

    - Suite Name: **Microsoft 365 Apps (Research) (1)**

    - Description: **Microsoft 365 Apps for the Research dept at Contoso (2)**

      ![](../media/1015.png)

5. On the **Configure app suite** tab, expand the **Select Office apps** dropdown, and ensure that only the following apps are selected:

    - Excel

    - Outlook

    - PowerPoint

    - Word

      ![](../media/219.png)

6. On the **App suite information** section, configure the following options:

     - Architecture: **64-bit (1)**

     - Default file format: **Office Open XML Format (2)**

     - Update channel: **Monthly Enterprise Channel (3)**

7. On the **properties** section, configure the following options and select **Next (5)**:

     - Accept the Microsoft Software License Terms on behalf of users: **Yes (4)**

       ![](../media/220.png)
     
8. On the **Assignments** tab, in the **Required** section, select **Add group.**

    ![](../media/221.png)

9. On the **Select groups** blade, on search bar serach for **Release (1)** select **Research (2)**, and then choose **Select (3)**.

    ![](../media/222.png)

10. Select **Next**. On the **Review + Create** tab, select **Create**.

    ![](../media/223.png)

11. On the **Microsoft 365 Apps (Research)** page, select **Properties (1)**. In the details pane verify that **Research (2)** is listed under **Required** in the **Assignments** section.

    ![](../media/1016.png)

### Task 3: Force policy synchronization from the Intune console

In this task you will sync SEA-WS1 again so the Microsoft 365 Apps installation begins quickly.

1. In the **Microsoft Intune admin center**, select **Devices (1)** and then select **All devices (2)**. In the details pane, select **SEA-WS1 (3)**.

    ![](../media/225.png)

3. On the **SEA-WS1** blade, select **Sync (1)** and when prompted select **Yes (2)**.

   ![](../media/226.png)

   > Intune will contact the device and tell it to synchronize all policies. This may take up to 5 minutes.


### Task 4: Verify Microsoft 365 apps are installed

n this task you will verify that Microsoft 365 Apps have been successfully installed on SEA-WS1.

1. Switch to **HOSTVM** and sign in to **SEA-WS1** and wait approximately 10-15 minutes for the Microsoft 365 Suite to install on the device.

2. Sign out of **SEA-WS1** and then sign back in as **Aaron Nicholls** with the PIN **102938**.

3. On **SEA-WS1**, on the taskbar, select **Start** and then select the **Settings** app.

    ![](../media/227.png)

4. In the **Settings** app, select **Apps** and on the **Apps & features** page, scroll down and verify that **Microsoft 365 Apps for enterprise - en-us** is listed.

   ![](../media/228.png)

   ![](../media/229.png)
  
   >**Note**: If the above said app is not listed, restart the SEA-WS1 and sign in back with PIN **102938**

5. Close the **Settings** app and select the **Start** button.

6. In the app list, select **Word** and verify that the app opens.

    ![](../media/230.png)

    ![](../media/231.png)

7. Close all open windows.

8. Sign out of SEA-WS1.

### Task 5: Monitor app installation status in Intune

In this task you will monitor app installation status in Intune to confirm deployment for users and devices.

1. Switch to **SEA-SVR1**.

2. In the **Microsoft Intune admin center**, select **Apps (1)**. On the **Apps | Overview** blade, select **Monitor (2)** and then select **App install status (3)**.

    ![](../media/232.png)

4. In the details pane, select **Microsoft 365 Apps \(Research\)**.

   ![](../media/1017.png)

5. In the details pane, under **Monitor** and under **User install status**, verify that **1** is displayed under Installed.

    ![](../media/234.png)

   _Note: that it may take some time for the information to display._
   
   _Note: This indicates that the app is installed on one device and for one user._

6. Select **Device install status**.

   ![](../media/235.png)

   > In the details pane, you can see the devices that the app is installed on, and also the name of the user. The **Device Name** column should list **SEA-WS1** and the **Status** column should say **Installed**. This means that the app is installed on SEA-WS1.

   _Note: that it may take some time for the information to display._

7. In the **Microsoft Intune admin center**, select **Devices (1)**. On the **Devices | Overview** blade, select **All devices (2)** and then in the details pane, select **SEA-WS1 (3)**.

    ![](../media/236.png)

9. On the **SEA-WS1** blade select **Managed Apps (1)**, then on the **SEA-WS1 | Managed Apps** blade in the details pane select **Microsoft 365 Apps (Research) (2)**.

   ![](../media/1018.png)

   ![](../media/1019.png)

   > On the **Microsoft 365 Apps (Research) - Installation details** window, you can see the entire lifecycle of the application, that is - when it was created, assigned, installation time and status and the last time the device checked in (synced with Intune).

11. Close all open windows.

**Results**: After completing this exercise, you will have successfully configured and deployed Microsoft 365 Apps from Intune.

Click on **Next** from the lower right corner to move on to the next page.

  ![](../media/pgn.png)
