# Practice Lab: Synchronizing Identities by using Microsoft Entra Connect 

## Summary

In this lab, you will configure synchronization from Active Directory Domain Services to Microsoft Entra ID.

### Scenario

Contoso Corporation is currently managing users in both AD DS and Entra ID as separate processes. This is time consuming and has led to inconsistent information. You have been tasked with addressing this issue by connecting the two directories by using the Microsoft Entra Connect synchronization tool.

#### Task 1: Configure directory synchronization with Microsoft Entra Connect

In this task, you will install and configure Microsoft Entra Connect on the server to synchronize your on-premises Active Directory users and groups with Microsoft Entra ID.

1. On **SEA-SVR1** from top left dropdown, if necessary, sign in as **Contoso\\Administrator** with the password of **Pa55w.rd** and close **Server Manager**.

    ![](../media/H2.png)

    > **Note :** If you’re unable to switch the VM from the dropdown menu, you can also access the VM directly from the desktop of your Host VM.

    ![](../media/1.png)

    ![](../media/p2t1s1.2.png)

2. On the **taskbar**, select **Microsoft Edge**.

    ![](../media/p2t1s2.png)

3. In the address bar, enter `https://entra.microsoft.com`

    ![](../media/p2t1s3.png)

4. In the left navigation pane, under **Entra ID**, select **Entra Connect (1)**. On the **Microsoft Entra Connect | Get started (2)** pane, select the **Manage (3)** tab.

    ![](../media/p2t1s4.2.png)

6. In the **Manage your infrastructure** page, select **Download Connect Sync Agent**.

    ![](../media/p2t1s4.1.png)

7. Select **Accept terms & download**. 

    ![](../media/p2t1s4.3.png)

    >**Note**: Entra Connect automatically downloads to the **Downloads** folder on SEA-SVR1.

8. Select **Open downloads folder** and then in the **Downloads** window, double-click **AzureAdConnect.msi**.

    ![](../media/p2t1s4.4.png)

    ![](../media/p2t1s5.png)

6. In the **Microsoft Entra Connect Sync** wizard, on the **Welcome to Microsoft Entra Connect Sync** page, select the **I agree to the license terms and privacy notice (1)** check box, and then select **Continue (2)**.

    ![](../media/p2t1s6.png)

7. On the **Express Settings** page, select **Customize**.

    ![](../media/p2t1s7.png)

8. On the **Install required components** page, select **Install**.

    ![](../media/p2t1s8.png)

9. On the **User sign-in (1)** page, ensure that **Password Hash Synchronization (2)** is selected, and then select **Next (3)**.

    ![](../media/p2t1s9.png)

10. On the **Connect to Microsoft Entra ID** page, in the **USERNAME** boxes, enter **<inject key="AzureAdUserEmail"></inject>**, and then select **Next**.

    ![](../media/p2t1s10.png)

11. In the **Sign in to your account** window, enter **<inject key="AzureAdUserEmail"></inject>**, select **Next**, then enter your tenant password **<inject key="AzureAdUserPassword"></inject>** and select **Sign in**.

    ![](../media/p2t1s11.1.png)

12. On the **Connect your directories** page, ensure that **Contoso.com** is listed under **FOREST**, and then select **Add Directory**.

    ![](../media/p2t1s12.png)

    ![](../media/p2ts13.2.png)

13. In the **AD forest account** window, select the **Create New AD Account (1)** option, and in the **ENTERPRISE ADMIN USERNAME** field, type **Contoso\\Administrator (2)**, and then type **Pa55w.rd** in the **PASSWORD (3)** field. Select **OK (4)**, and then select **Next**.

    ![](../media/p2t1s13.png)

14. On the **Microsoft Entra sign-in configuration** page, ensure that in the **USER PRINCIPAL NAME** drop-down list, the **userPrincipalName (1)** value is selected. Select **Continue without matching all UPN suffixes to verified domains (2)** and then select **Next (3)**.

    ![](../media/p2t1s15.png)

16. On the **Domain and OU filtering** page, select **Sync selected domains and OUs**.

17. Expand **Contoso.com**, clear the checkbox next to **Contoso.com** and ensure that the only following check boxes are selected: **IT**, **Managers**, **Marketing**, **Research**, and **Sales**. Select **Next**.

    ![](../media/p2t1s17.png)

18. On the **Uniquely identifying your users** page, select **Next**.

    ![](../media/p2t1s18.png)

19. On the **Filter users and devices** page, select **Next**.

    ![](../media/p2t1s19.png)

20. On the **Optional features** page, review available options, but do not make any changes. Ensure that **Password hash synchronization** is selected, and then select **Next**.

    ![](../media/p2t1s20.png)

21. On the **Ready to configure** page, ensure that **Start the synchronization process when configuration completes** is selected, and then select **Install**.

    ![](../media/p2t1s21.png)

22. When configuration is complete, select **Exit**.

    ![](../media/p2t1s22.png)

      > Note: At this time, synchronization of objects from your local Active Directory Domain Services (AD DS) and Azure AD begins. You should wait approximately 3-4 minutes for this process to complete.

23. Close all open windows.

### Task 2: Verify synchronization in Entra ID

In this task, you will verify that the synchronization worked by checking the synced users and groups in the Entra admin center.

1. On the taskbar, select **Microsoft Edge** in the address bar, enter **https://entra.microsoft.com**.

3. At the Sign-in prompt, enter **<inject key="AzureAdUserEmail"></inject>** and then select **Next**.

    ![](../media/p2t2s3.png)

4. At the Enter password page, enter the password for the Admin account as **<inject key="AzureAdUserPassword"></inject>** and then select **Sign in**. 

   > Note: Check with your instructor on the password to use for signing in with the Admin account.

5. At the Save password prompt, select **Save**.

6. At the Stay signed in prompt, select **No**. The Entra admin center opens.

7. In the Microsoft Entra admin center, in the navigation pane, select **Users** > **All users**.

8. Verify that you see users from your local AD DS. Ensure that these users have the value **Yes** in the **On-premises sync enabled** column. 

    ![](../media/p2t2s8.png)

9. In the Navigation pane, under **Identity**, select **Groups** > **All groups**. Verify that you see groups from your local AD DS. Ensure that these groups have the value **Windows Server AD** in the **Source** column.

    ![](../media/p2t2s10.png)

10. Select the **Managers** group.

11. On the **Managers** group page, select **Members** and then ensure that you see users.

    ![](../media/p2t2s11.3.png)

    > Note that you cannot add to or remove members from this group, as it is sourced from the local AD DS. 

12. Close Microsoft Edge.

**Results**: After completing this exercise, you will have successfully configured Microsoft Entra Connect to synchronize identity from Active Directory Domain Services to Entra ID.

**END OF LAB**
