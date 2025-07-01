

#

# Template:

## Patch:
**File Names:** 
**Description:**
**Patch Notes:**

#

## Patch: 2025-06-26 P1
**File Names:** 
	
	- over_all_adminpage.php
	- email_all_functions.php
	

**Description:** 

	- Changing the cut off period of the admin account.

**Patch Notes:**

	- Updating the cut off period generate from user. Now convert to automation.
	- The logic create a cut off period base on the current day number.
	- This will will ensure the previous no clock out from the last cut off period will not be notified again.



	
                  // Begin your original logic
                  $months = ["January", "February", "March", "April", "May", "June",
                                 "July", "August", "September", "October", "November", "December"];

                      // Get today's date info
                      $currentDay = (int) date('d');
                      $currentMonthIndex = (int) date('m') - 1; // 0-based index
                      $currentYear = date('Y');

                      // Determine cutoff period
                      $cutoffPeriod = $currentDay >= 16 ? 'secondCutoff' : 'firstCutoff';

                      // Build date range
                      $m = str_pad($currentMonthIndex + 1, 2, "0", STR_PAD_LEFT);
                      if ($cutoffPeriod === "firstCutoff") {
                          $fmonthday = "$currentYear-$m-01";
                          $ldayofmst = "$currentYear-$m-15";
                      } else {
                          $fmonthday = "$currentYear-$m-16";
                          $ldayofmst = "$currentYear-$m-31";
                      }




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

	<?php

	    // Convert to 24-hour format
                  $startTimeObj = DateTime::createFromFormat('g:i A', $govertimestarts);
                  $endTimeObj   = DateTime::createFromFormat('g:i A', $govertimeends);

                  $govertimestarts = $startTimeObj ? $startTimeObj->format('H:i') : '';
                  $govertimeends   = $endTimeObj ? $endTimeObj->format('H:i') : '';

       ?>


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

           $.post("https://url/tmp-staff-all-timesheet-blank/", {
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

You're getting an error because you're trying to access `$_POST['email']` and `$_POST['password']`, but your form actually uses `name="log"` and `name="pwd"`, which are the default field names WordPress uses for login.