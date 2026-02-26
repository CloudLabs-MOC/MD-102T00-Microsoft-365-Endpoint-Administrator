# Practice Lab: Configuring Self-service password reset for user accounts in Entra ID

## Summary

In this lab, you will configure and validate self-service password reset (SSPR) for user accounts in Azure Active Directory.

### Prerequisites

To following lab(s) must be completed before this lab:

- 0102-Synchronizing Identities by using Microsoft Entra Connect
- 0203-Manage Device Enrollment into Intune


### Scenario

The Help Desk has indicated that a large number of support tickets are related to password resets. You have been asked to propose a solution for users to reset their own password. For accounts that are synchronized from AD DS, the process should reset both their Azure AD and AD DS password. 

### Task 1: Configure password writeback

In this task you will enable password writeback in Azure AD Connect so that password resets made in Azure AD can update the on-premises AD DS password.

1. Sign in to **SEA-SVR1** as **Contoso\\Administrator** with the password **Pa55w.rd** and close **Server Manager**.

2. On the desktop, double-click **Azure AD Connect**.

    ![](../media/301.png)

3. On the **Welcome to Microsoft Entra Connect Sync** page, select **Configure**.

    ![](../media/302.png)

4. On the **Additional tasks** page, select **Customize synchronization options (1)**, and then select **Next (2)**.

    ![](../media/303.png)

5. On the **Connect to Microsoft Entra ID** page, if needed type **<inject key="AzureAdUserEmail"></inject>** in the **USERNAME (1)** text box, then select **Next (2)**.

    ![](../media/304.png)

6. On the **Sign in to your account** dialog, select your **<inject key="AzureAdUserEmail"></inject>** account and enter your Admin tenant password **<inject key="AzureAdUserPassword"></inject>**, and then select **Sign in**.

    ![](../media/305.png)

6. On the **Connect your directories** page, select **Next**.

    ![](../media/306.png)

7. On the **Domain and OU filtering** page, select **Next**.

    ![](../media/307.png)

8. On the **Optional features** page, select **Password writeback (1)**, and then select **Next (2)**.

    ![](../media/308.png)

9. On the **Ready to configure** page, select **Configure**.

    ![](../media/310.png)

10. On the **Configuration complete** page, select **Exit**.

    ![](../media/311.png)

### Task 2: Enable self-service password reset

In this task you will enable self-service password reset for all users and configure authentication methods and security questions in the Entra admin center.

1. On **SEA-SVR1**, on the taskbar select **Microsoft Edge**, in the address bar type **https://entra.microsoft.com/**, and then press **Enter**.

    ![](../media/312.png)

2. Sign in as  **<inject key="AzureAdUserEmail"></inject>**, and use the tenant Admin password **<inject key="AzureAdUserPassword"></inject>**, If the **Stay signed in?** prompt appears, select **No**.  

   > The Microsoft Entra admin center opens.

1. In the navigation pane, under **Entra ID (1)**, select **Authentication methods (2)**. 

    ![](../media/313.png)

1. Ensure that **SMS (1)** and **Email OTP (2)** show **Yes** in the **Enabled** \(third\) column. 

    ![](../media/314.png)

1. In the Microsoft Entra admin center, in the navigation pane, under **Entra ID**, select **Password reset (1)**. In the **Password reset | Properties (2)** window, select **All (3)** to enable self-service password reset to all users. Select **Save (4)**.

    ![](../media/315.png)

1. In the **Password reset | Properties** window select **Authentication methods (1)** and then **Security questions (2)**, then for the **Number of questions required to register (3)** select **3**, for the **Number of questions required to reset (4)** select **3**, and in the **Select security questions** section select **No security questions configured (5)**, then select **Predefined**, choose any three questions, and select **OK**.

    ![](../media/316.png)

    ![](../media/317.png)

    ![](../media/318.png)

    ![](../media/319.png)


1. Select **Save**.

    ![](../media/320.png)

1. Select **Registration** Select **No (1)** for **Require users to register when signing in**, and then select **Save (2)**.

    ![](../media/1021.png)

1. In the navigation pane, select **On-premises integration**.

1. Verify that your on-premises writeback client is running.

    ![](../media/322.png)

1. Close Microsoft Edge.

### Task 3: Validate self-service password reset

In this task you will sign in as a user and verify that they can successfully change their password using the self-service password reset options.

1. Switch to **SEA-WS3**.

2. If necessary, sign in as **Admin** with the password of **Pa55w.rd**.

    ![](../media/323.png)

3. On the taskbar, select **Microsoft Edge**.

4. Browse to **https://myaccount.microsoft.com**. 

    ![](../media/324.png)

5. On the **Pick an account** page, select **Use another account**.

    ![](../media/325.png)

6. On the **Sign in** page, enter **`Aaron@yourtenant.onmicrosoft.com`** and then select **Next**.

    ![](../media/326.png)

7. On the **Enter password** page, enter **Pa55w.rd** and then select **Sign in**. If the Microsoft Edge prompts to save the password, select **Save**.

    ![](../media/327.png)

8. On the **My Account** page, in the navigation pane, select **Password**.

9. On the **Change your password** page, enter the following information and then select **submit**:

     - New password: **Pa55w.rd1234!**
     - Confirm new password: **Pa55w.rd1234!**

       ![](../media/330.png)

10. If Microsoft Edge prompts to save the password, select **Save**.

11. Close Microsoft Edge and sign out of SEA-WS3.

### Task 4: Run AD Sync

In this task you will manually trigger an Azure AD Connect sync cycle to ensure password changes are fully synchronized in the lab environment.

*Note that this step is normally not necessary for password writeback, but is recommended to address issues inherent in lab environments and ensure AD DS is synchronized with Azure AD.*

1. Switch to **SEA-SVR1**.

2. Right-click **Start (1)** and then select **Windows PowerShell (Admin) (2)**.

    ![](../media/332.png)

3. At the **Windows PowerShell** command prompt, type the following command, and
    then press **Enter**:

    ```
    Start-ADSyncSyncCycle –PolicyType Delta
    ```

    ![](../media/1022.png)

4. Close Windows PowerShell, and then wait for approximately 3-4 minutes.

### Task 5: Verify password writeback

In this task you will verify password writeback by signing in to an on-premises computer using the newly updated password.

1. Switch to **HOSTVM** and sign in to **SEA-CL1**.

   >**Note** : If you are unable to sign in to SEA-CL1, then turnoff the **SEA-CL2** Hyper-V VM which is not being used in this lab from the HyperV-Manager which is available in the HOSTVM and then start the **SEA-CL1** VM.

   ![](./media/md612.png)

   ![](./media/md613.png)

   >**Note** : Before proceeding with the next step, ensure that you are in basic session mode and able to view Clipboard in the menu bar as shown in the below image. If not please change it to the basic session by selecting the icon which was highlighted in the tool bar in the below image.

   ![](../media/passwordwriteback.png)

2. On **SEA-CL1**, select **Other user**, and then attempt to sign in as **Contoso\\Aaron** with the password of **Pa55w.rd**.

    ![](../media/333.png)

    ![](../media/334.png)

3. Ensure that you get the message that the user name or password is incorrect.

    ![](../media/335.png)

4. Sign in to **SEA-CL1** as **Contoso\Aaron** with the password **Pa55w.rd1234!**. 

   > You should be able to sign in. This confirms that the password you changed in the Azure portal is written back to the local Active Directory Domain Services (AD DS) account.

5. Sign out of **SEA-CL1**.

**Results**: After completing this exercise, you will have successfully configured and validated self-service password reset.

**END OF LAB**
