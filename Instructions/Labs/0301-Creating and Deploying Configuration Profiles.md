# Practice Lab: Creating and Deploying Configuration Policies

## Summary

In this lab, you will use Microsoft Intune to create and apply a Configuration policy for a Windows 11 device.

### Prerequisites

To following lab(s) must be completed before this lab:

- 0101-Managing Identities in Entra ID

- 0102-Synchronizing Identities by using Microsoft Entra Connect

- 0203-Manage Device Enrollment into Intune

- 0204-Enrolling devices into Intune

  > Note: You will also need a mobile phone that can receive text messages used to secure Windows Hello sign in authentication to Azure AD.

## ## Exercise 1: Create and apply a Configuration policy

### Scenario

You need to use Entra and Intune to manage members of the Developers department at Contoso . You have been asked to evaluate the solutions that would enable the users to work effectively and securely on Windows 11 devices. Aaron Nicholls has volunteered to help you test and evaluate the solution and provide feedback. He has also given you some initial requirements that must be included and applied to the developer's Windows devices:

- The Gaming section in Settings should not be visible.
- The Privacy section in Settings should be restricted as much as possible.
- The C:\DevProjects folder must be excluded from Windows Defender.
- The process devbuild.exe must be excluded from Windows Defender.
- Most used apps and Recently added apps should not be displayed on the Start menu.


### Task 1: Verify device settings

In this task you will check the current settings on the SEA-WS1 device to understand what needs to be changed through the Intune configuration profile.

1. Switch to **HOSTVM** and Sign in to **SEA-WS1** VM from the desktop shortcut as **Aaron Nicholls** with the PIN **102938**

    ![](../media/dsk.png)

   >**Note** : Ensure that you are in basic session mode and able to view Clipboard in the menu bar as shown in the below image. If not please change it to the basic session by selecting the icon which was highlighted in the tool bar in the below image and then sign in with PIN.

   ![](../media/passwordwriteback1.png)

3. On the taskbar, select **Start (1)** and then select **Settings (2)**.

   ![](../media/41.png)

4. On the **Settings** navigation list, verify that you can see the **Gaming** setting.

   ![](../media/42.png)

5. Select the **Personalization (1)** setting and then on the Personalization page, select **Start (2)**. Ensure that **Show recently added apps** and **Show most used apps** are both set to **On**.

   ![](../media/1009.png)

   ![](../media/44.png)

6. In the **Settings** app, select **Privacy & security**.

7. On the **Privacy & security** page, take note of the options under **Security**, **Windows permissions**, and **App permissions**.

8. On the **Privacy & security** page, select **Windows Security** and then select **Open Windows Security**.

   ![](../media/45.png)

9. On the **Windows Security** page, select **Virus & threat protection**.

   ![](../media/46.png)

10. On the **Virus & threat protection** page, under **Virus & threat protection settings**, select **Manage settings** . 

    ![](../media/47.png)

11. Scroll down to **Exclusions** and select **Add or remove exclusions**. At the User Account Control, select **Yes**.

    ![](../media/48.png)

    ![](../media/49.png)

12. On the **Exclusions** page, verify that no exclusions have been configured.

      ![](../media/50.png)

13. Close the **Windows Security** window.

14. Close the **Settings** window.

### Task 2: Create a Configuration policy based on scenario requirements

In this task you will create a new Intune configuration profile that applies the required restrictions and Defender exclusions for Contoso developers.

1. Switch to **SEA-SVR1** and enter **Pa55w.rd** at the Password section.

2. On **SEA-SVR1**, on the taskbar, select **Microsoft Edge**.

3. In Microsoft Edge, type **https://intune.microsoft.com** in the address bar, and then press **Enter**. 

4. Sign in as user **<inject key="AzureAdUserEmail"></inject>**, and use the tenant Admin password **<inject key="AzureAdUserPassword"></inject>** 

1. In the **Microsoft Intune admin center**, select **Devices (1)** from the navigation bar, then on the **Devices | Overview** page select **Configuration (2)**, and on the **Devices | Configuration** blade in the details pane select **+ Create (3)** and then select **+ New policy (4)**.

   ![](../media/52.png)

8. In the **Create a profile** blade, select the following options, and then select **Create**:

   - Platform: **Windows 10 and later (1)**
   - Profile type: **Templates (2)**
   - Template name: **Device restrictions (3)**

      ![](../media/53.png)

9. In the **Basics** blade, enter the following information, and then select **Next (3)**:

   - Name: **Contoso Developer - standard (1)**
   - Description: **Basic restrictions and configuration for Contoso Developers. (2)**

     ![](../media/54.png)

10. On the **Configurations settings** blade, expand **Control Panel and Settings**. 

11. Select **Block** next to the **Gaming** and **Privacy** options.

     ![](../media/55.png)

12. On the **Device restrictions** blade, expand **Start**. 

    ![](../media/56.png)

13. Scroll down and select **Block** next to **Most used apps**, **Recently added apps** and **Recently opened items in Jump Lists**.

    ![](../media/57.png)

14. On the **Device restrictions** blade, scroll down and expand **Microsoft Defender Antivirus**. 

    ![](../media/58.png)

15. Under **Microsoft Defender Antivirus,** scroll down and expand **Microsoft Defender Antivirus Exclusions (1)**.

16. Under **Microsoft Defender Antivirus Exclusions** in the **Files and folders** box, type the following:

    **C:\\DevProjects (3)**.

17. In the **Processes** box, type the following:
    **DevBuild.exe (4)**. 

      ![](../media/59.png)

18. Select **Next** three times until you reach the **Review + create** blade. Select **Create**.

      ![](../media/60.png)

### Task 3: Create the Contoso Developer device group

In this task you will create a device group in Entra ID to target the configuration profile to specific developer devices.

1. In the **Microsoft Intune admin center**, in the navigation pane select **Groups (1)**, and on the **Groups | All groups (2)** blade select **New group (3)**.

   ![](../media/61.png)

3. On the **New Group** blade, enter the following information:

   - Group type: **Security (1)**
   - Group name: **Contoso Developer devices (2)**
   - Group description: **All Windows devices in Contoso Developer department (3)**
   - Membership type: **Assigned (4)**
   - Under **Members**, select **No members selected (5)**. 

     ![](../media/62.png)

5. On the **Add members** blade, in the **Search** box type **Sea (1)**. Select **SEA-WS1 (2)** and then choose **Select (3)**.

   ![](../media/63.png)

6. On the **New Group** blade, select **Create**. 

   ![](../media/64.png)

7. On the **Groups | All groups** blade, verify that the **Contoso developer devices** group is displayed.

   ![](../media/65.png)

### Task 4: Create a dynamic Entra device group

In this task you will create a dynamic device group that automatically includes all Windows devices based on their operating system.

1. On the **Groups | All Groups (1) (2)** blade, on the details pane, select **New group (3)**.

   ![](../media/66.png)

2. On the **Group** blade, provide the following values:

   - Group type: **Security (1)**
   - Group name: **Windows Devices (2)**
   - Membership type: **Dynamic Device (3)**
   - Under the **Dynamic Device Members** section, select **Add dynamic query (4)**. 

     ![](../media/67.png)

4. On the **Dynamic membership rules** blade, in the **Rule syntax** section, select **Edit**. 

   ![](../media/68.png)
    
5. In the **Edit rule syntax (1)** text box, add the following simple membership rule and select **OK (2)**.

    ```
    (device.deviceOSType -contains "Windows")
    ```

     ![](../media/69.png)      
      

6. On the **Dynamic membership rules** blade, select **Save**.

   ![](../media/70.png)

7. On the **New Group** page, select **Create**.

   ![](../media/71.png)

### Task 5: Assign a Configuration policy to Windows devices

In this task you will assign the configuration profile to the developer device group so the settings apply to SEA-WS1.

1. In the **Microsoft Intune admin center**, in the navigation pane select **Devices (1)**, then on the **Devices | Overview** blade select **Configuration (2)**, and on the **Devices | Configuration** blade in the details pane select the **Contoso Developer – standard (3)** profile.

   ![](../media/72.png)

4. On the **Contoso Developer – standard** blade, scroll down to the **Assignments** section, and select **Edit**.

   ![](../media/73.png)

5. On the Assignments page, under **Included groups** select **Add groups**.

   ![](../media/74.png)

6. On the **Select groups to include** blade, in the **Search (1)** box, select **Contoso Developer devices (2)** and then select **Select (3)**.

   ![](../media/75.png)

7. Back on the **Device restrictions** blade, select **Review + save**, then select **Save**.

   ![](../media/76.png)

   ![](../media/77.png)

8. In the Microsoft Intune admin center, select **Devices** in the breadcrumb navigation menu.

### Task 6: Verify that the Configuration policy is applied

In this task you will verify on SEA-WS1 that Intune has applied the configuration profile and that all required changes are in effect.

1. Switch to **HOSTVM** and sign in to **SEA-WS1** VM from the desktop shortcut.

2. On **SEA-WS1**, on the taskbar, select **Start** and then select **Settings**.

   ![](../media/78.png)

3. In **Settings**, select **Accounts (1)** and then select **Access work or school (2)**.

   ![](../media/79.png)

4. In the **Access work or school** section, select the **Connected to Contoso's Azure AD** link and then select **Info**.

   ![](../media/80.png)

5. In the **Managed by Contoso** page, scroll down and then under Device sync status, select **Sync**. Wait for the synchronization to complete.

   ![](../media/81.png)

6. Close the **Settings** app.

   _Note: The sync progress may take up to 15 minutes before the profile is applied to the Windows 11 device. Signing out or restarting the device can accelerate this process. PIN **102938**_

7. On **SEA-WS1**, select **Start** and then select **Settings**. Verify that the **Gaming** setting has been removed.

   ![](../media/82.png)

8. Select **Privacy & security** and notice that many of the privacy settings are now hidden. 

9. Select the **Personalization** setting and then select **Start**. Verify that **Show recently added apps** and **Show most used apps** are set to **Off**. 

   ![](../media/83.png)

10. In the **Settings** app, select **Privacy and Security**. On the **Privacy & Security** page, select **Windows Security** and then select **Open Windows Security**.

    ![](../media/84.png)

    ![](../media/04.png)

12. On the **Windows Security** page, select **Virus & threat protection**.

    ![](../media/85.png)

13. On the **Virus & threat protection** page, select **Manage settings** under **Virus & threat protection settings**. 

      ![](../media/86.png)

14. Scroll down to **Exclusions** and select **Add or remove exclusions**. Select **Yes** at the User Account Control message.

    ![](../media/87.png)

    ![](../media/88.png)

15. On the **Exclusions** page, verify that **C:\\DevProjects** and **DevBuild.exe** are displayed.

    ![](../media/89.png)

16. Close the **Windows Security** page and then close the **Settings** app.

      > **Results**: After completing this exercise, you will have successfully created and assigned a Configuration policy for a Windows 11 device.

## Exercise 2: Modify an assigned Configuration policy   

### Scenario

There was an exception to Contoso's policy that specifies that members of the Developer department should not have the Privacy options blocked in Settings on their devices. This change should be implemented and tested.

### Task 1: Change settings in an assigned Configuration policy

In this task you will modify the existing configuration profile by removing the Privacy restriction from the device settings.

1. Switch to **SEA-SVR1** and use password **Pa55w.rd** to login.

   ![](../media/H2.png)

   ![](../media/p1t1s1.2.png)

2. On **SEA-SVR1**, in the **Microsoft Intune admin center** select **Devices (1)** and then **Configuration**, and on the **Devices | Configuration (2)** blade in the details pane select **Contoso Developer – standard (3)**.

   ![](../media/90.png)

4. On the **Contoso Developer - standard** blade, scroll down to the **Configuration settings** section, and then select **Edit**.

   ![](../media/91.png)

5. On the **Device restrictions** page, expand **Control Panel and Settings**. 

   ![](../media/92.png)

6. Next to **Privacy**, select **Not configured**. 

   ![](../media/93.png)

7. Select **Review + save**, and then select **Save**.

   ![](../media/94.png)

### Task 2: Force device synchronization from the Intune admin center

In this task you will force a policy sync from the Intune admin center so the updated configuration applies to the device quickly.

1. On **SEA-SVR1**, in the Microsoft Intune admin center, select **Devices (1)** in the navigation pane and then select **All devices (2)**. In the details pane, select **SEA-WS1 (3)**.
    
    ![](../media/95.png)
    
3. On the **SEA-WS1** blade, select **Sync (1)** and when prompted select **Yes (2)**. 

   ![](../media/97.png)

   >**Note:** Intune will contact the device and tell it to synchronize all policies. This may take up to 5 minutes._

4. Close Microsoft Edge.

### Task 3: Verify changes on SEA-WS1

In this task you will confirm on SEA-WS1 that the updated configuration has taken effect and that the Privacy settings are visible again.

1. Switch to **HOSTVM** and sign in to **SEA-WS1** VM from desktop shortcurt.

2. On **SEA-WS1** and on the taskbar, select **Start** and then select the **Settings** app.

   ![](../media/98.png)

3. In the **Settings** app, select **Privacy & security** and verify that all of the customization options are back.

4. Close all open windows and sign out of **SEA-WS1**.

    > **Results**: After completing this exercise, you will have successfully modified an assigned a Configuration policy, and verified the changes.

**END OF LAB**
