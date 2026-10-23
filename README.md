# Header
<p align="center">
  <img src="Images/Header.png" alt="Okta Group Rules and Attribute Based Access">
</p>

# Okta Group Rules and Attribute Based Access

This lab builds attribute based access control in Okta for Kennon Technologies. Custom profile attributes and group rules place users into groups automatically, and each group grants an app, so updating a user's profile changes their access without anyone editing group membership. The lab also tests how rules handle manual group changes and rule deactivation, and traces every access change in the System Log.

---

## Skills Demonstrated

- Creating custom user profile attributes with enumerated values
- Restricting attribute permissions so users cannot change their own access
- Building group rules with basic conditions and Okta Expression Language
- Assigning applications to groups for membership based access
- Testing mover scenarios through profile attribute changes
- Analyzing how group rules handle manual assignments, removals, and deactivation
- Auditing access changes with System Log filters

---

## Prerequisites

- An Okta org with Super Administrator access
- A private or incognito browser window for signing in as test users

---

## Environment

| Component | Details |
|---|---|
| Identity Provider | Okta Integrator Free Plan |
| Organization | Kennon Technologies (kennon.tech) |
| Custom Attributes | employmentType, workLocation |
| Groups | KT-Engineering, KT-Sales, KT-Managers, KT-Contractors, KT-Remote |
| Applications | Engineering Portal, Sales CRM, Manager Reports, Contractor Portal, Remote Access Portal |
| Test Users | Marcus Hale, Dana Brooks, Leo Tran, Priya Shah |
| Browser | Incognito window for end user sign in testing |

---

## Table of Contents

1. [Add Custom Profile Attributes](#1-add-custom-profile-attributes)
2. [Create Groups and Bookmark Apps](#2-create-groups-and-bookmark-apps)
3. [Create Test Users with Profile Attributes](#3-create-test-users-with-profile-attributes)
4. [Build Group Rules](#4-build-group-rules)
5. [Verify Access as End Users](#5-verify-access-as-end-users)
6. [Change Attributes and Confirm Automatic Access Updates](#6-change-attributes-and-confirm-automatic-access-updates)
7. [Group Rule Behavior Checks](#7-group-rule-behavior-checks)
8. [Cleanup](#8-cleanup)

---

## 1) Add Custom Profile Attributes

Two custom attributes are added to the default user profile to track employment type and work location. Group rules will use these alongside the built in department and title attributes.

### Add a Custom Attribute

1. In the **Okta Administrator Console** open the **Directory** dropdown then select **Profile Editor**
2. Select **User (default)** then **Add Attribute** and enter the following information then **Save and Add Another:**
   
   - **Data Type:** string
   - **Display Name:** Employment Type
   - **Variable Name:** employmentType
   - **Description:** Full time employee or contractor
   - **Enum:** Check define enumerated list of values
   - **Attribute Member 1**
     - **Display Name:** Full Time
     - **Value:** FullTime
   - **Attribute Member 2**
     - **Display Name:** Contractor
     - **Value:** Contractor
  
# Image 1
<p align="center">
  <img src="Images/Image%201.PNG" alt="Image 1">
</p>


### Add a Second Custom Attribute

1. Create another attribute with the following information then **Save:**
   
   - **Data Type:** string
   - **Display Name:** Work Location
   - **Variable Name:** workLocation
   - **Description:** Primary work location
   - **Enum:** Check define enumerated list of values
   - **Attribute Member 1**
     - **Display Name:** Fort Worth Office
     - **Value:** FortWorth
   - **Attribute Member 2**
     - **Display Name:** Remote
     - **Value:** Remote
    
# Image 2
<p align="center">
  <img src="Images/Image%202.PNG" alt="Image 2">
</p>

### Verify the Custom Attributes

1. On the **User (default)** page scroll to the bottom to verify **Employment Type** and **Work Location** appear

# Image 3
<p align="center">
  <img src="Images/Image%203.PNG" alt="Image 3">
</p>

---

## 2) Create Groups and Bookmark Apps

Five groups are created to represent access, and each one is assigned a Bookmark app. Since apps are assigned to groups, group membership alone decides which apps a user sees.

### Create the Groups

1. In the **Directory** dropdown select **Groups** then **Add Group**
2. Create a group with the following information then **Save**:

   - **Name:** KT-Engineering
   - **Description:** Engineering department access

# Image 4
<p align="center">
  <img src="Images/Image%204.PNG" alt="Image 4">
</p>

3. Create more groups with the following information:

   - **First Group**
     - **Name:** KT-Sales
     - **Description:** Sales department access

   - **Second Group**
     - **Name:** KT-Managers
     - **Description:** Sales managers access

   - **Third Group**
     - **Name:** KT-Contractors
     - **Description:** Contractor access

   - **Fourth Group**
     - **Name:** KT-Remote
     - **Description:** Remote workers access

# Image 5
<p align="center">
  <img src="Images/Image%205.PNG" alt="Image 5">
</p>

### Create the Bookmark App

1. Open the **Applications and Resources** dropdown then select **Applications**
2. Press **Browse App Catalog** then search for the **Bookmark App** then click **Add Integration**
3. Fill the **General Settings** page with the following information then press **Done**
   - **Application Label:** Engineering Portal
   - **URL:** https://example.com/engineering

# Image 6
<p align="center">
  <img src="Images/Image%206.PNG" alt="Image 6">
</p>

4. Create app integration for the other four apps using the following information:

   - **First Applcation**
     - **Application Label:** Sales CRM
     - **URL:** https://example.com/sales

   - **Second Applcation**
     - **Application Label:** Manager Reports
     - **URL:** https://example.com/reports

   - **Third Applcation**
     - **Application Label:** Contractor Portal
     - **URL:** https://example.com/contractors

   - **Fourth Applcation**
     - **Application Label:** Remote Access Portal
     - **URL:** https://example.com/remote

5. Open the **Applications** page then confirm all five apps appear

# Image 7
# Image 8
<p align="center">
  <img src="Images/Image%207.PNG" alt="Image 7">
  <img src="Images/Image%208.PNG" alt="Image 8">
</p>

### Assign Each App to Its Group

1. Select the **Engineering Portal**
2. Open the **Assignments** tab then open the **Assign** dropdown then select **Assign to Groups**
3. Next to **KT-Engineering** press **Assign** then **Done**

# Image 9
<p align="center">
  <img src="Images/Image%209.PNG" alt="Image 9">
</p>

4. Repeat for the other 4 applications

   - **First Application**
     - **App:** Sales CRM
     - **Group:** KT-Sales

   - **Second Application**
     - **App:** Manager Reports
     - **Group:** KT-Managers

   - **Third Application**
     - **App:** Contractor Portal
     - **Group:** KT-Contractors

   - **Fourth Application**
     - **App:** Remote Access Portal
     - **Group:** KT-Remote

### Verify the Group Assignments

1. Open the **Directory** dropdown then open the **Groups** page
2. Select **KT-Engineering** then open the **Applications** tab
3. Confirm the **Engineering Portal** appears

# Image 10
<p align="center">
  <img src="Images/Image%2010.PNG" alt="Image 10">
</p>

4. Open the **KT-Sales, KT-Managers, KT-Contractors, and KT-Remote** groups and confirm the application appears

---

## 3) Create Test Users with Profile Attributes

Four test users are created and given a mix of attribute values. Each user is set up to land in a specific combination of groups once the rules run.

### Create the Test Users

1. Open the **Directory** dropdown then **People** then **Add Person**
2. Create a person with the following information then **Save and Add Another**

   - **User Type:** User
   - **First Name:** Marcus
   - **Last Name:** Hale
   - **Username:** marcus.hale@kennon.tech
   - **Primary Email:** marcus.hale@kennon.tech
   - **Password:** <Create a Password>
   - **User Must Change Password on First Login:** Uncheck

# Image 11
<p align="center">
  <img src="Images/Image%2011.PNG" alt="Image 11">
</p>

3. Create 3 more people with the following information:

   - **First Person**
     - **User Type:** User
     - **First Name:** Dana
     - **Last Name:** Brooks
     - **Username:** dana.brooks@kennon.tech
     - **Primary Email:** dana.brooks@kennon.tech
     - **Password:** <Create a Password>
     - **User Must Change Password on First Login:** Uncheck

   - **Second Person**
     - **User Type:** User
     - **First Name:** Leo
     - **Last Name:** Tran
     - **Username:** leo.tran@kennon.tech
     - **Primary Email:** leo.tran@kennon.tech
     - **Password:** <Create a Password>
     - **User Must Change Password on First Login:** Uncheck

   - **Third Person**
     - **User Type:** User
     - **First Name:** Priya
     - **Last Name:** Shah
     - **Username:** priya.shah@kennon.tech
     - **Primary Email:** priya.shah@kennon.tech
     - **Password:** <Create a Password>
     - **User Must Change Password on First Login:** Uncheck

# Image 12
<p align="center">
  <img src="Images/Image%2012.PNG" alt="Image 12">
</p>

### Set Each User's Profile Attributes

1. Open **Marcus Hale's** profile then open the **Profile** tab then select **Edit**
2. Fill out the following information then **Save:**

   - **Title:** Software Engineer
   - **Department:** Engineering
   - **Employment Type:** Full Time
   - **Work Location:** Fort Worth Office

# Image 13
# Image 14
<p align="center">
  <img src="Images/Image%2013.PNG" alt="Image 13">
  <img src="Images/Image%2014.PNG" alt="Image 14">
</p>

3. Open **Dana Brooks'** profile and add the following information then **Save:**

   - **Title:** Sales Manager
   - **Department:** Sales
   - **Employment Type:** Full Time
   - **Work Location:** Remote

# Image 15
# Image 16
<p align="center">
  <img src="Images/Image%2015.PNG" alt="Image 15">
  <img src="Images/Image%2016.PNG" alt="Image 16">
</p>

4. Open **Leo Tran's** profile and add the following information then **Save:**

   - **Title:** Account Executive
   - **Department:** Sales
   - **Employment Type:** Full Time
   - **Work Location:** Fort Worth Office

# Image 17
# Image 18
<p align="center">
  <img src="Images/Image%2017.PNG" alt="Image 17">
  <img src="Images/Image%2018.PNG" alt="Image 18">
</p>

5. Open **Priya Shah's** profile and add the following information then **Save:**

   - **Title:** QA Tester
   - **Department:** Engineering
   - **Employment Type:** Contractor
   - **Work Location:** Remote

# Image 19
# Image 20
<p align="center">
  <img src="Images/Image%2019.PNG" alt="Image 19">
  <img src="Images/Image%2020.PNG" alt="Image 20">
</p>

---

## 4) Build Group Roles

Group rules are built to place users into groups based on their attributes. The rules range from simple single attribute conditions to an Okta Expression Language rule that combines department and title.

### Create and Activate a Basic Group Rule

1. Open the **Directory** dropdown then select **Groups**
2. Open the **Rules** tab then press **Add Rule**
3. Create a rule with the following information then **Save**

   - **Name:** KT-Engineering by Department
   - **IF:** Use basic condition
   - **Attribute Type:** User attribute
   - **Attribute:** department
   - **Operator:** Equals
   - **Value:** Engineering
   - **THEN Assign to:** KT-Engineering
   - **Except:** leave empty

# Image 21
<p align="center">
  <img src="Images/Image%2021.PNG" alt="Image 21">
</p>

4. On the **Rules** page to the right of the **KT-Engineering by Department** rule open the **Actions** dropdown then **Activate**

# Image 22
<p align="center">
  <img src="Images/Image%2022.PNG" alt="Image 22">
</p>

### Verify the Rule Membership

1. Open the **All** tab then select **KT-Engineering**
2. Confirm **Marcus Hale** and **Priya Shah** appear

# Image 23
<p align="center">
  <img src="Images/Image%2023.PNG" alt="Image 23">
</p>

### Create the Remaining Group Rules

1. Repeat the steps to create, activate, and verify the following 4 rules:

   - **First Rule**
      - **Name:** KT-Sales by Department
      - **IF:** Use basic condition
      - **Attribute Type:** User attribute
      - **Attribute:** department | string
      - **Operator:** Equals
      - **Value:** Sales
      - **THEN Assign to:** KT-Sales
      - **Except:** leave empty
   
   - **Second Rule**
      - **Name:** KT-Contractors by Employment Type
      - **IF:** Use basic condition
      - **Attribute Type:** User attribute
      - **Attribute:** employmentType | string
      - **Operator:** Equals
      - **Value:** Contractor
      - **THEN Assign to:** KT-Contractors
      - **Except:** leave empty
   
   - **Third Rule**
      - **Name:** KT-Remote by Work Location
      - **IF:** Use basic condition
      - **Attribute Type:** User attribute
      - **Attribute:** workLocation | string
      - **Operator:** Equals
      - **Value:** Remote
      - **THEN Assign to:** KT-Remote
      - **Except:** leave empty

   - **Fourth Rule**
      - **Name:** KT-Managers by Title
      - **IF:** Use Okta Expression Language
      - **Expression:** `user.department == "Sales" AND String.stringContains(user.title, "Manager")`
      - **THEN Assign to:** KT-Managers
      - **Except:** leave empty

# Image 24
<p align="center">
  <img src="Images/Image%2024.PNG" alt="Image 24">
</p>

---

## 5) Verify Access as End Users

Each test user signs in to confirm their dashboard shows only the apps their attributes should grant. This verifies the full chain from attribute to group to app.

### Verify Each User's Dashboard

1. In an **Incognito Window** sign in to **Marcus Hale's Okta Account**
2. Confirm you can see the **Engineering Portal** app on the dashboard

# Image 25
<p align="center">
  <img src="Images/Image%2025.PNG" alt="Image 25">
</p>

3. Sign out of **Marcus's account** then sign in as **Dana Brooks**
4. Confirm you can see the **Manager Reports, Remote Access Portal, and Sales CRM** apps on the dashboard

# Image 26
<p align="center">
  <img src="Images/Image%2026.PNG" alt="Image 26">
</p>

5. Sign out of **Dana's account** then sign in as **Leo Tran**
6. Confirm you can see the **Sales CRM** app on the dashboard

# Image 27
<p align="center">
  <img src="Images/Image%2027.PNG" alt="Image 27">
</p>

7. Sign out of **Leo's account** then sign in as **Priya Shah**
8. Confirm you can see the **Engineering Portal, Contractor Portal, and Remote Access Portal** apps on the dashboard

# Image 28
<p align="center">
  <img src="Images/Image%2028.PNG" alt="Image 28">
</p>

---

## 6) Change Attributes and Confirm Automatic Access Updates

User attributes are changed to simulate department moves, employment changes, and promotions. Group membership and app access update automatically, and the System Log confirms Okta made each change on its own.

### Change a User's Department

1. In the **Okta Administrator Console** open the **Directory** dropdown then **People**
2. Select **Marcus Hale** then open the **Profile** tab then click **Edit**
3. Change the **Department** from **Engineering** to **Sales** then **Save**

# Image 29
<p align="center">
  <img src="Images/Image%2029.PNG" alt="Image 29">
</p>

### Verify the Department Change

1. Open **Marcus's Groups** tab and confirm **KT-Engineering** doesn't appear but **KT-Sales** appears

# Image 30
<p align="center">
  <img src="Images/Image%2030.PNG" alt="Image 30">
</p>

2. In an **Incognito Window** sign in to **Marcus Hale's Okta Account**
3. Confirm that only the **Sales CRM** app appears on the dashboard

# Image 31
<p align="center">
  <img src="Images/Image%2031.PNG" alt="Image 31">
</p>

### Change a User's Employment Type

1. In the **Okta Administrator Console** open **Priya Shah's** profile
2. Open the **Profile** tab then click **Edit**
3. Change the **Employment Type** from **Contractor** to **Full Time** then **Save**

# Image 32
<p align="center">
  <img src="Images/Image%2032.PNG" alt="Image 32">
</p>

### Verify the Employment Type Change

1. Open **Priya's Groups** tab and confirm that **KT-Contractors** doesn't appear but **KT-Engineering** and **KT-Remote** still appear

# Image 33
<p align="center">
  <img src="Images/Image%2033.PNG" alt="Image 33">
</p>

2. In an **Incognito Window** sign in to **Priya Shah's Okta Account**
3. Confirm that only the **Engineering Portal** and **Remote Access Portal** apps appear on the dashboard

# Image 34
<p align="center">
  <img src="Images/Image%2034.PNG" alt="Image 34">
</p>

### Change a User's Title

1. In the **Okta Administrator Console** open **Leo Tran's** profile
2. Open the **Profile** tab then click **Edit**
3. Change the **Title** from **Account Executive** to **Sales Manager** then **Save**

# Image 35
<p align="center">
  <img src="Images/Image%2035.PNG" alt="Image 35">
</p>

### Verify the Title Change

1. Open **Leo's Groups** tab and confirm that **KT-Managers** and **KT-Sales** appear

# Image 36
<p align="center">
  <img src="Images/Image%2036.PNG" alt="Image 36">
</p>

2. In an **Incognito Window** sign in to **Priya Shah's Okta Account**
3. Confirm that only the **Sales CRM** and **Manager Reports** apps appear on the dashboard

# Image 37
<p align="center">
  <img src="Images/Image%2037.PNG" alt="Image 37">
</p>

### Review the Changes in the System Log

1. In the **Okta Administrator Console** open the **Reports** dropdown then **System Log**
2. Set the time range to cover today's changes
3. Select **Advanced Filters** then enter the following filter then **Apply Filter**
   `eventType sw "group.user_membership"`

# Image 38
<p align="center">
  <img src="Images/Image%2038.PNG" alt="Image 38">
</p>

4. Review the event from the attribute changes. The log should show four membership changes, all with **Okta System** as the actor:
    - Marcus Hale removed from KT-Engineering and added to KT-Sales
    - Priya Shah removed from KT-Contractors
    - Leon Tran added to KT-Managers
   
# Image 39
<p align="center">
  <img src="Images/Image%2039.PNG" alt="Image 39">
</p>

---

## 7) Group Rule Behavior Checks

This phase tests how group rules treat manual group changes and rule deactivation. These behaviors determine whether access stays accurate when admins and rules both manage the same group.

### Manual Group Assignments

1. In the **Okta Administrator Console** open the **Directory** dropdown then **Groups**
2. Open **KT-Engineering** then click **Assign People**
3. Press the **Plus** next to **Marcus Hale** then **Done**

# Image 40
<p align="center">
  <img src="Images/Image%2040.PNG" alt="Image 40">
</p>

4. Under the **Directory** dropdown select **People**
5. Select **Marcus Hale** then open the **Profile** tab then **Edit**
6. Change the **Title** from **Software Engineer** to **Sales Engineer** then **Save**

# Image 41
<p align="center">
  <img src="Images/Image%2041.PNG" alt="Image 41">
</p>

### Verify Manual Assignments Persist

1. Open **Marcus's Groups** tab and confirm both the **KT-Engineering** and **KT-Sales** groups appear

# Image 42
<p align="center">
  <img src="Images/Image%2042.PNG" alt="Image 42">
</p>

2. Open the **Reports** dropdown then **System Log**
3. Set the time range to cover today's changes
4. Select **Advanced Filters** then enter the following filter then **Apply Filter**
    `eventType sw "group.user_membership"`

# Image 43
<p align="center">
  <img src="Images/Image%2043.PNG" alt="Image 43">
</p>

5. Review the event from the attribute changes. The log should show one new membership changes, with **Okta System** as the actor:

# Image 44
<p align="center">
  <img src="Images/Image%2044.PNG" alt="Image 44">
</p>

### Manual Group Removals

1. Open the **Directory** dropdown then **Groups**
2. Open **KT-Remote** find **Priya Shah** then remove her from the group

# Image 45
<p align="center">
  <img src="Images/Image%2045.PNG" alt="Image 45">
</p>

3. Under the **Directory** dropdown select **People**
4. Select **Priya Shah** then open the **Profile** tab then **Edit**
5. Change the **Title** from **QA Tester** to **QA Engineer** then **Save**

# Image 46
<p align="center">
  <img src="Images/Image%2046.PNG" alt="Image 46">
</p>

### Verify the Rule Exclusion

1. Open **Priya's Group** tab and confirm the **KT-Engineering** group appear

# Image 47
<p align="center">
  <img src="Images/Image%2047.PNG" alt="Image 47">
</p>

2. Open the **Reports** dropdown then **System Log**
3. Set the time range to cover today's changes
4. Select **Advanced Filters** then enter the following filter then **Apply Filter**
    `eventType sw "group.user_membership"`

# Image 48
<p align="center">
  <img src="Images/Image%2048.PNG" alt="Image 48">
</p>

5. Review the event from the attribute changes. The log should show two new membership changes, with **Okta System** as the actor for one and **Ryan Kennon** as the other actor:

# Image 49
<p align="center">
  <img src="Images/Image%2049.PNG" alt="Image 49">
</p>

### Rule Deactivation and Reactivation

1. Open the **Directory** dropdown then **Groups** then open the **Rules** tab
2. Click the **Actions** dropdowns next to **KT-Managers by Title** then choose **Deactivate**

# Image 50
<p align="center">
  <img src="Images/Image%2050.PNG" alt="Image 50">
</p>

3. Open the **All** tab then select **KT-Managers**
4. Confirm both **Dana Brooks** and **Leo Tran** appear

# Image 51
<p align="center">
  <img src="Images/Image%2051.PNG" alt="Image 51">
</p>

5. Open the **Directory** dropdown then **People**
6. Select **Leo Tran** then the **Profile** tab then **Edit**
7. Change the **Title** from **Sales Manager** back to **Account Executive** then **Save**

# Image 52
<p align="center">
  <img src="Images/Image%2052.PNG" alt="Image 52">
</p>

8. Check **Leo's Group** tab and confirm both **KT-Sales** and **KT-Managers** appear

# Image 53
<p align="center">
  <img src="Images/Image%2053.PNG" alt="Image 53">
</p>

9. Under the **Directory** dropdown select **Groups** then open the **Rules** tab
10. Open the **Actions** dropdown next to **KT-Managers by Title** then press **Activate**

# Image 54
<p align="center">
  <img src="Images/Image%2054.PNG" alt="Image 54">
</p>

### Verify Reactivation Reevaluates Member

1. Go back to **Leo Tran's** profile then open the **Groups** tab
2. Confirm that only **KT-Managers** appears

# Image 55
<p align="center">
  <img src="Images/Image%2055.PNG" alt="Image 55">
</p>

3. Open the **Reports** dropdown then **System Log**
4. Set the time range to cover today's changes
5. Select **Advanced Filters** then enter the following filter then **Apply Filter**
    `eventType sw "group.user_membership"`

# Image 56
<p align="center">
  <img src="Images/Image%2056.PNG" alt="Image 56">
</p>

6. Review the event from the attribute changes. The log should show two new membership changes, with **Ryan Kennon** as the actor:

# Image 57
<p align="center">
  <img src="Images/Image%2057.PNG" alt="Image 57">
</p>

---

## 8) Cleanup

### Deactivate and Delete the Group Rules

All lab objects are removed in reverse order of creation. Group rules go first, since custom attributes cannot be deleted while a rule still references them.

1. Under the **Directory** dropdown select **Groups** then open the **Rules** tab
2. Open the **Actions** dropdown next to **KT-Mangers by Title** then select **Deactivate**

# Image 58
<p align="center">
  <img src="Images/Image%2058.PNG" alt="Image 58">
</p>

3. Open the **All** tab select **KT-Managers**
4. Confirm **Dana Brooks** still appears despite deleting the rule

# Image 59
<p align="center">
  <img src="Images/Image%2059.PNG" alt="Image 59">
</p>

5. Delete all the **Group Rules** we created in this lab

# Image 60
<p align="center">
  <img src="Images/Image%2060.PNG" alt="Image 60">
</p>

### Deactivate and Delete the Test Users

1. Under the **Directory** dropdown select **People**
2. **Deactivate** and **Delete** all users except administrator

# Image 61
<p align="center">
  <img src="Images/Image%2061.PNG" alt="Image 61">
</p>

### Deactivate and Delete the Bookmark Apps

1. Under the **Applications and Resources** dropdown select **Applications**
2. Click the **Contractor Portal** then select the **Active** dropdown then **Deactivate**
3. Click the **Inactive** dropdown then **Delete**

# Image 62
<p align="center">
  <img src="Images/Image%2062.PNG" alt="Image 62">
</p>

4. Delete all the **Applications** we created in this lab

# Image 62.5
<p align="center">
  <img src="Images/Image%2062.5.PNG" alt="Image 62.5">
</p>

### Delete the Groups

1. Under the **Directory** dropdown select **Groups**
2. Open **KT-Engineering** then open the **Action** dropdown then **Delete**

# Image 63
<p align="center">
  <img src="Images/Image%2063.PNG" alt="Image 63">
</p>

3. Delete all the **Groups** we created in this lab

# Image 64
<p align="center">
  <img src="Images/Image%2064.PNG" alt="Image 64">
</p>

### Remove the Custom Attributes

1. Under the **Directory** dropdown select **Profile Editor** select **User (default)**
2. Scroll to the bottom and press the **X** next to **Employment Type** and **Work Location** to **Delete** the attributes

# Image 65
<p align="center">
  <img src="Images/Image%2065.PNG" alt="Image 65">
</p>

---

## Closing Note

This lab showed how attribute based access removes the need to manage group membership by hand. Once the group rules were in place, updating a user's department, employment type, or title was enough to change their access, and the System Log recorded each change as an automatic action by Okta. The behavior checks were the most useful part, since they showed that manual removals create rule exclusions, manual assignments are never removed by a rule, and deactivated rules leave existing members in place until they are reactivated.
