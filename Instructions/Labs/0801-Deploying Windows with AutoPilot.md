# Practice Lab: Deploying Windows with Autopilot

## Summary

In this lab you will learn how provision a Windows 11 device with Autopilot using User-driven mode.

> **!IMPORTANT**: Once you launch the track, you’ll have access to a virtual machine (VM) for **40 hours**. The displayed track duration of **30 days** indicates the time frame during which you can use your VM. Please plan your lab sessions accordingly. If the VM uptime of **40 hours** is fully exhausted before completing the labs, access will be lost. To avoid this and for detailed instructions on VM usage and stopping/deallocating the VM, refer to the Getting Started page.  

> If the full 40 hours of VM uptime is exhausted, the VM will no longer be accessible, and **the lab duration cannot be extended**.

### Prerequisites

To following lab(s) must be completed before this lab:

- 0101-Managing Identities in Entra ID

- 0102-Synchronizing Identities by using Microsoft Entra Connect

- 0701-Deploying Windows 11 using Microsoft Deployment Toolkit


### Scenario

Contoso IT is planning to roll out a deployment of new Windows 11 devices using Autopilot. The devices have a default installation of Windows 11. Users should be able to connect the device, turn it on, and answer minimal questions during the OOBE, using their Azure AD credentials to sign in. The process should automatically enroll and join the Azure AD domain. You have been asked to configure and test the experience using the SEA-WS4, which you recently installed and configured using Hyper-V.

> **Important**: We cannot use Windows 11 Hyper-V based virtual machines for Autopilot testing (Which we configured in the previous lab, 0701). This is due to a physical Trusted Platform Module (TPM) requirement. In this lab, we will test autopilot using Windows 10, however in the real world you can follow the same process for deploying windows 11 via Autopilot. for more details, see [Troubleshooting Windows Enrollment Issues](https://learn.microsoft.com/en-us/troubleshoot/mem/intune/device-enrollment/troubleshoot-windows-enrollment-errors#securing-your-hardware-failed-0x800705b4).

### Task 1: Create group in Entra ID

In this task you will create a dynamic device group in Entra ID that will automatically contain all devices registered with Windows Autopilot.

1. Sign in to **SEA-SVR1** as **Contoso\\Administrator** with the password **Pa55w.rd** and close **Server Manager**.

     ![](../media/H2.png)

    ![](../media/p1t1s1.2.png)

2. On the taskbar, select **Microsoft Edge**.

3. In Microsoft Edge, in the address bar, type **https://entra.microsoft.com**, and then press **Enter**. If prompted, sign in with your **<inject key="AzureAdUserEmail"></inject>**, and use the tenant Admin password **<inject key="AzureAdUserPassword"></inject>**

4. In the navigation pane expand **Entra ID (1)**, then under **Groups (2)** select **All groups (3)**, and in the **Groups | All groups** blade select **New group (4)**.

    ![](../media/600.png)

7. In the **New Group** blade, in the **Group type** list select **Security (1)**, then in the **Group name** box type **IT Devices (2)**, in the **Group description** box type **IT Department Devices (3)**, in the **Membership type** list select **Dynamic Device (4)**, and select **Add dynamic query (5)**.

    ![](../media/601.png)

12. On the **Dynamic membership rules** blade select **Edit** above the **Rule syntax** box.

    ![](../media/602.png)

13. In the Edit rule syntax text box, add the following simple membership rule and select **OK**.

    ```
    (device.devicePhysicalIDs -any (_ -contains "[ZTDId]"))
    ```

     ![](../media/603.png)

14. Select **Save** to close **Dynamic membership rules**, and then select **Create** to create the group.

    ![](../media/604.png)

    ![](../media/605.png)

### Task 2: Create a virtual machine using Hyper-V

In this task you will create a new Windows 10 virtual machine in Hyper-V that will be used to simulate an Autopilot device.

1. Switch to **HOSTVM**, Click on Hyper-V manager available on the Task bar

1. In Actions click on **New(1)** and Click on **Virtual machine(2)**.

   ![](../media/1051.png)

1. In the before you begin page, click on **Next**.

   ![](media/002.png)

1. In Specify Name and location page, enter the name **SEA-W10-CL3(1)** and click on **Next(2)**.

   ![](media/003.png)

1. In Specify Generation page,  choose **Generation 1(1)** and click on **Next(2)**.

   ![](media/004.png)

1. In Assign Memory enter the size **4096**(1) and enable **Use dynamic memory for this virtual machine(2)** and click on **Next(2)**

   ![](media/005.png)

1. In Configure networking Select the drop down and choose **Internalswitch(1)** and click on **Next(2)**

   ![](media/006.png)

1. In Connect Virtual Hard disks Leave the default settings and click on **Next**

1. In installation options select **Install operating system from bootable CD/DVD ROM(1)**. Under that select **Image file iso(2)**

1. Click on **Browse(3)** and navigate to **D:\Labfiles\ISOs** and select **Win10.iso(4)** and click on **Next(5)**

   ![](media/007.png)

1. Review the settings on summary page and click on **Finish**

## Task 03: Configure Domain for the created virtual machine

In this task you will complete the Windows 10 setup on the VM and join it to the Contoso domain so it can be prepared for Autopilot.

1. Once the **SEA-W10-CL3** VM is created, right click and select **start**.

1. Once it is in the Running state, right click and select **Connect**.

   ![](media/0008.png)

1. You can see the Windows setup wizard.

1. Click on **Next**

    ![](../media/606.png)

1. Click on **Install now**

   ![](media/008.png)

1. Select the checkbox **I Accept the License terms(1)**. and click on **Next(2)**

   ![](media/009.png)

1. On the *Which type of installation do you want* page, choose **Custom:Install Windows Only (advanced)** option

    ![](../media/607.png)

1. On the *Which type of installation do you want* page, select the **Drive 0 unallocated space(1)** and click on **Next(2)** to begin the installation process.

   ![](media/010.png)

   >**Note**: Installation might roughly take upto 15-20 mins. Do Not Press any key until the Windows Logo appears.

1. Once the installation is completed it will ask you to select Region. Select The default one (United States) and select **Yes**

    ![](../media/608.png)

1. Select the Keyboard layout **US**

   ![](media/011.png)

1. Skip Additional keyboard layout.

   ![](media/012.png)

1. When the Wizard asks you to sign in with microsoft. Select **Domain join instead** from the bottom left.

   ![](media/013.png)

1. On *Who is going to use this PC* page, enter **Admin** at the Name text box and click on **Next**.

    ![](../media/609.png)

1. For password and Confirm password, enter **Pa55w.rd** and Select **Next**.

    ![](../media/610.png)

1. On create security questions for this account page, Select any three question of your choice and fill in the answers, then click on next.

1. Click on **Accept** for Choose privacy settings for your device page.

   ![](media/016.png)

1. Click on **Not now** for the Cortana setup.

   ![](media/017.png)

1. The setup will take few minutes to complete.

1. Once completed, the Connect screen pops up from hyper-v click on connect. The system reboots

   ![](media/018.png)

1. Once Rebooted it asks for username and password. Enter **Admin** for username and **Pa55w.rd** for password.

    ![](../media/1052.png)

1. Once logged in to **SEA-W10-CL3** and search and select **Run** from Start menu to open Run command.

    ![](../media/611.png)

1. Type **sysdm.cpl** and press enter which opens System properties.

   ![](media/022.png)
   
1. Click on **Change**.

   ![](media/023.png)

1. When the screen pops-up leave the computer name as default, and under **Member of** select Domain and Type **Contoso.com**, Select Ok

   ![](media/024.png)

1. Windows security screen pops-up Give username as **Administrator** And Password as **Pa55w.rd**. Press enter

   ![](media/025.png)

1. A screen pops-up with Restart request. Select Restart now.

  >**Note**: If the pop-up does not appear, manually restart the system.
   
### Task 4: Generate a device-specific comma-separated value (CSV) file

In this task you will collect the Autopilot hardware information from the VM into a CSV file using PowerShell.

1. In the **SEA-W10-CL3** VM, sign in with **Admin** enter **Pa55w.rd** for password.

2. Right-click **Start (1)**, select **Windows PowerShell (Admin) (2)**, and then select **Yes** at the **User Account Control** prompt.

    ![](../media/612.png)

3. At the Windows PowerShell command-line prompt, type the following cmdlet, and then press **Enter**:

    ```
    Install-Script -Name Get-WindowsAutoPilotInfo
    ```

4. You will receive three prompts. Each time, type **Y**, and then press **Enter**.

    ![](../media/613.png)

5. At the Windows PowerShell command-line prompt, type the following cmdlet, and then press **Enter**:

    ```
    Set-ExecutionPolicy RemoteSigned
    ```

6. When prompted, type **Y**, and then press Enter.

    ![](../media/614.png)

7. At the Windows PowerShell command-line prompt, type the following cmdlet, and then press **Enter**:

    ```
    Get-WindowsAutoPilotInfo.ps1 -OutputFile C:\Computer.csv
    ```

8. At the Windows PowerShell command-line prompt, type the following command, press **Enter**, and then review the file content:

    ```
    type C:\Computer.csv
    ```

9. Close out of **Windows Powershell**.

### Task 5: Work with a Windows Autopilot deployment profile

In this task you will import the device’s Autopilot CSV into Intune and create a Windows Autopilot deployment profile in user-driven mode, assigning it to the IT Devices group.

1. On **SEA-W10-CL3**, in the windows taskbar, select **Microsoft Edge**.

2. In **Microsoft Edge**, navigate to **https://intune.microsoft.com**. Sign in with your  **<inject key="AzureAdUserEmail"></inject>** account.

    >Note: If prompted to register for MFA. Follow the same procedures you used earlier in the course to add your phone number.

4. In the **Microsoft Intune admin center** select **Devices (1)**, then in the **Device onboarding** section select **Enrollment (2)**, and in the **Windows** tab scroll down to **Windows Autopilot (3)** and select **Devices (4)**.

    ![](../media/615.png)

6. In the **Windows Autopilot devices** blade on the menu bar, select **Import**, select the **folder icon (1)** and then browse to **C:\\ (2)**, select **Computer.csv (3)**, select **Open (4)**, and then select **Import**. 

    ![](../media/616.png)

    ![](../media/617.png)

    ![](../media/618.png)

   _Note: The import process can take up to 15 minutes, but normally takes around 5 minutes._  

   _**Important**: After the process is complete, the device may not show automatically. If this is the case, select the **Refresh** button. If the device still does not appear, select the **Sync** button, wait a few minutes, and then select **Refresh**._

7. Select **X** to close the **Windows Autopilot devices** blade. 

8. On the Windows **Enrollment (1)** blade, in the details pane, select **Deployment Profiles (2)**.

    ![](../media/619.png)

9. On the **Windows AutoPilot deployment profiles** blade, select **Create profile (1)** and then select **Windows PC (2)**.

    ![](../media/620.png)

10. In the **Basics** tab, in the **Name** text box, type **Contoso profile1**. For **Convert all targeted devices to Autopilot** select **No**, and then select **Next**.

    ![](../media/621.png)

12. On the **Out-of-box experience (OOBE)** tab, ensure that the **Deployment mode** is set to **User-Driven (1)**.

13. Ensure that **Join to Microsoft Entra ID as** is set to **Microsoft Entra Joined (2)**.

14. Ensure that the following options are set:

    - Microsoft Software License Terms: **Hide (3)**

    - Privacy Settings: **Hide (4)**

    - Hide change account options: **Hide (5)**

    - User account type: **Administrator (6)**.

    - Allow pre-provisioned deployment: **No (7)**

    - Language (Region): **Operating system default (8)**

    - Automatically configure keyboard: **Yes (9)**

    - Apply device name template: **No (10)**

    - Select **Next (11)**

         ![](../media/622.png)

16. On the **Assignments** tab, under **Included groups** select **Add groups**.

    ![](../media/623.png)

17. Select the **IT Devices (1)** group and click **Select (2)**. Select **Next**.

    ![](../media/624.png)

18. On the **Review + create** blade, review the information and then select **Create**.

    ![](../media/625.png)

19. Close out of **Microsoft Edge**

### Task 6: Reset the PC

In this task you will reset the Windows 10 VM to simulate a brand-new device and trigger the Autopilot out-of-box experience.

1. On **SEA-W10-CL3**, select **Start**, type **reset** and select **Reset this PC**.

    ![](../media/626.png)

2. In the **Reset this PC** section, select **Get started**.

    ![](../media/627.png)

3. Select **Remove everything**, and then select **Local reinstall**.

   ![](../media/628.png)

   ![](../media/1053.png)

4. Select **Next** on Additional settings page and then select **Reset**.

    ![](../media/1054.png)

    ![](../media/1054.png)

    **>Note:** Normally this task is not required for new deployment of physical devices. The device’s autopilot info is either provided by the manufacturer or can be obtained from the device prior to the OOBE. For the purposes of this lab, we must initiate a reset to simulate a new device OOBE.

    >**Note**: This process can take 30-60 minutes and will reboot several times during the process.

### Task 7: Verify Autopilot deployment

In this task you will sign in to the reset device as Aaron, complete the Autopilot setup, verify the device is Entra joined and managed, and confirm its Autopilot status in the Entra admin center.

>**Note** : Before proceeding with the next step, ensure that you are in basic session mode and able to view Clipboard in the menu bar as shown in the below image. If not please change it to the basic session by selecting the icon which was highlighted in the tool bar in the below image.

   ![](../media/passwordwriteback1.png)

1. At the **Contoso Corp. Sign-in Page**, enter **`Aaron@yourtenant.onmicrosoft.com` (1)** and select **Next (2)**.

   ![](../media/629.png)

   >**Note**: Replace **yourtenant** with the tenant name provided to you.

2. At the Password page, enter **Pa55w.rd1234!** and select **Next**.

    ![](../media/630.png)

3. At the **Use Windows Hello with your account**, select **OK**.

    ![](../media/631.png)

4. At the **Verify your identity** page, select the Text verification method.

    ![](../media/632.png)

5. At the **Enter code** page, enter the code that has been texted to your mobile device and then select **Verify**.

    ![](../media/633.png)

6. On the **Setup up a PIN** dialog box, in the **New PIN (1)** and **Confirm PIN (2)** fields, enter **102938**, and then select **OK (3)**.

    ![](../media/634.png)

7. On the **All set!** page, select **OK**.

    ![](../media/1056.png)

8. Select **Start** and select **Settings**. 

9. Select **Accounts**, and then select **Access work or school**. Verify the device is connected to Contoso's Azure AD.

    ![](../media/635.png)

10. Select **Connected to Contoso's Azure AD** and select **Info**.

    ![](../media/636.png)

11. On the **Managed by Contoso** page, scroll down and then select **Sync**.

    ![](../media/637.png)

12. On **SEA-W10-CL3**, close the **Settings** window.

13. Switch to **SEA-SVR1**.

14. In the Microsoft Entra admin center, select **Identity**, select **Devices** and then select **All devices**. 

    ![](../media/638.png)

    > Note that the new device displays with an icon that indicates an Autopilot device. Also note that the Join Type is **Microsoft Entra joined** with Aaron Nicholls as the owner.

15. Select the Autopilot device and then select **Manage**. 

    ![](../media/639.png)

16. Again select the Autopilot device to review the management page. 

17. Notice that you can Retire, Wipe, Sync, and Restart the device.

    ![](../media/640.png)

18. Select the ellipsis at the end of the menu bar and take notice of the additional management capabilities.

    ![](../media/641.png)

    > **Note**: Additional capabilities include Fresh Start, Autopilot Reset, Quick scan, Full scan, as well as others.

18. Close Microsoft Edge.

**Results**: After completing this exercise, you will have provisioned a Windows device with Autopilot using User-driven mode.

**END OF LAB**
