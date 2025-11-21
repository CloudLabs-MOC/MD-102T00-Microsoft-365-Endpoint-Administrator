# Practice Lab: Refreshing Windows with Autopilot Reset and Self-Deploying mode

## Summary

In this lab you will learn how perform a remote Autopilot reset.

### Prerequisites

To following lab(s) must be completed before this lab:

- 0101-Managing Identities in Entra ID

- 0102-Synchronizing Identities by using Microsoft Entra Connect

- 0701-Deploying Windows 11 using Microsoft Deployment Toolkit

- 0801-Deploying Windows 11 with Autopilot


### Scenario

SEA-WS4 has been deployed by using Windows Autopilot. You need to test out another provisioning scenario that involves Autopilot Reset. You will create a new deployment profile configured with the Windows Autopilot Self-Deploying mode.

### Task 1: Configure a  Self-Deploying Windows Autopilot deployment profile

In this task you will create a new Autopilot deployment profile configured for Self-Deploying mode and assign it to the IT Devices group.

1. Switch to **SEA-SVR1**.

2. In **Microsoft Edge**, open a new tab and navigate to **https://intune.microsoft.com**. If prompted, sign in with your **<inject key="AzureAdUserEmail"></inject>**.

3. In the **Microsoft Intune admin center** select **Devices (1)**, then in the **Device onboarding** section select **Enrollment (2)**, and on the **Windows enrollment** tab scroll down to **Windows Autopilot** in the details pane and select **Deployment Profiles (3)**.

    ![](../media/643.png)

6. On the **Windows AutoPilot deployment profiles** blade, select **Contoso Profile 1** and then select **Properties**.

    ![](../media/644.png)

7. Scroll down to **Assignments** and then select **Edit (1)**.

    ![](../media/645.png)

8. Next to **IT Devices**, select **Remove**.

    ![](../media/646.png)

9. Select **Review and save** and then select **Save**.

    ![](../media/647.png)

    ![](../media/648.png)

10. Close the **Contoso Profile 1|Properties** page.

11. On the **Windows AutoPilot deployment profiles** blade, select **Create profile (1)** and then select **Windows PC (2)**.

    ![](../media/649.png)

12. In the **Basics** tab, in the **Name** text box, type **Contoso profile 2 (1)**. For **Convert all targeted devices to Autopilot** select **No (2)**, and then select **Next (3)**.

    ![](../media/650.png)

14. On the **Out-of-box experience (OOBE)** tab, ensure that the **Deployment mode** is set to **Self-Deploying**.

    ![](../media/651.png)

15. Ensure that the following options are set:

   - Language (Region): **Operating system default**
   - Automatically configure keyboard: **Yes**
   - Apply device name template: **Yes**
   - Enter a name: **Contoso-%RAND:2%**

16. Select **Next**.

17. On the **Assignments** tab, under **Included groups** select **Add groups**.

    ![](../media/652.png)

18. Select the **IT Devices** group and click **Select**. Select **Next**.

    ![](../media/653.png)

19. On the **Review + create** blade, review the information and then select **Create**.

    ![](../media/654.png)

### Task 2: Perform an Autopilot reset

In this task you will remotely trigger an Autopilot Reset on the Autopilot-registered device from Intune.

1. In the **Microsoft Intune admin center**, select **Devices (1)** and then select **All devices (2)**. Select the Autopilot PC (Begins with the name DESKTOP).

    ![](../media/655.png)

3. In the menu bar, select the ellipsis and then select **Autopilot Reset**.

    ![](../media/656.png)

5. At the message prompt, select **Yes**.

    ![](../media/657.png)

6. Switch to **HOSTVM** and sign in to **SEA-W10-CL3**.

   > Note: SEA-W10-CL3 should still be running from the previous lab.

7. Restart **SEA-W10-CL3**.

   >**Note**: This process can take 30-45 minutes and will reboot several times during the process. 

   >**Note**: If the reset process does not begin after a restart, please sign in, manually sync the device with Intune, and then restart **SEA-W10-CL3**.

### Task 3: Verify Autopilot deployment

In this task you will complete the Autopilot setup after the reset and verify that the device is joined to Entra ID and managed by Intune.

   >**Note** : Before proceeding with the next step, ensure that you are in basic session mode and able to view Clipboard in the menu bar as shown in the below image. If not please change it to the basic session by selecting the icon which was highlighted in the tool bar in the below image.

   ![](../media/passwordwriteback1.png)

1. At the sign-in page, enter **`Aaron@yourtenant.onmicrosoft.com`** with the Password of **Pa55w.rd1234!**.

    ![](../media/659.png)

    >**Note**: Replace **yourtenant** with the tenant name provided to you 

2. At the **Use Windows Hello with your account**, select **OK**.

    ![](../media/660.png)

3. At the **Verify your identity** page, select the Text verification method.

    ![](../media/661.png)

4. At the **Enter code** page, enter the code that has been texted to your mobile device and then select **Verify**.

    ![](../media/662.png)

5. On the **Setup up a PIN** dialog box, in the **New PIN** and **Confirm PIN** fields, enter **102938**, and then select **OK**.

    ![](../media/663.png)

6. On the **All set!** page, select **OK**.

    ![](../media/654.png)

7. Select **Start** and select **Settings**. 

8. Select **Accounts**, and then select **Access work or school**. Verify the device is connected to Contoso's Azure AD. Select **Connected to Contoso's Azure AD** and select **Info**.

    ![](../media/665.png)

    ![](../media/666.png)

10. On the **Managed by Contoso** page, scroll down and then select **Sync**.

    ![](../media/667.png)

11. On **SEA-W10-CL3**, close the **Settings** window.

    **Results**: After completing this exercise, you will have provisioned a Windows device with Autopilot Reset using Self-Deploying mode.

**END OF LAB**
