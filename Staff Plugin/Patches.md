

#

Template:

## Patch:
**File Names:** 
**Description:**
**Patch Notes:**


#

## Patch:
**File Names:** 

	- staff_balances_dashb.php
	- New page: fetching_all_staff_leaves_balances.php


**Description:**

	- Validate and check and also update the all staff leaves balances.
	- For checking and update the staff leave balances anytime and for any users visit that page.

**Patch Notes:**

	- Creating a dynamic checking for all the staff for there leave balances.


	```javascript


	 			/**
                ** ALL STAFF LEAVE BALANCES
                ** REALTIME UPDATING THE RECORDS
                ** OF ALL THE STAFF.
                **/

                fetch("https://igsl-portal.igsl.asia/api/fetch-staff-leave-balances/")
                    .then(response => {
                        if (!response.ok) {
                            throw new Error("Network response was not ok");
                        }
                        return response.json(); // or response.text() if it's not JSON
                    })
                    .then(data => {
                        //console.log(data); // handle your data here
                    })
                    .catch(error => {
                        console.error("Fetch error:", error);
                    });





	```


	```php


	    global $wpdb;




                       /**
                       *   GET THE FULL NAME ON THE STAFF FULLDETAILS TBL TO
                       *   DISPLAY HIS / HER FULL NAME
                       **/

                         $divbyhrs = 0;
                         $totaldayxxx = 0;

                         $gcuurnuserr = $current_user->user_login;


                           // Try to get the selected year
                           $gdplist = $wpdb->get_results(
                               $wpdb->prepare(
                                   "SELECT year_selected_only FROM tmp_staff_yearly_selections_db WHERE staff_userid = %s",
                                   $gcuurnuserr
                               )
                           );

                           // Set default to current year if no record found
                           if (!empty($gdplist)) {
                               $yearseco = $gdplist[0]->year_selected_only;
                           } else {
                               $yearseco = date('Y'); // fallback to current year
                           }




                       $gallfdtailn = $wpdb->get_results("SELECT Name, userid FROM `staff_almost_fullrecords` WHERE  inactive ='No' GROUP BY Name, userid  ORDER BY Name ASC  ");
                       foreach ($gallfdtailn as $key => $nvvalue) {


                         $fnames = $nvvalue->Name;
                         $useridxzz = $nvvalue->userid;

                         if (!empty($fnames)) {

                             $totalbalsxxx = 0;
                             $totalleave = 0;
                             $totalvleaves = 0;

                             $gtimesheetfs = $wpdb->get_results("
                                 SELECT staff_id, start_date, end_date, reasons, leave_request_type, day_schedule_half_whole
                                 FROM `staff_leave_request_tbl`
                                 WHERE staff_id = '$useridxzz'
                                   AND YEAR(start_date) = '$yearseco'
                                   AND leave_request_type IN ('VacationLeave','SickLeave')
                                   AND (admin_status = 'APPROVED' OR admin_status = 'PENDING')
                                 GROUP BY staff_id, start_date, end_date
                             ");

                             $counters = 0;

                             foreach ($gtimesheetfs as $gtvalue) {
                                 $useridg = $gtvalue->staff_id;
                                 $reasons = $gtvalue->reasons;
                                 $leave_request_type = $gtvalue->leave_request_type;
                                 $day_schedule_half_whole = $gtvalue->day_schedule_half_whole;

                                 $startxxx = new DateTime($gtvalue->start_date);
                                 $endxx = new DateTime($gtvalue->end_date);

                                 // Add +1 day only if the time is 00:00:00 (to include end day properly)
                                 if ($endxx->format('H:i:s') === '00:00:00') {
                                     //$endxx->modify('+1 day');
                                 }

                                 // Default day count logic
                                 $dayCount = 0;

                                 // If SickLeave and start-end is same day, check hours
                                 if ($leave_request_type === 'SickLeave') {
                                     $intervalMinutes = ($endxx->getTimestamp() - $startxxx->getTimestamp()) / 60;

                                     // Same calendar day
                                     if ($startxxx->format('Y-m-d') === $endxx->format('Y-m-d')) {
                                         if ($intervalMinutes >= 480) { // 8 hours
                                             $dayCount = 1;
                                         } elseif ($intervalMinutes >= 240) { // 4 hours
                                             $dayCount = 0.5;
                                         } else {
                                             $dayCount = 0;
                                         }
                                     } else {
                                         // For multi-day SickLeave, count weekdays only
                                         $period = new DatePeriod($startxxx, new DateInterval('P1D'), (clone $endxx)->modify('+1 day'));
                                         foreach ($period as $dt) {
                                             $dayOfWeek = $dt->format('N');
                                             if ($dayOfWeek < 6) {
                                                 $dayCount += 1;
                                             }
                                         }
                                     }
                                 } else {
                                     // VacationLeave – count weekdays normally
                                     $period = new DatePeriod($startxxx, new DateInterval('P1D'), (clone $endxx)->modify('+1 day'));
                                     foreach ($period as $dt) {
                                         $dayOfWeek = $dt->format('N');
                                         if ($dayOfWeek < 6) {
                                             if ($day_schedule_half_whole === 'Whole Day') {
                                                 $dayCount += 1;
                                             } else {
                                                 $dayCount += 0.5;
                                             }
                                         }
                                     }
                                 }


                                 // Accumulate totals
                                   if ($leave_request_type === 'VacationLeave') {
                                       $totalvleaves += $dayCount;
                                   } elseif ($leave_request_type === 'SickLeave') {
                                       $totalleave += $dayCount;
                                   }
                                   $totalbalsxxx += $dayCount;


                                 // Output row
                                 ?>

                                 <?php
                             }
                             }
                             $totalsickleave = $totalleave;
                             $totalvleavesx  = $totalvleaves;


                             // FINALIZE LEAVE BALANCES PER USER

                             if ($totalvleaves > 0) {
                                 $wpdb->query($wpdb->prepare(
                                     "UPDATE staff_yearleave_balances
                                      SET total_leaves_filed = %f
                                      WHERE staff_userid = %s AND leaves_names = 'VacationLeave' AND years = %s",
                                     $totalvleaves,
                                     $useridxzz,
                                     $yearseco
                                 ));
                                 //echo "VacationLeave → $useridxzz | Filed: $totalvleaves<br>";
                             }

                             if ($totalleave > 0) {
                                 $wpdb->query($wpdb->prepare(
                                     "UPDATE staff_yearleave_balances
                                      SET total_leaves_filed = %f
                                      WHERE staff_userid = %s AND leaves_names = 'SickLeave' AND years = %s",
                                     $totalleave,
                                     $useridxzz,
                                     $yearseco
                                 ));

                               //  echo "SickLeave → $useridxzz | Filed: $totalleave<br>";
                             }



                           }





                           $gcalvals = "
                               SELECT
                                   staff_userid,
                                   leaves_names,
                                   Yearly_Entitlement,
                                   total_leaves_filed,
                                   Remaining_Balances,
                                   (Yearly_Entitlement - total_leaves_filed) AS balance_difference
                               FROM staff_yearleave_balances
                               WHERE years = '$yearseco'
                               ORDER BY balance_difference ASC
                           ";

                           $getal = $wpdb->get_results($gcalvals);

                           foreach ($getal as $row) {
                               $new_balance = floatval($row->Yearly_Entitlement) - floatval($row->total_leaves_filed);

                               // Update Remaining_Balances for this row
                               $wpdb->query(
                                   $wpdb->prepare(
                                       "UPDATE staff_yearleave_balances
                                        SET Remaining_Balances = %f
                                        WHERE staff_userid = %s AND leaves_names = %s AND years = %d",
                                       $new_balance,
                                       $row->staff_userid,
                                       $row->leaves_names,
                                       $yearseco
                                   )
                               );


                               // Store log/debug info
                               $updated_data[] = $row->staff_userid . " - " . $row->leaves_names . ": New Remaining_Balances = " . number_format($new_balance, 2);





                           }


                           // Final response (after all updates)
                           wp_send_json_success([
                               'message' => 'Remaining_Balances successfully updated.',
                               'data' => $updated_data,
                               'count' => count($updated_data),
                           ]);





	```








#

## Patch: 2025-07-03 P1
**File Names:** 

	- staff_nointervention_timesheets.php
	- rsoadetails.php
	- rapthemegrabber.php
	- fetch_dataall_rconly.php
	- facility_charging_calculate.php
	- calculation_payroll_page_crtd.php


**Description:**

	- Fixing the creation or inserting the leave withoupay with the deducation income balance.
	- Transfering rsoadetails.php from theme to plugin rapthemegrabber. 
	- Updating the calculation and exporting to Netsuite RC or Vendor name dynamic tagging.


**Patch Notes:**

	- Transferring rsoadetails.php for easily updating the code refining.
	- assign page: post=330 | page name: SOA DETAILS 
	- Main Template Grabber: rapthemegrabber.php
	- Template calculation_payroll_page_crtd.php

	- Template:
	   - fetch_dataall_rconly.php
	   - Adding inserting Responsibility Centre with checking if already exist or not if not system will create that RC that
	    	will inserted to igsl_rc_and_vendor_combine table for dynamic change that will use in the future update and insert new data.


	 	- facility_charging_calculate.php
		- This page include all the exporting to netsuite for facility charging for personal tag or rc tag.
		- Adding rest day working day for guard



	```php
	
		<?php
		
		
			 	/***
				** THIS PART IS FOR GUARD LEAVES THAT
				** IS WORKING ON WEEKENDS SATURDAY AND SUNDAY
				**/


				// Section: Approved Whole-Day Leave Processing
				// Retrieves and processes all approved whole-day leave requests that overlap
				// with the current payroll period. Each day of an approved leave is then
				// inserted into the payroll timesheet records.
				$resultsxx = $wpdb->get_results(
									$wpdb->prepare(
										"SELECT * FROM `staff_leave_request_tbl`
										WHERE ((start_date BETWEEN %s AND %s) OR (end_date BETWEEN %s AND %s))
											AND `day_schedule_half_whole` = 'Whole Day'
											AND `admin_status` = 'APPROVED'
											AND `staff_id` IN ('jmiranda', 'Jligan')",
										$start, $end, $start, $end
									)
								);


				// Iterate through each fetched approved whole-day leave record
				foreach ($resultsxx as $rvalue) {
					// Extract relevant data from the current leave record
					$idkey = $rvalue->idkey;
					$staff_id = strtolower($rvalue->staff_id);
					$leave_request_type = strtolower($rvalue->leave_request_type);

					// Determine the start and end day of the leave period
					$start_day = (int)date('d', strtotime($rvalue->start_date));
					$end_day = (int)date('d', strtotime($rvalue->end_date));

					// Sub-section: Adjust Leave Dates to Fit Payroll Period Boundaries
					// Ensures that the processing of leave days does not go outside the
					// defined payroll period ($start to $end).
					if ($start_day < substr($start, 8, 2)) {
						$start_day = substr($start, 8, 2); // Adjust leave start to payroll start day
					}
					if ($end_day > substr($end, 8, 2)) {
						// Adjust leave end to payroll end day. The -1 might be a specific business rule
						// or an off-by-one adjustment depending on the exact definition of $end.
						$end_day = substr($end, 8, 2) - 1;
					}

					// Loop through each individual day within the adjusted leave period
					for ($day = $start_day; $day <= $end_day; $day++) {
						// Construct the full date for the current day being processed
						$dates = date('Y-m-d', strtotime(substr($rvalue->start_date, 0, 8) . $day));
						$user_action = $leave_request_type; // The type of leave (e.g., 'vacation', 'sick')


							// Sub-section: Prevent Duplicate Leave Entries
							// Checks if a leave entry for this specific staff member, date, and leave type
							// already exists in the payroll timesheet table.
							$existing_record = $wpdb->get_var($wpdb->prepare(
										"SELECT COUNT(*) FROM `staff_timesheets_records_pay`
										WHERE `dates` = %s AND `staff_id` = %s",
										$dates, $staff_id
									));

									// Optional: Debug output
									echo "<br><strong>Leave Type:</strong> " . esc_html($leave_request_type) . " | <strong>Staff ID:</strong> " . esc_html($staff_id) . " | <strong>Date:</strong> " . esc_html($dates) . "<br>";

									// Insert only if no existing record
									if (intval($existing_record) === 0) {
										$inserted = $wpdb->insert(
											'staff_timesheets_records_pay',
											array(
												'dates'       => $dates,
												'user_action' => $user_action,
												'staff_id'    => $staff_id,
											),
											array(
												'%s', // dates
												'%s', // user_action
												'%s'  // staff_id
											)
										);

										// Optional: Show success or failure
										if ($inserted === false) {
											echo '<div class="alert alert-danger">❌ Insert failed: ' . esc_html($wpdb->last_error) . '</div>';
											error_log('WPDB Insert Error: ' . $wpdb->last_error);
										} else {
											echo '<div class="alert alert-success">✅ Inserted successfully.</div>';
										}

										echo '<div class="alert alert-success">✅ ' .$staff_id ." - " . $dates. '.</div>';

									}




					}
				}

		
		
		?>
	

		<?php
				
					
							/**
							** GET THE USER EMAIL ADD THEN 
							** DO A SEARCH AND FIND THE EMAIL ADDRESS 
							** THAT IS BIND TO THER USERNAME VIA PORTAL
							**/


							
							// Get user email safely
								$gwordpdash = $wpdb->get_var(
									$wpdb->prepare(
										"SELECT user_email FROM {$wpdb->prefix}users WHERE user_login = %s",
										$user_namep
									)
								);
								
								// Proceed only if an email is found
								if ($gwordpdash) {
									// Get vendor using the fetched email safely
									$getvendors = $wpdb->get_results(
										$wpdb->prepare(
											"SELECT * FROM igsl_rc_and_vendor_combine WHERE Name_Email = %s LIMIT 1",
											$gwordpdash
										)
									);
								}
				
				?>

	```


#

## Patch: 2025-07-02 P1
**File Names:**  

	- staff_nointervention_timesheets.php
	- previous_timesheets_allrecords_view.php
	- ldhr_late_undertimes.php
	- all_staff_timesheets_rec_fetchajax.php
	- ezra_application_form_admin_page.php
	- export_ezra_gym_csv_netsuite.php
	- ezra_application_form_all_data_functions.php




**Description:** 

	- Dynamic Change of Last day of per month.
	- Dynamic Month of choosing cut off period.
	- Updating the correct late and undertime via staff_timesheet_pay.
	- Adding new page for fetching all staff timesheet records.
	- Display the cancellation remarks and add cancelled status.
	- Strickting to approved only members who will get the billing for the ezra gym membership. Inside calculation and export to netsuite.
	- Making to cname@igsl.asia mail send who will manage the application for cancellation of membership in the ezra gym.
	


**Patch Notes:**

	- This snippet will get the last day of each month.

```php


		<?php

				$gmonth = $timesheetsmonth;
				$gcutoff = $timesheetscufof;
				$ydatesonly = $gyearselect;



						/**
						** CREATE ARRAY TO SIMPLIFY THE MONTH AND CUTOFF CODES
						**/

						$worldmonths = [
							"January", "February", "March", "April", "May", "June",
							"July", "August", "September", "October", "November", "December"
						];

						foreach ($worldmonths as $key => $gvalmonth) {

							// Match the month
							if ($gmonth === $gvalmonth) {

								$gkeysvals = $key + 1;

								// Pad month to 2 digits
								$addzerob = str_pad($gkeysvals, 2, "0", STR_PAD_LEFT);

								if ($gcutoff === "firstCutoff") {
									$fmonthday = "$ydatesonly-$addzerob-01";
									$ldayofmst = "$ydatesonly-$addzerob-15";
								} else { // secondCutoff
									$fmonthday = "$ydatesonly-$addzerob-16";

									// Get the last day of the month dynamically
									$last_day = date("t", mktime(0, 0, 0, $gkeysvals, 1, $ydatesonly));
									$ldayofmst = "$ydatesonly-$addzerob-$last_day";
								}

							}
						}

	?>

```

```php

			<?php
			/**
			 * TEMPLATE: API FOR FETCHING ALL WP USERS + Timesheet Table
			 */

			// Prevent direct access
			defined('ABSPATH') || exit;

			if (!is_user_logged_in()) {
				wp_send_json_error(['message' => 'Unauthorized'], 401);
			}

			$user = wp_get_current_user();
			$allowed_roles = ['administrator', 'um_registrar-role', 'um_special-staff', 'um_special-role', 'um_staff', 'um_custodians', 'um_housing-role', 'um_finance-role'];

			if (array_intersect($allowed_roles, $user->roles)) {
				// All your PHP logic begins here



				$curresupv = $current_user->user_login;

				$tstimesheetsrec = $wpdb->get_results("SELECT * FROM `supervisor_timesheet_view` WHERE Supervisors = '$curresupv' ");
				foreach ($tstimesheetsrec as $key => $thvalue) {
					$timesheetsmonth =  $thvalue->Month;
					$timesheetscufof =  $thvalue->CutoffPeriod;
					$YearOnly =  $thvalue->YearOnly;
					$gyearselect = $thvalue->YearOnly;

				}







				?>

				<table id="stafftimeshetsf" style="width:100%" class="hover table table-responsive toggleTable">
					<thead>
						<tr>
							<th>No.</th>
							<th>Staff</th>
							<th>Dates</th>
							<th>Clock In</th>
							<th>Clock Out</th>
							<th>Late</th>
							<th>Undertime</th>
							<th>Absence</th>
							<th>Request Type</th>
							<th>Total</th>
						</tr>
					</thead>
					<tbody>
					<?php
					$timezone = +8;
					$curyear = gmdate("Y", time() + 3600 * ($timezone + date("I")));
					$datesonly = gmdate("m/d/Y", time() + 3600 * ($timezone + date("I")));
					$gonlydays = gmdate("d", time() + 3600 * ($timezone + date("I")));

					$gmonth = $timesheetsmonth;
					$gcutoff = $timesheetscufof;
					$ydatesonly = $gyearselect;

					$worldmonths = [
						"January", "February", "March", "April", "May", "June",
						"July", "August", "September", "October", "November", "December"
					];

					foreach ($worldmonths as $key => $gvalmonth) {
						if ($gmonth === $gvalmonth) {
							$gkeysvals = $key + 1;
							$addzerob = str_pad($gkeysvals, 2, "0", STR_PAD_LEFT);

							if ($gcutoff === "firstCutoff") {
								$fmonthday = "$ydatesonly-$addzerob-01";
								$ldayofmst = "$ydatesonly-$addzerob-15";
							} else {
								$fmonthday = "$ydatesonly-$addzerob-16";
								$ldayofmst = "$ydatesonly-$addzerob-31";
							}
						}
					}

					$startDate = new DateTime($fmonthday);
					$endDate = new DateTime($ldayofmst);
					$endDate->modify('+1 day');

					$weekends = $weekendsx = $displayWeekends = [];
					$interval = new DateInterval('P1D');
					$period = new DatePeriod($startDate, $interval, $endDate);

					foreach ($period as $date) {
						$dayOfWeek = $date->format('N');
						if ($dayOfWeek == 6) {
							$weekends[] = $date->format('Y-m-d');
							$displayWeekends[] = $date->format('Y-m-d') . " - Saturday";
						} elseif ($dayOfWeek == 7) {
							$weekendsx[] = $date->format('Y-m-d');
							$displayWeekends[] = $date->format('Y-m-d') . " - Sunday";
						}
					}

					foreach ($displayWeekends as $weekend) {
						echo $weekend . "<br>";
					}

					echo "<br><h4>Legend:</h4><br>";
					echo "<div style='display: flex; align-items: center; gap: 20px;'>
							<div style='background-color:#ffde21; height:25px; width:25px; margin-right: 5px;'></div><p style='margin: 0;'>Saturday</p>
							<div style='background-color:#90d5ff; height:25px; width:25px; margin-right: 5px;'></div><p style='margin: 0;'>Sunday</p>
							<div style='background-color:#FF3131; height:25px; width:25px; margin-right: 5px;'></div><p style='margin: 0;'>Late or Undertime</p>
						</div><br>";

					$onlyactivs = $wpdb->get_results("SELECT userid, Name FROM tabl  WHERE inactive ='No' ORDER BY Name ASC");

					foreach ($onlyactivs as $liusvalue) {
						$idlist = $liusvalue->userid;
						$naming = $liusvalue->Name;
						$countser = 0;
						$totalhrsxx = 0;

						$stgallsupstafli = $wpdb->get_results(
							$wpdb->prepare(
								"SELECT COUNT(*) as row_count, dates, clock_in, clock_out, regular, staff_id, user_action, late, undertime, absence
								FROM TBL
								WHERE dates BETWEEN %s AND %s
								AND staff_id = %s
								AND YEAR(dates) = %d
								GROUP BY dates, clock_in, clock_out, total_hours, staff_id, user_action, late, undertime, absence",
								$fmonthday, $ldayofmst, $idlist, $ydatesonly
							)
						);

						foreach ($stgallsupstafli as $listofres) {
							if ($listofres->staff_id != $idlist) continue;

							$rowstyle = '';
							if (in_array($listofres->dates, $weekends)) {
								$rowstyle = "background-color:#ffde21";
							} elseif (in_array($listofres->dates, $weekendsx)) {
								$rowstyle = "background-color:#90d5ff";
							} elseif ($listofres->late > 0 || $listofres->undertime > 0) {
								$rowstyle = "background-color:#FF3131";
							}

							echo "<tr style='$rowstyle'>
									<td>" . ++$countser . "</td>
									<td style='text-align:left;'>" . strtoupper($naming) . "</td>
									<td>{$listofres->dates}</td>
									<td>{$listofres->clock_in}</td>
									<td>{$listofres->clock_out}</td>
									<td>{$listofres->late}</td>
									<td>{$listofres->undertime}</td>
									<td>{$listofres->absence}</td>
									<td>" . strtoupper($listofres->user_action) . "</td>
									<td>8</td>
								</tr>";

							$totalhrsxx += 8;
						}

						if ($countser > 0) {
							echo "<tr style='background-color:#d1ab9b'>
									<td colspan='9'><strong>Total Hours:</strong></td>
									<td><h5>{$totalhrsxx}</h5></td>
								</tr>";
						}
					}
					?>
					</tbody>
				</table>

				<?php
			}
			?>


```

#

## Patch: 2025-07-01 P1
**File Names:**  

	- ezra_application_form_admin_page.php
	- igsl_all_vendor_list.php 
	- export_ezra_gym_csv_netsuite.php



**Description:** 

	- Updating the correct Vendor or RC name for charging to account

# Patch Notes: Ezra Gym Membership Vendor Name Auto-Update

## Overview


#

- Fixing the export_ezra_gym_csv_netsuite import to netsuite data creation.

	- Fixed:
		- Removing all unknown data.
		- Fixing the random RC name that tag to the ezra gym member that has no vendor name listed in the table.
		- Adding auto update vendor name of the ezra gym membership table.


#

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

# igsl_all_vendor_list.php 

<!-- OLD VERSION COPY FOR REFERENCE -->

```html
  <table id="rdatamain" class="hover row-border tab" style="width:70%">
      <thead>
          <tr>
              <th>ID</th>
              <th>RC / VENDOR NAME</th>
              <th>EMAIL</th>
              <th>USER</th>
              <th>USER1</th>
              <th>EMPLOYEE NAME</th>
              <th>STATUS</th>
              <th>ACTIONS</th>

          </tr>
      </thead>
      <tbody>

        <!-- MAKING FOR  LOOP FOR DISPLAYING DATA FROM DATABASE -->



          <?php

          // MAKING DATABASE CONNECTION AND GET ALL DATA FROM DATABASE

            $results = $wpdb->get_results("SELECT * FROM igsl_rc_and_vendor_combine");


                foreach ($results as $rvalue) {


          ?>
          <tr   >

            <td><?php   echo $rvalue->id_key; ?></td>
            <td style="text-align: left; font-size: 2rem"><?php   echo $rvalue->RC_Vendor_Name; ?></td>
            <td style="text-align: left; font-size: 2rem"><?php   echo $rvalue->Name_Email; ?></td>
            <td style="text-align: left; font-size: 2rem"><?php   echo $rvalue->user_name; ?></td>
            <td style="text-align: left; font-size: 2rem"><?php   echo $rvalue->user_name1; ?></td>
            <td style="text-align: left; font-size: 2rem"><?php   echo $rvalue->employee_names; ?></td>
            <td><?php   echo $rvalue->States; ?></td>
            <td >
              <!-- <button onclick="location.href='#'" type="button" class="btn btn-warning">CANCEL</button> -->





                <form method='post' action='<?= $_SERVER['REQUEST_URI']; ?>'>
                <!-- <button  onclick="location.href='#/?data=<?= $rvalue->id; ?>'"   type="button" class="btn btn-info cancel" value="edit" <?php if ($rvalue->status == 'CONFIRMED' || $rvalue->status == 'CANCELLED' || $rvalue->status == 'REJECTED'){ ?> disabled <?php   } ?> > EDIT </button> -->
                <!-- <button id='<?= $rvalue->id; ?>' data-url='<?= $rvalue->id; ?>' name="cancel" type="button" class="btn btn-danger ajax_delete cancel" value="cancel" > CANCEL </button> -->

                  <?php
                    $psndata = $rvalue->id;
                    $encrypturl = base64_encode( json_encode($psndata) );
                  ?>




                </form>

                <div style="display:grid; grid-template-columns: auto auto; gap: 1%">
                        <div>
                        <button onclick="getDetails('<?php echo $rvalue->id_key ?>')"  name="gid"  class="btn btn-success cancel glyphicon glyphicon-edit" type="button"  data-toggle="modal" data-target="#exampleModal">

                            </button>
                        </div>
                        <div>
                        <button type="button" class="btn btn-danger  glyphicon glyphicon-trash" onclick="delrcvendor('<?php echo $rvalue->id_key ?>')"></button>


                            </div>

                </div>



          </td>


                <?php } ?>
          </tr>




        </tbody>

   <!-- FOREACH TABLE CLOSING TAGS  -->


    </table>




```


- Updated Fetching Data via Ajax way to less load time in the page

```javascript

<script>

      $(document).ready(function () {
          $('#rcVendorTable').DataTable({
              processing: true,
              serverSide: true,
              pageLength: 50, // 👈 Default page length
              lengthMenu: [[50, 200, 500, 1000, -1], [50, 200, 500, 1000, "All"]], // 👈 Dropdown options

              ajax: {
                  url: 'url/', // Your API endpoint
                  type: 'POST'
              },
              columns: [
                  {
                      data: null,
                      render: function (data, type, row, meta) {
                          return meta.row + meta.settings._iDisplayStart + 1; // Correct row numbering
                      },
                      title: "No."
                  },
                  {
                       data: 'rc_vendor_name',
                       title: 'RC Vendor Name',
                       createdCell: function (td) {
                         $(td).css('text-align', 'left');
                       }
                     },
                  {
                      data: 'id_kay',
                      title: 'Email',
                      createdCell: function (td) {
                        $(td).css('text-align', 'left');
                      },
                      render: function (data, type, row) {
                         return `<a href="#" onclick="getDetails('${data}'); return false;">${row.name_email}</a>`;
                      }
                    },

                  { data: 'user_id', title: 'User Login' },
                  { data: 'employee_names', title: 'Employee Names' },
                  { data: 'bpi_account', title: 'BPI Account' },
                  { data: 'states', title: 'States' },
              ],
              dom: 'Bfrtip',
              buttons: [
               { extend: 'copy', className: 'btn btn-sm btn-primary' },
               { extend: 'csv', className: 'btn btn-sm btn-primary' },
               { extend: 'excel', className: 'btn btn-sm btn-primary' },
               { extend: 'pdf', className: 'btn btn-sm btn-primary' },
               { extend: 'print', className: 'btn btn-sm btn-primary' }
             ],
             responsive: true,
              order: []
          });
      });

</script>

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


	```

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