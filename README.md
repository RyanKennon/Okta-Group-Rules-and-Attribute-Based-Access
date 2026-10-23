# Okta-Group-Rules-and-Attribute-Based-Access

## 1) Add Custom Profile Attributes

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

3. Create another attribute with the following information then **Save:**
   
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

4. On the **User (default)** page scroll to the bottom to verify **Employment Type** and **Work Location** appear

# Image 3

---

## 2) Create Groups and Bookmark Apps

1. In the **Directory** dropdown select **Groups** then **Add Group**
2. Create a group with the following information then **Save**:

   - **Name:** KT-Engineering
   - **Description:** Engineering department access

# Image 4

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

4. Open the **Applications and Resources** dropdown then select **Applications**
5. Press **Browse App Catalog** then search for the **Bookmark App** then click **Add Integration**
6. Fill the **General Settings** page with the following information then press **Done**
   - **Application Label:** Engineering Portal
   - **URL:** https://example.com/engineering

# Image 6

7. Create app integration for the other four apps using the following information:

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

8. Open the **Applications** page then confirm all five apps appear

# Image 7
# Image 8

9. Select the **Engineering Portal**
10. Open the **Assignments** tab then open the **Assign** dropdown then select **Assign to Groups**
11. Next to **KT-Engineering** press **Assign** then **Done**

# Image 9

12. Repeat for the other 4 applications

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

13. Open the **Directory** dropdown then open the **Groups** page
14. Select **KT-Engineering** then open the **Applications** tab
15. Confirm the **Engineering Portal** appears

# Image 10

16. Open the **KT-Sales, KT-Managers, KT-Contractors, and KT-Remote** groups and confirm the application appears

---

## 3) Create Test Users with Profile Attributes

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

4. Open **Marcus Hale's** profile then open the **Profile** tab then select **Edit**
5. Fill out the following information then **Save:**

   - **Title:** Software Engineer
   - **Department:** Engineering
   - **Employment Type:** Full Time
   - **Work Location:** Fort Worth Office

# Image 13
# Image 14

6. Open **Dana Brooks'** profile and add the following information then **Save:**

   - **Title:** Sales Manager
   - **Department:** Sales
   - **Employment Type:** Full Time
   - **Work Location:** Remote

# Image 15
# Image 16

7. Open **Leo Tran's** profile and add the following information then **Save:**

   - **Title:** Account Executive
   - **Department:** Sales
   - **Employment Type:** Full Time
   - **Work Location:** Fort Worth Office

# Image 17
# Image 18

8. Open **Priya Shah's** profile and add the following information then **Save:**

   - **Title:** QA Tester
   - **Department:** Engineering
   - **Employment Type:** Contractor
   - **Work Location:** Remote

# Image 19
# Image 20

---

## 4) Build Group Roles

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

4. On the **Rules** page to the right of the **KT-Engineering by Department** rule open the **Actions** dropdown then **Activate**

# Image 22

5. Open the **All** tab then select **KT-Engineering**
6. Confirm **Marcus Hale** and **Priya Shah** appear

# Image 23

7. Repeat the steps to create, activate, and verify the following 4 rules:

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

---

## 5) Verify Access as End Users

1. In an **Incognito Window** sign in to **Marcus Hale's Okta Account**
2. Confirm you can see the **Engineering Portal** app on the dashboard

# Image 25

3. Sign out of **Marcus's account** then sign in as **Dana Brooks**
4. Confirm you can see the **Manager Reports, Remote Access Portal, and Sales CRM** apps on the dashboard

# Image 26

5. Sign out of **Dana's account** then sign in as **Leo Tran**
6. Confirm you can see the **Sales CRM** app on the dashboard

# Image 27

7. Sign out of **Leo's account** then sign in as **Priya Shah**
8. Confirm you can see the **Engineering Portal, Contractor Portal, and Remote Access Portal** apps on the dashboard

# Image 28

---

## 6) Change Attributes and Confirm Automatic Access Updates

1. In the **Okta Administrator Console** open the **Directory** dropdown then **People**
2. Select **Marcus Hale** then open the **Profile** tab then click **Edit**
3. Change the **Department** from **Engineering** to **Sales** then **Save**

# Image 29

4. Open **Marcus's Groups** tab and confirm **KT-Engineering** doesn't appear but **KT-Sales** appears

# Image 30

5. In an **Incognito Window** sign in to **Marcus Hale's Okta Account**
6. Confirm that only the **Sales CRM** app appears on the dashboard

# Image 31

7. In the **Okta Administrator Console** open **Priya Shah's** profile
8. Open the **Profile** tab then click **Edit**
9. Change the **Employment Type** from **Contractor** to **Full Time** then **Save**

# Image 32

10. Open **Priya's Groups** tab and confirm that **KT-Contractors** doesn't appear but **KT-Engineering** and **KT-Remote** still appear

# Image 33

11. In an **Incognito Window** sign in to **Priya Shah's Okta Account**
12. Confirm that only the **Engineering Portal** and **Remote Access Portal** apps appear on the dashboard

# Image 34

13. In the **Okta Administrator Console** open **Leo Tran's** profile
14. Open the **Profile** tab then click **Edit**
15. Change the **Title** from **Account Executive** to **Sales Manager** then **Save**

# Image 35

16. Open **Leo's Groups** tab and confirm that **KT-Managers** and **KT-Sales** appear

# Image 36

17. In an **Incognito Window** sign in to **Priya Shah's Okta Account**
18. Confirm that only the **Sales CRM** and **Manager Reports** apps appear on the dashboard

# Image 37

19. In the **Okta Administrator Console** open the **Reports** dropdown then **System Log**
20. Set the time range to cover today's changes
21. Select **Advanced Filters** then enter the following filter then **Apply Filter**
   `eventType sw "group.user_membership"`

# Image 38

23. Review the event from the attribute changes. The log should show four membership changes, all with **Okta System** as the actor:
    - Marcus Hale removed from KT-Engineering and added to KT-Sales
    - Priya Shah removed from KT-Contractors
    - Leon Tran added to KT-Managers
   
# Image 39

---

# 7) Group Rule Behavior Checks

1. In the **Okta Administrator Console** open the **Directory** dropdown then **Groups**
2. Open **KT-Engineering** then click **Assign People**
3. Press the **Plus** next to **Marcus Hale** then **Done**

# Image 40

4. Under the **Directory** dropdown select **People**
5. Select **Marcus Hale** then open the **Profile** tab then **Edit**
6. Change the **Title** from **Software Engineer** to **Sales Engineer** then **Save**

# Image 41

7. Open **Marcus's Groups** tab and confirm both the **KT-Engineering** and **KT-Sales** groups appear

# Image 42

8. Open the **Reports** dropdown then **System Log**
9. Set the time range to cover today's changes
10. Select **Advanced Filters** then enter the following filter then **Apply Filter**
    `eventType sw "group.user_membership"`

# Image 43

11. Review the event from the attribute changes. The log should show one new membership changes, with **Okta System** as the actor:

# Image 44

12. Open the **Directory** dropdown then **Groups**
13. Open **KT-Remote** find **Priya Shah** then remove her from the group

# Image 45

14. Under the **Directory** dropdown select **People**
15. Select **Priya Shah** then open the **Profile** tab then **Edit**
16. Change the **Title** from **QA Tester** to **QA Engineer** then **Save**

# Image 46

17. Open **Priya's Group** tab and confirm the **KT-Engineering** group appear

# Image 47

18. Open the **Reports** dropdown then **System Log**
19. Set the time range to cover today's changes
20. Select **Advanced Filters** then enter the following filter then **Apply Filter**
    `eventType sw "group.user_membership"`

# Image 48

21. Review the event from the attribute changes. The log should show two new membership changes, with **Okta System** as the actor for one and **Ryan Kennon** as the other actor:

# Image 49

22. Open the **Directory** dropdown then **Groups** then open the **Rules** tab
23. Click the **Actions** dropdowns next to **KT-Managers by Title** then choose **Deactivate**

# Image 50

24. Open the **All** tab then select **KT-Managers**
25. Confirm both **Dana Brooks** and **Leo Tran** appear

# Image 51

26. Open the **Directory** dropdown then **People**
27. Select **Leo Tran** then the **Profile** tab then **Edit**
28. Change the **Title** from **Sales Manager** back to **Account Executive** then **Save**

# Image 52

29. Check **Leo's Group** tab and confirm both **KT-Sales** and **KT-Managers** appear

# Image 53

30. Under the **Directory** dropdown select **Groups** then open the **Rules** tab
31. Open the **Actions** dropdown next to **KT-Managers by Title** then press **Activate**

# Image 54

32. Go back to **Leo Tran's** profile then open the **Groups** tab
33. Confirm that only **KT-Managers** appears

# Image 55

34. Open the **Reports** dropdown then **System Log**
35. Set the time range to cover today's changes
36. Select **Advanced Filters** then enter the following filter then **Apply Filter**
    `eventType sw "group.user_membership"`

# Image 56

37. Review the event from the attribute changes. The log should show two new membership changes, with **Ryan Kennon** as the actor:

# Image 57

---

## 8) Cleanup

1. Under the **Directory** dropdown select **Groups** then open the **Rules** tab
2. Open the **Actions** dropdown next to **KT-Mangers by Title** then select **Deactivate**

# Image 58

3. Open the **All** tab select **KT-Managers**
4. Confirm **Dana Brooks** still appears despite deleting the rule

# Image 59

5. Delete all the **Group Rules** we created in this lab

# Image 60

6. Under the **Directory** dropdown select **People**
7. **Deactivate** and **Delete** all users except administrator

# Image 61

8. Under the **Applications and Resources** dropdown select **Applications**
9. Click the **Contractor Portal** then select the **Active** dropdown then **Deactivate**
10. Click the **Inactive** dropdown then **Delete**

# Image 62

11. Delete all the **Applications** we created in this lab

# Image 62.5

12. Under the **Directory** dropdown select **Groups**
13. Open **KT-Engineering** then open the **Action** dropdown then **Delete**

# Image 63

14. Delete all the **Groups** we created in this lab

# Image 64

15. Under the **Directory** dropdown select **Profile Editor** select **User (default)**
16. Scroll to the bottom and press the **X** next to **Employment Type** and **Work Location** to **Delete** the attributes

# Image 65













