# Practice Lab: Managing Identities in Entra ID

## WWL Tenants - Terms of Use

If you are being provided with a tenant as a part of an instructor-led training delivery, please note that the tenant is made available for the purpose of supporting the hands-on labs in the instructor-led training. 

Tenants should not be shared or used for purposes outside of hands-on labs. The tenant used in this course is a trial tenant and cannot be used or accessed after the class is over and are not eligible for extension. 

Tenants must not be converted to a paid subscription. Tenants obtained as a part of this course remain the property of Microsoft Corporation and we reserve the right to obtain access and repossess at any time.

## Summary

In this lab, you will use the Entra ID admin center to create and modify users, assign administrative roles, create and modify groups, and manage license assignments in Entra ID.

## Exercise 1: Creating users in Entra ID

### Scenario

You need to create user accounts in Entra ID for new employees that will start next week. New users are listed in the following table:

| Name           | User Name                             | Password   | Job title         | Department |
| -------------- | ------------------------------------- | ---------- | ----------------- | ---------- |
| Edmund Reeve   | `ereeve@yourtenant.onmicrosoft.com`   | Pa55-w.rd! | HR Rep            | HR         |
| Miranda Snider | `msnider@yourtenant.onmicrosoft.com`  | Pa55-w.rd! | Helpdesk Manager  | Operations |
| Allan Deyoung  | `AllanD@yourtenant.onmicrosoft.com`   | Pa55-w.rd! | Accountant        | Accounting |
| Joni Sherman   | `JoniS@yourtenant.onmicrosoft.com`    | Pa55-w.rd! | Marketing Head    | Marketing  |
| Alex Wilber    | `AlexW@yourtenant.onmicrosoft.com`    | Pa55-w.rd! | Support Executive | Support    |
| Cody Godinez   | `cgodinez@yourtenant.onmicrosoft.com` | Pa55-w.rd! | Sales Rep         | Sales      |

_Note: For location use either your local region or United States._

You've also been told that several more employees will be hired over the next couple of months. You've decided that scripting would be a far more efficient method of adding a large number of new users. You've decided to create a PowerShell script and test it out when you create Cody, Allan, Joni and Alex accounts.

### Task 1: Create users by using the Microsoft Entra admin center

1. Switch to **SEA-SVR1**, sign in as **Contoso\\Administrator** with the password of **Pa55w.rd**.

2. Close **Server Manager**.

3. On the taskbar, select **Microsoft Edge**.

4. In the address bar, enter **<https://entra.microsoft.com>**.

5. At the Sign-in prompt, enter **<inject key="AzureAdUserEmail"></inject>** and then select **Next**.

6. At the Enter password page, enter the password for the Admin account as **<inject key="AzureAdUserPassword"></inject>** and then select **Sign in**.

7. At the Save password prompt, select **Save & Turn on**.

8. At the Stay signed in prompt, select **No**. The Entra admin center opens.

   >**Note**: If the prompt asks for **Action Required** Select **Ask later**.

12. In the Microsoft Entra admin center, in the left navigation pane, under **Identity** click on  **Users** and select **All users**.

    > Take note of the users that already exist as members of the Azure AD domain. The **On-premises sync enabled** column states **No** for all current users. This indicates that each user was created directly in Azure AD and not synchronized from an on-premises directory service.

13. On the **Users | All users** page, select **+ New user** then select **Create new user**.

14. On the **Create new user** page, enter the following:

    - User Principal Name: **`ereeve`**
    - Display Name: **Edmund Reeve**

15. Uncheck **Auto-generated password**

16. Next to **Password**, enter **Pa55-w.rd!**

17. Select **Next:Properties** located at the bottom of the page.

18. Next to **First name**, enter **Edmund**.

19. Next to **Last name**, enter **Reeve**.

20. Next to **User type**, make note that **Member** is selected.
    > Note: The **Member** user type is the default user type. This user type is used for most users in an organization.

21. Next to **Job title**, enter **HR Rep**.

22. Next to **Department**, enter **HR**.

23. Under **Settings**, next to **Usage location**, select **United States**.

24. Select **Next:Assignments** located at the bottom of the page.

25. On the **Assignments** page, note that no assignments are selected.
    > by default no groups are assigned to the user. This is because the user is not a member of any groups until you assign them.

26. Select **Next:Review + create** located at the bottom of the page.
    > Review the information on this page to ensure that it is correct.

27. Select **Create**.

28. On the **Users | All users** page, select **New user** then select **Create new user**.

29. On the **Create new user** page, enter the following:

    - User Principal Name: **`msnider`**
    - Display Name: **Miranda Snider**

30. Uncheck **Auto-generated password**

31. Next to **Password**, enter **Pa55-w.rd!**

32. Select **Next:Properties** located at the bottom of the page.

33. Next to **First name**, enter **Miranda**.

34. Next to **Last name**, enter **Snider**.

35. Next to **User type**, make note that **Member** is selected.

36. Next to **Job title**, enter **Helpdesk Manager**.

37. Next to **Department**, enter **Operations**.

38. Next to **Usage location**, select **United States**.

39. Select **Next:Assignments** located at the bottom of the page.

40. On the **Assignments** page, note that no assignments are selected.

41. Select **Next:Review + create** located at the bottom of the page.

42. Select **Create**.

43. Minimize the **Microsoft Edge** window.

### Task 2: Disable the security defaults (Only if it set to Enabled)

1. Navigate to: **Identity > Overview > Properties** in the Microsoft entra admin center.

2. Select: **Manage security defaults**.

3. On the **Security defaults** side screen, if Security defaults are enabled, set them to **Disabled**.

4. From the drop-down list, select **My organization is using Conditional Access**.
Select **Save**.

5. A pop-up will appear to confirm disabling Security defaults. Select **Disable**.

### Task 3: Create users by using Powershell

1. On **SEA-SVR1**, click into the **Windows Search** bar and then type **PWSH**. Right click on **PowerShell 7** and then select **Run as Administrator**.

2. In the **PowerShell 7** window, type the following command, and then press **Enter**. If prompted, enter **Y** at the NuGet and repository messages:

    ```
    Install-Module Microsoft.Graph -Scope CurrentUser
    ```

3. In the **PowerShell 7** window, type the following command, and then press **Enter**:

    ```
    Connect-MgGraph -scopes "user.readwrite.all, group.readwrite.all"
    ```

4. A new tab in **Microsoft Edge** will appear prompting you to sign in. In the **Sign in to your account** dialog box, sign in as **<inject key="AzureAdUserEmail"></inject>** with the tenant password, and then select **Sign in**.
   > **Note** - If the account already exists then click on it.

6. On the **Permissions Requested** prompt that appears, check **Consent on behalf of your organization** and then select **Accept**.

7. Close out of the **Authentication complete** tab and then minimize **Microsoft Edge**

8. Back In the **PowerShell 7** window, type the following code to create a new profile object, and then press **enter**. Replace **Pa55-w.rd!** with a complex password of your choice:

   >**Note**: Copy paste the Commands on notepad before pasting it in the powershell to avoid mistakes.

    ```
    $PWProfile = @{
      Password = "Pa55-w.rd!";
      ForceChangePasswordNextSignIn = $false
    }
    ```

9. Next, type the following code to create a new user, and then press **Enter**. Be sure to replace **yourtenant** with your assigned tenant name:

    ```
    New-MgUser `
        -DisplayName "Cody Godinez" `
        -GivenName "Code" -Surname "Godinez" `
        -MailNickname "cgodinez" `
        -UsageLocation "US" `
        -UserPrincipalName "cgodinez@yourtenant.onmicrosoft.com" `
        -PasswordProfile $PWProfile -AccountEnabled `
        -Department "Sales" -JobTitle "Sales Rep"
    ```

    ```
    New-MgUser `
        -DisplayName "Allan Deyoung" `
        -GivenName "Allan" -Surname "Deyoung" `
        -MailNickname "alland" `
        -UsageLocation "US" `
        -UserPrincipalName "AllanD@yourtenant.onmicrosoft.com" `
        -PasswordProfile $PWProfile -AccountEnabled `
        -Department "Accounting" -JobTitle "Accountant"
    ```

    ```
    New-MgUser `
        -DisplayName "Joni Sherman" `
        -GivenName "Joni" -Surname "Sherman" `
        -MailNickname "jonis" `
        -UsageLocation "US" `
        -UserPrincipalName "JoniS@yourtenant.onmicrosoft.com" `
        -PasswordProfile $PWProfile -AccountEnabled `
        -Department "Marketing" -JobTitle "Marketing head"
    ```

    ```
    New-MgUser `
        -DisplayName "Alex Wilber" `
        -GivenName "Alex" -Surname "Wilber" `
        -MailNickname "alexw" `
        -UsageLocation "US" `
        -UserPrincipalName "AlexW@yourtenant.onmicrosoft.com" `
        -PasswordProfile $PWProfile -AccountEnabled `
        -Department "Support" -JobTitle "Support Executive"
    ```    
   
10. To confirm that the users was created, In the **PowerShell 7** window, type the following command and then press **Enter**:

    ```
    Get-MgUser
    ```

> Verify that the list of users from your tenant is displayed. Also take note of which users have a license assigned. Any user with the **isLicensed** value of **False** has not been assigned a license.

**Results**: After completing this exercise, you will have successfully created new user accounts in Azure AD.

## Exercise 2: Assigning Administrative Roles in Entra ID

### Scenario

You need to review and modify the current administrative roles for your tenant.

You have been provided a list of users should have administrative roles assigned as indicated in the following table.  

| Name           | Must be able to:                         | Administrative Role needed: |
| -------------- | ---------------------------------------- | --------------------------- |
| Allan Deyoung  | Manage the tenant                        | Global administrator        |
| Edmund Reeve   | Manage users, group, and password resets | User administrator          |
| Miranda Snider | Manage password resets                   | Helpdesk administrator      |

### Task 1: Review and Assign Administrative Roles

1. On SEA-SVR1, switch to Microsoft Edge.

2. In the **Microsoft Entra admin center**, in the Navigation pane, expand **Identity** click on Show more Select **Roles & admins**.

3. In all roles tab, using the search box, search for **Global administrator**.

4. Select **Global administrator**.

6. In the **Assignments** pane, select **Add assignments** and select **Allan Deyoung**

7. Select **Add**. go back to the role assignment section by clicking on the cancel **X** on top right side.

8. Using the search box, search for **User administrator**.

9. to the role assignment section by clicking on the cancel **X** on top right side.

10. Using the search box, search for **User administrator**.

11. Select **User administrator**.

12. In the **User administrator** pane, select **Add assignments**.

13. In the **Add assignments** pane, search for and select **Edmund Reeve**.

14. Select **Add**.

15. In the navigation breadcrumbs, select **Roles & administrators | All roles**.

16. Using the search box, search for **Helpdesk administrator**.

17. Select **Helpdesk administrator**.

18. In the **Helpdesk administrator** pane, select **Add assignments**.

19. In the **Add assignments** pane, search for and select **Miranda Snider**.

20. Select **Add**.

21. In the navigation pane, select **Home**.

**Results**: After completing this exercise, you should have successfully assigned administrative roles to users.

## Exercise 3: Creating and managing groups and validating license assignment

### Scenario

You need to add the three new users to a Security group and assign licenses as indicated in the following table.  

| Name           | Member of:       | License to assign                                            |
| -------------- | ---------------- | ------------------------------------------------------------ |
| Edmund Reeve   | Contoso_Managers | Office 365 E5, Enterprise Mobility + Security E5 via group membership |
| Miranda Snider | Contoso_Managers | Office 365 E5, Enterprise Mobility + Security E5 via group membership |
| Cody Godinez   | Contoso_Sales    | Office 365 E5, Enterprise Mobility + Security E5 via group membership direct assignment |
| Allan Deyoung  | Contoso_Admins | Office 365 E5, Enterprise Mobility + Security E5 via group membership |
| Alex Wilber  | Contoso_Admins | Office 365 E5, Enterprise Mobility + Security E5 via group membership |

You also been asked to modify the Company branding for the sign-in page.

### Task 1: Create groups by using the Microsoft Entra admin center

1. On **SEA-SVR1**, in the Microsoft Entra admin center, in the navigation pane, select **Identity > Groups** > **All groups**.

2. Select **New group**.

3. On the **New Group** page, enter the following:

    - Group type: **Security**
    - Group name: **Contoso_Managers**
    - Membership type: **Assigned**

4. Under Members, select **No members selected**.

5. In the Add members page add **Edmund Reeve**, **Miranda Snider**, and then click **Select**.

6. Select **Create**.

1. Back in **Groups|All groups** tab, select **New group**.

3. On the **New Group** page, enter the following:

    - Group type: **Security**
    - Group name: **Contoso_Admins**
    - Membership type: **Assigned**

4. Under Members, select **No members selected**.

5. In the Add members page add **Allan Deyoung**, **Alex Wilber**, and then click **Select**.

6. Select **Create**.

### Task 2: Create groups by using PowerShell

1. On SEA-SVR1, switch to Windows PowerShell.

2. In the **PowerShell 7** window, type the following code to create a new group, and then press **Enter**:

    ```
    New-MgGroup -DisplayName “Contoso_Sales” -Description “Contoso_Sales_team_users” -MailEnabled:$false -Mailnickname "Contoso_Sales" -SecurityEnabled
    ```

3. In the **PowerShell 7** window, type the following command, and then press **Enter**:

    ```
    Get-MgGroup
    ```

4. Verify that you get the list of groups in your tenant, including the Contoso_Sales group you just created.

5. In the **PowerShell 7** window, type the following code to define a variable as the Contoso_Sales group, and then press **Enter**:

    ```
    $group = Get-MgGroup | Where-Object {$_.DisplayName -eq "Contoso_Sales"}
    ```

6. In the **PowerShell 7** window, type the following code to define another variable as the user, and then press **Enter**:

    ```
    $user = Get-MgUser | Where-Object {$_.DisplayName -eq "Cody Godinez"}
    ```

7. In the **PowerShell 7** window, type the following code to add Cody to Contoso_Sales using set variables, and then press **Enter**:

    ```
    New-MgGroupMember -GroupId $group.Id -DirectoryObjectId $user.Id
    ```

8. In the **PowerShell 7** window, type the following code, and then press **Enter**:

    ```
    Get-MgGroupMember -GroupId $group.Id | FL
    ```

9. Verify that you see **Cody Godinez** as value in **AdditionalProperties**.

10. Close PowerShell.

### Task 3: Review licenses

1. In the Microsoft Entra admin center, in the navigation pane, select **Identity > Billing** > **Licenses**.

2. On the **Licenses|Overview** page, under **Manage**, select **All products**.

   > Take note of the current licenses available and assigned for **Enterprise Mobility + Security E5** and **Office 365 E5**.

3. In the Microsoft Entra admin center, in the Navigation pane, select **Identity > User experiences** > **Company branding**.

4. On the **Company Branding** page, under **Default sign-in experience**, select **Customize**.

5. On the **Customize default sign-in experience** page, navigate to the **Sign-in form** tab and configure the following settings:

   - Sign-in page text: **Contoso Corp. Sign-in Page**

6. Select **Review + Create**, review the settings and then select **Create**.

7. In the Microsoft Entra admin center, in the Navigation pane, select **Identity > Users** > **All users**.

8. In the user list, select **Cody Godinez**.

9. In the Cody Godinez Profile page, under Manage, select **Licenses**.

   > Notice that Cody does not have any current license assignments.

10. Select **Assignments**.

11. In the Update license assignments page, select the check box next to **Enterprise Mobility + Security E5** and **Office 365 E5**.

12. Select **Save**.

13.  In the Microsoft Entra admin center, in the Navigation pane, select **Groups** > **All groups**.

15. On the Groups|All groups page, select **Contoso_Admins**.

16. On the Contoso_Admins page, select **Licenses**.

    > Notice that the Contoso_Admins group does not have any current license assignments.

17. Select **Assignments**.

18. In the Update license assignments page, select the check box next to **Enterprise Mobility + Security E5** and **Office 365 E5**.

19. Select **Save**.


14. In the Microsoft Entra admin center, in the Navigation pane, select **Groups** > **All groups**.

15. On the Groups|All groups page, select **Contoso_Managers**.

16. On the Contoso_Managers page, select **Licenses**.

    > Notice that the Contoso_Managers group does not have any current license assignments.

17. Select **Assignments**.

18. In the Update license assignments page, select the check box next to **Enterprise Mobility + Security E5** and **Office 365 E5**.

19. Select **Save**.

20. In the Microsoft Entra admin center, in the Navigation pane, select **Billing** > **Licenses**.

21. On the **Licenses|Overview** page, under **Manage**, select **All products**.

22. On the Licenses|All products page, select **Office 365 E5**.

   > Take note of the users that are assigned the Office 365 E5 license. Notice the Assignment Paths column which indicates how license assignment is configured for each user. Edmund and Miranda both receive their license assignment from their membership in the Contoso_Managers group. Allan and Alex both receive heir license assignment from their membership in the Contoso_Admins group. You may need to select **Refresh** a couple of times to update the Assignment path column.

22. Close Microsoft Edge.

**Results**: After completing this exercise, you should have successfully created and managed groups, modified company branding, and assigned licenses.

**END OF LAB**
