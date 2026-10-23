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










