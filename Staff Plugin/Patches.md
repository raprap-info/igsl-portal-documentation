

#

Template:

## Patch:
**File Names:** 
**Description:**
**Patch Notes:**


#


## Patch: 2025-07-01 P1
**File Names:**  

	- ezra_application_form_admin_page.php

**Description:** 

	- Updating the correct Vendor or RC name for charging to account

# Patch Notes: Ezra Gym Membership Vendor Name Auto-Update

## Overview

This patch introduces a feature to automatically update the vendor name in the Ezra Gym membership table (`igsl_ezra_gym_reservation`) based on registered vendor names within the `RC Vendor List` (specifically, the `igsl_rc_and_vendor_combine` table). This aims to reduce manual work for administrators and minimize human errors related to incorrect Responsibility Centre (RC) or vendor name entries.

## Logic and Rules

1.  **Email Address as Key:** The core logic relies on using the user's email address to search for a corresponding registered vendor name in the `igsl_rc_and_vendor_combine` table.
2.  **Dynamic Update:** If a matching vendor name is found for the user's email, the system will dynamically update that specific user's `vender_name` in the `igsl_ezra_gym_reservation` table. This ensures accurate charging processes for personal accounts.
3.  **Registration Check:** If a user's email is not registered in the `RC Vendor List`, a "No Vendor Registered" message will be displayed, indicating that no automatic update can be performed for that user.

## Code Snippet

```php
<?php

    /**
     ** EZRA GYM MEMBERSHIP REGISTRATION
     ** PATCH: 2025-06-27
     ** DOCUMENTATIONS:
     ** ADDING ON LOAD UPDATE THE MEMBERSIP
     ** THE VENDOR NAME UPDATE DYNAMICALLY INSERT INTO
     ** THE TBL OF EZRA MEMBERSHIP VIA EMAIL ADDRESS CHECK VALIDATION
     **/

    // Retrieve the RC Vendor Name from the combined RC and Vendor table
    // using the currently logged-in user's email address.
    $gallvendor = $wpdb->get_results("SELECT RC_Vendor_Name FROM igsl_rc_and_vendor_combine WHERE Name_Email ='$user->user_email' ");

    // Check if a vendor name was found for the user's email.
    if(!empty($gallvendor[0]->RC_Vendor_Name)){
        // If found, display the vendor name in green.
        echo "<p style='color:green'>" . $gallvendor[0]->RC_Vendor_Name . "</p>";

        // Update the 'vender_name' in the Ezra Gym reservation table
        // for the specific user's email with the retrieved vendor name.
        $updatemembershpven = $wpdb->query(
            $wpdb->prepare(
                "UPDATE igsl_ezra_gym_reservation SET vender_name = %s WHERE email = %s",
                $gallvendor[0]->RC_Vendor_Name,
                $user->user_email
            )
        );
    } else {
        // If no vendor name is found for the user's email, display a "No Vendor Registered" message in red.
        echo "<p style='color:red'>No Vendor Registered.</p>";
    }

?>

```

#


## Patch: 2025-06-30 p1
**File Names:**  api_latest_rc_list.php, api_alluserfportaldash.php
**Description:** For serverside fetching data
**Patch Notes:**

	- To easily get the records and less load time.



#

## Patch: 2025-06-23 p1
**File Names:** staff_task_progress_roadmap.php
**Description:** Adding Visual Search via copied image 
**Patch Notes:**

     - This inovation will make writing and copying image to text will be easily write and take notes and a futuristic way to seamless and effortless way of writing a notes.


#


## Patch: 2025-06-20 p1
**File Names:** 
	
	- igslhousingfinalcurmonthisting.php.
	- igslsendingemail.php.
	- igslhousingutilitymeterlist.php
	- staff_all_info_records.php




**Description:** Console Log Error
**Patch Notes:**

	- Fixing error log displayed error.





#

## Patch: 2025-06-18 p1
**File Names:**  

	- calculation_payroll_page_crtd.php
	- report_payroll_fr_finance_pg.php

**Description:** Payroll Calculations update
**Patch Notes:**

	
	- Fixing the error when the page visit in the first place.

	Solution:

	```php

	<?php

	 $month_period = $_POST['month_period'] ?? '';

		 $month = '';
		 $period = '';

		 if (strpos($month_period, ' : ') !== false) {
		     list($month, $period) = explode(' : ', $month_period);
		 } else {
		     // Fallback or error handling
		     $month = date('Ym');  // Default to current month
		     $period = '1';        // Default to first period
		 }

		 // Safeguard: Ensure valid length for $month
		 if (strlen($month) !== 6 || !is_numeric($month)) {
		     die("Invalid month format.");
		 }

		 // Build start and end date
		 if ($period == '1') {
		     $start = substr($month, 0, 4) . '-' . substr($month, 4, 2) . '-01';
		     $end = substr($month, 0, 4) . '-' . substr($month, 4, 2) . '-15';
		 } else {
		     $start = substr($month, 0, 4) . '-' . substr($month, 4, 2) . '-16';
		     $end = substr($month, 0, 4) . '-' . substr($month, 4, 2) . '-31';
		 }

		 // Get month name
		 function getMonthName($monthNumber) {
		     return DateTime::createFromFormat('!m', $monthNumber)->format('M'); // "Jan", "Feb", ...
		 }

		 $mm = getMonthName(substr($month, 4, 2));
		 $yyyy = substr($month, 0, 4);
		 $title = "IGSL STAFF Salary Summary - $mm $yyyy (Period $period)";

		?>
	```

	- Fixing calculation payroll page that display divided 4 instead of two from the account of Noelly.



#

## Patch: 2025-06-17 p2
**File Name:** igslsendingemail.php
**Description:** Changing send individual laundry calcualtions
**Patch Notes:**
 
 	- Fixing the individual sending display of laundry enumaration list of all laundry cost.

#

## Patch: 2025-06-17 p1
**File Name:**  calculation_payroll_page_crtd.php
**Description:** Payroll Calculations update
**Patch Notes:**

	- Fixed overtime calculation for Regular Holiday that calculated x2 but only x 1 only.

	- Fixing calculation payroll page that display divided 4 instead of two from the account of Noelly.


#

## Patch: 2025-06-16 p4  
**File Name: staff_filling_overtime.php && timesheet_clock_tracking_all_functions.php**    
**Description: Staff Filing Overtime fixed the time format.**    
**Patch Notes:**

	```php

	<?php

	    // Convert to 24-hour format
                  $startTimeObj = DateTime::createFromFormat('g:i A', $govertimestarts);
                  $endTimeObj   = DateTime::createFromFormat('g:i A', $govertimeends);

                  $govertimestarts = $startTimeObj ? $startTimeObj->format('H:i') : '';
                  $govertimeends   = $endTimeObj ? $endTimeObj->format('H:i') : '';

       ?>


	```javascript
       <script>
       			

		   flatpickr(".fovstartend", {

		        allowInput: true,  // Allows manual input
		        enableTime: true,  // Enables time selection
		        noCalendar: true,  // Hides the calendar, only time picker will be shown
		        dateFormat: "h:i K", // Formats the input as hours:minutes AM/PM (e.g., "03:30 PM")
		        time_24hr: false   // Set to false to enable AM/PM

					});

		    flatpickr(".ovetimsheet", {
		      allowInput: true,  // Allows manual input
		      enableTime: false,  // Enables time selection
		      noCalendar: false,  // Hides the calendar, only time picker will be shown
		      dateFormat: "Y-m-d", // Formats the input as hours:minutes AM/PM (e.g., "03:30 PM")
		      time_24hr: false   // Set to false to enable AM/PM
		    });



       </script>

	```
#




## Patch: 2025-06-16 P3
**File Name:  calculation_payroll_page_crtd.php **
**Description: Changing the calculation process from before that** trigger the update pending and approved now into approved only process.
**Patch Notes:**

- This process will improved the way of the calculation process that only approved by the supervisors only for the clearler information details.




#


## Patch: 2025-06-16 P2  
**File Name: igslaclhomepage.php && newupdateigslaclhome.php**  
**Description:**
**Patch Notes:**

 - Reuse the calcualation of leaves that has no table display only the calculations that will trigger
 each time staff or guard visit.
- Using this page tmp_staff_timesheet_blankpage_reload.php for regular visit and update.

		//FOR AUTOMATE CALCULATION OF
       //LEAVE BALANCES OF ALL THE STAFF

         function allleavecal(){


           let leavescal = "";

           $.post("https://igsl-portal.igsl.asia/tmp-staff-all-timesheet-blank/", {
               leavescal: leavescal
           }, function (data, status) {
               // STATUS WHEN THE PROCESS IS NOT ERROR
               try {
                   const leavlbal = JSON.parse(data);
                   console.log("leave balanace calculations" + leavlbal);
               } catch (e) {
                   console.error("Failed to parse JSON:", e);
                   console.log("Raw response:", data);
               }
           });


         }

         allleavecal();

  - Adding Login logic so that only login user will use this post request


		if (!is_user_logged_in()) {
		    wp_redirect(home_url('/login-challenge/'), 302);
		    exit();
		}


 



#
## Patch: 2025-06-16 P1  
**File Name:** external_google_logs.php  
**Description:** When visiting the `/login-challenge/`, it shows an error that causes a white page only.  

**Patch Notes:**  

 - You're getting an error because you're trying to access `$_POST['email']` and `$_POST['password']`, but your form actually uses `name="log"` and `name="pwd"`, which are the default field names WordPress uses for login.