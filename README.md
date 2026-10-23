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
























