<?php
/**
 ** Template Name: IGSL NEW DASHBOARD FOR STAFF PAGE 2023
 ** Desciptions: UPDATING REQUEST VIA SUPERVISOR
 ** Version: 02
 ** Date Update: 072024
 **/



 $timestamp = date("Y-m-d h:i:sa");


  /**
   *Redirect if assessed directly
   *For Security purposes
   ***/ 

  // Ensure the file is included from within the WordPress environment
    if (!defined('ABSPATH')) {
        exit;
    }


 $user = wp_get_current_user();

if(!is_user_logged_in()) {
           wp_redirect( home_url( '/wp-login.php' ), 302 );
           exit();
           }
         else{




                   //GET THE GLOBAL TEMPLATE OF WORDPRESS AND ECHO THE TEMPLATE NAME
                  //CREATING A FUNCTION THAT WILL SHOW THE TEMPLATE NAME OF THE CURRENT PAGE
                  //ONLY FOR ADMINISTRATOR ONLY.

                  function tf_check_user_role( $roles ) {
                     /*@ Check user logged-in */
                  if ( is_user_logged_in() ) :
                      /*@ Get current logged-in user data */
                      $user = wp_get_current_user();
                      /*@ Fetch only roles */
                      $currentUserRoles = $user->roles;
                      /*@ Intersect both array to check any matching value */
                      $isMatching = array_intersect( $currentUserRoles, $roles);
                      $response = false;
                      /*@ If any role matched then return true */
                      if ( !empty($isMatching) ) :
                          $response = true;
                      endif;
                      return $response;
                  endif;
              }
              $roles = [ 'administrator' ];
              if ( tf_check_user_role($roles) ) :
                      global $template;

                        echo "<h3 style='text-align: center;color:orange'>" . basename($template) . "</h3>";
              endif;




              $templatename = basename($template);



          //GET THE CURRENT USER BY USER LOGIN - USERNAME
          $currentulog = $current_user->user_login;

          // CHECK THE ROLES AND PAGE ALLOWED

            $grolescheck = $wpdb->get_results("SELECT COUNT(*) as ctnkeys FROM `igslportal_access_role` WHERE user_name = '$currentulog' AND page_allowed = '$templatename' ");

            foreach ($grolescheck as $key => $gchvalue) {

                    $gvals = $gchvalue->ctnkeys;



                  }


                  if(  $gvals  > 0 ){



                    
              //GETTING THE IPADDRESS OF THE CURRENT USER

              if ( ! empty( $_SERVER['HTTP_CLIENT_IP'] ) ) {

                //check ip from share internet
  
                $ip = $_SERVER['HTTP_CLIENT_IP'];
  
                } elseif ( ! empty( $_SERVER['HTTP_X_FORWARDED_FOR'] ) ) {
  
                //to check ip is pass from proxy
  
                $ip = $_SERVER['HTTP_X_FORWARDED_FOR'];
  
                } else {
  
                $ip = $_SERVER['REMOTE_ADDR'];
  
                }



?>


<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link
      rel="shortcut icon"
      href="https://res.cloudinary.com/dozs20to9/image/upload/v1628672919/MEDIA%20FILES%20IGSL/igsl-favicon-logo.png"
      type="image/x-icon"
    />
    <title>Supervisor TSH</title>

    <!-- ========== All CSS files linkup ========= -->
    <link rel="stylesheet" href="<?php echo plugin_dir_url( __FILE__ ) . 'plain-template-main/assets/css/bootstrap.min.css' ?>"/>
    <link rel="stylesheet" href="<?php echo plugin_dir_url( __FILE__ ) . 'plain-template-main/assets/css/lineicons.css' ?>" />
    <link rel="stylesheet" href="<?php echo plugin_dir_url( __FILE__ ) . 'plain-template-main/assets/css/materialdesignicons.min.css'?>" />
    <link rel="stylesheet" href="<?php echo plugin_dir_url( __FILE__ ) . 'plain-template-main/assets/css/fullcalendar.css'?>" />
    <link rel="stylesheet" href="<?php echo plugin_dir_url( __FILE__ ) . 'plain-template-main/assets/css/fullcalendar.css'?>" />
    <link rel="stylesheet" href="<?php echo plugin_dir_url( __FILE__ ) . 'plain-template-main/assets/css/main.css'?>" />
    <link rel="stylesheet" href="<?php echo plugin_dir_url( __FILE__ ) . 'simplepicker-main/dist/simplepicker.css'?>" />


    <!-- SUPERVISOR APPORVAL CSS LINK -->
    <link rel="stylesheet" href="<?php echo plugin_dir_url( __FILE__ ) . 'css/supervisor_approval.css'?>" />


   <!-- IGSL CSS SELF HOST CDN -->

        <link rel="stylesheet" href="https://cdn.igsl.asia/igsl-css/flatpickr.min.css">
        <link rel="stylesheet" href="https://cdn.igsl.asia/igsl-css/fontawesome.6.2.1.min.css">
        <link rel="stylesheet" href="https://cdn.igsl.asia/igsl-css/jquery.dataTables.css">
        <link rel="stylesheet" href="https://cdn.igsl.asia/igsl-css/magicpopup.css">
        <link rel="stylesheet" href="https://cdn.igsl.asia/igsl-css/responsive.dataTables.min.css">
        <link rel="stylesheet" href="https://cdn.igsl.asia/igsl-css/rowReorder.dataTables.min.css">
        <link rel="stylesheet" href="https://cdn.igsl.asia/igsl-css/select2.css">


     <!-- IGSL CSS SELF HOST CDN END HERE-->



     <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
     <link rel="stylesheet"   href= "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">



<style media="screen">


</style>


<script src="<?php echo plugin_dir_url( __FILE__ ) . 'simplepicker-main/dist/simplepicker.js'?>" ></script>


<?php


  //ADDING DEFAULT DESIGN AND CALL IT
  require_once $_SERVER['DOCUMENT_ROOT'] . '/wp-content/plugins/igsldashboard_lister/templates/mainheaderfooter/mainheader.php';
  


?>



<body >





<input  type="hidden" id="gcurrentuserid" value="<?= $current_user->user_login ?>">


 <div class="overlay"></div>
 <!-- ======== sidebar-nav end =========== -->

 <!-- ======== main-wrapper start =========== -->
 <main class="main-wrapper">
   <!-- ========== header start ========== -->

                
        <?php
        
           //ADDING HEADER AND CALL
            require_once $_SERVER['DOCUMENT_ROOT'] . '/wp-content/plugins/igsldashboard_lister/templates/all_headers/supervisor_approval_header.php';
        
        ?>

   <!-- ========== header end ========== -->

    <!-- ========== section start ========== -->
    <section class="section">
      <div class="container-fluid">
        <!-- ========== title-wrapper start ========== -->
        <div class="title-wrapper pt-30">
          <div class="row align-items-center">
            <div class="col-md-6">
              <div class="title mb-30">
                <h2> Administrator Dashboard</h2>
              </div>
            </div>
            <!-- end col -->
            <div class="col-md-6">
              <div class="breadcrumb-wrapper mb-30">
                <nav aria-label="breadcrumb">
                  <ol class="breadcrumb">
                    <li class="breadcrumb-item">
                      <a href="#0">Dashboard</a>
                    </li>
                    <li class="breadcrumb-item active" aria-current="page">
                      admin-dashboard
                    </li>
                  </ol>
                </nav>
              </div>
            </div>
            <!-- end col -->
          </div>
          <!-- end row -->
        </div>
        <!-- ========== title-wrapper end ========== -->



                    <!-- START FOR DATE ROW -->

                    <div class="row">
                      <div class="col-lg-12">
                        <div class="card-style mb-30">
                          <div class="title d-flex flex-wrap justify-content-between">




                              <h2 class="text-medium lg-7">

                                <?php
                                    $timezone  = + 8; //(GMT +8:00) Philippines
                                    $timenow = gmdate("H", time() + 3600*($timezone+date("I")));
                                    $wekkday = gmdate("l", time() + 3600*($timezone+date("I")));
                                    $manilatimenow = gmdate("Y", time() + 3600*($timezone+date("I")));
                                    $manilatimenowd = gmdate("F d", time() + 3600*($timezone+date("I")));
                                    // $timenow = 17;
                                    //$timeonly = gmdate("h:m:s", time() + 3600*($timezone+date("h:m:s")));
                                    // echo $timenow;

                                    if($timenow >= 24 || $timenow < 13){
                                      $clocknow = "Good Morning";
                                      } elseif($timenow === 13 || $timenow < 18 ) {
                                          $clocknow = "Good Afternoon";
                                      }elseif($timenow === 18 || $timenow <= 24){
                                          $clocknow = "Good Evening";
                                      }


                                      // Set the new timezone
                                      date_default_timezone_set('Asia/Manila');
                                      $timeonly = date('h:i:s');





                                  ?>




                                </h2><br>



                              <br>


                              <div  class="mobif" style="width: 100%;" >

                                <div style="background-color: #fbbe28;">
                                  <h2 class="mobiftext" style="text-align: center; font-size: 5rem; font-weight: bolder;color: #ffff"><?= $wekkday?></h2>
                                  <p class="mobiftext linehe" style="text-align: center;font-weight: bolder;font-size: 3rem;color:#1b3f75"><?= $manilatimenowd ?></p>
                                </div>
                                <div  style=" " >
                                    <h2 class="mobiftext" style="text-align: center; font-size: 5rem; font-weight: bolder;color: #fbbe28"><?= $manilatimenow?></h2>
                                    <div style="font-size: 3rem; text-align: center;color:#545271; font-weight: bolder; vertical-align: center; "  id="MyClockDisplay" onload="showTime()"></div>

                                </div>

                              </div>



                          </div>
                          <!-- End Title -->

                          <!-- End Chart -->
                        </div>
                      </div>


                         <!-- END FOR DATE ROW -->
                    </div>



                            <div class="row">
                                <div class="col-lg-12">
                                <div class="card-style mb-30">
                                    <div
                                    class="
                                        title
                                        d-flex
                                        flex-wrap
                                        align-items-center
                                        justify-content-between
                                    "
                                    >
                                    <div class="left">
                                 
                                        <?php 
           
                 
                 
                                         /**
                                         ** ADDING FUNCTIONS FOR MULTIPLE DAYS
                                         **/


                                         $curresupv = $current_user->user_login;

                                         $tstimesheetsrec = $wpdb->get_results("SELECT * FROM `supervisor_timesheet_view` WHERE Supervisors = '$curresupv' ");
                                         foreach ($tstimesheetsrec as $key => $thvalue) {
                                             $timesheetsmonth =  $thvalue->Month; // MONTH SELECTED
                                             $gyearselect = $thvalue->YearOnly; //YEAR SELECTED

                                         }



                                        //GET THE DATA FROM THE DB



                                         /**
                                         ** GET THE CURENT YEAR, MONTH AND DAY FOR DISPLAYING THE SPECIFIC
                                         ** LIST OF REQUESTS OF THE STAFF VIA SUPERVISOR SELECT
                                         **/

                                         /**
                                         ** PH TIMEZONES AND GET ONLY YEAR
                                         **/


                                         $timezone  = + 8; //(GMT +8:00) Philippines
                                        

                                         /**
                                          * THE NEW PATCH UPDATE 072024
                                          * WE REMOVE THE PERIOD CUT OFF FOR SUPERVISORS
                                          * WHO APPROVING VIA EITHER 1-15 OR 16 - 30
                                          * THE NEW UPDATE WILL ONLY CHANGE TO 1 - 30
                                          * SO THAT THE SUPERIVOR CAN EASILY SEE
                                          * ALL THE STAFF LIST OF REQUESTS PER MONTH
                                          */

                                         $gmonth = $timesheetsmonth;
                                         $ydatesonly = $gyearselect;

                                                            
                                        /**
                                        * THIS UPDATE INTRODUCES NEW FUNCTIONALITIES TO THE SUPERVISOR PAGE:
                                        *
                                        * ENHANCED MONTHLY DISPLAY: THE DISPLAYED MONTH WILL NOW INCLUDE BOTH 
                                        * THE MONTH NAME AND THE YEAR FOR BETTER USER CLARITY.
                                        *
                                        * INTERNAL DATE RANGE: WHILE ONLY THE MONTH AND YEAR ARE SHOWN, THE FUNCTION 
                                        * INTERNALLY MAINTAINS A DATE RANGE FROM THE 1ST TO THE 31ST OF THE DISPLAYED MONTH. 
                                        * THIS ALLOWS FOR FUNCTIONALITIES THAT REQUIRE THE FULL DATE RANGE WITHOUT CLUTTERING THE USER INTERFACE.
                                        *
                                        * VERSION CONTROL UPDATE: 072024 (JULY 2024)
                                        */




                                        /**
                                        ** GET THE CURENT YEAR, MONTH AND DAY FOR DISPLAYING THE SPECIFIC
                                        ** LIST OF REQUESTS OF THE STAFF VIA SUPERVISOR SELECT
                                        **/

                              
                                        //GET CURRENT ID
                                        $curid = $current_user->user_login;




                                        //GET THE DATA FROM THE DB



                                        /**
                                        ** GET THE CURENT YEAR, MONTH AND DAY FOR DISPLAYING THE SPECIFIC
                                        ** LIST OF REQUESTS OF THE STAFF VIA SUPERVISOR SELECT
                                        **/

                                        /**
                                        ** PH TIMEZONES AND GET ONLY YEAR
                                          **/

                                        $timezone  = + 8; //(GMT +8:00) Philippines
                                        $ydatesonly = gmdate("Y", time() + 3600*($timezone+date("I")));

                                      

                                        $samplefuls = gmdate("m/d/Y H:i", time() + 3600*($timezone+date("I")));


                                        /**
                                        * GET THE SUPERVISOR SELECTED
                                        * YEAR AND MONTH 
                                        */

                                        $gmonth = $timesheetsmonth;
                                        $gselecyrs = $gyearselect;
                    

                                        /**
                                        ** CREATE ARRAY TO SIMPLY THE MONTH AND CUTOFF CODES
                                        **/


                                        $worldmonths = array(

                                        "January","February", "March", "April" ,"May" , "June", "July", "August", "September", "October" , "November", "December"
                                        );

                                        foreach ($worldmonths as $keys => $gvalmonth) {

                                          /**
                                          ** GET ONLY IN THE LOOP THE SAME MONTH
                                          **/

                                          if($gmonth == $gvalmonth){



                                                      /**
                                                      ** AFTER GEETING THE KEY VALUES
                                                      ** ADD PLUS 1 AND CREATE THE CUTOFFS
                                                      **/

                                                      $gkeysvals = $keys + 1;

                                                      /**
                                                      ** ADD ZERO AT THE BEGINNING IF BELOW 10
                                                      **/

                                                      if($gkeysvals < 10){

                                                        $addzerob = "0" . $gkeysvals;

                                                      }else{

                                                        $addzerob = $gkeysvals;
                                                      }


                                                        $fmonthday = $addzerob . "/01/" . $gyearselect;
                                                        $ldayofmst = $addzerob . "/31/".$gyearselect;

                                                        $startdates = $addzerob . "/01/" . $gyearselect;
                                                        $endsts =  $addzerob . "/31/".$gyearselect;



                                                    }//CLOSING FOR MONTH ARRAY NUMBER KEY
                                                }//CLOSING FOR MONTLY ARRAY
                                        

                                                /**
                                                * FINAL DATE DURATION DISPLAY
                                                * FORMAT HERE
                                                */


                                            

                           


                                        /**
                                        * VERSION CONTROL
                                        *  UPDATE END HERE
                                        * 
                                        */       
                                    


                 
                /**
                 * DISPLAYING THE CURRENT 
                 * TIMESHEET PERIODS
                 * 
                 * */                  

               ?>



               <?php
               
                /**
                 * GET THE CURRENT USER LOGIN
                 */

                  $curresupv = $current_user->user_login;

               ?>

              <h4 class="text-medium mb-2">Timesheets  Period:&nbsp;  <?php echo $timesheetsmonth ." : ". $fmonthday . " - " .$ldayofmst ?> <br>                              

                <!-- GET THE CURRENT MONTH AND CUTTOFF HERE -->


                    <input type="hidden" id="cgmonth" value="<?php echo $timesheetsmonth ?>">
                    <input type="hidden" id="gccutoffpds" value="<?php echo $timesheetscufof ?>">
                
                <br>                            
               <form  method="post">



               <select  name="yearmonth" onchange="this.form.submit()" id="month" style="text-align: center">
                   <option value="SELECT Month..">SELECT Month..</option>
                    <option value="January"     <?php if($timesheetsmonth== "January")   {echo "selected";}?>  >January</option>
                    <option value="February"    <?php if($timesheetsmonth == "February")  {echo "selected";}?> >February</option>
                    <option value="March"       <?php if($timesheetsmonth == "March")     {echo "selected";}?> >March</option>
                    <option value="April"       <?php if($timesheetsmonth == "April")     {echo "selected";}?> >April</option>
                    <option value="May"         <?php if($timesheetsmonth == "May")       {echo "selected";}?> >May</option>
                    <option value="June"        <?php if($timesheetsmonth == "June")      {echo "selected";}?> >June</option>
                    <option value="July"        <?php if($timesheetsmonth== "July")      {echo "selected";}?> >July</option>
                    <option value="August"      <?php if($timesheetsmonth == "August")    {echo "selected";}?> >August</option>
                    <option value="September"   <?php if($timesheetsmonth == "September") {echo "selected";}?> >September</option>
                    <option value="October"     <?php if($timesheetsmonth == "October")   {echo "selected";}?> >October</option>
                    <option value="November"    <?php if($timesheetsmonth == "November")  {echo "selected";}?> >November</option>
                    <option value="December"    <?php if($timesheetsmonth == "December")  {echo "selected";}?> >December</option>
               </select>

              <!-- SELECTING TIMESHEET GET THIS HIDDEN MONTH AND CUTOFF -->

               <input type="hidden" id="gmonth">
               <input type="hidden" id="ggcutoff">

               <select name="gyearview" onchange="this.form.submit()" id="dbetween" style="text-align: center">
                    <option value=" ">SELECT Year</option>


                      <?php

                            //CREATE INCREMENTED YEAR

                            $yearnow = gmdate("Y", time() + 3600*($timezone+date("I")));


                        ?>




                        <option value='2023' <?php if($gyearselect == '2023' )  { echo "selected"; } ?> > 2023 </option>
                        <option value='<?php echo $yearnow ?>' <?php  if($gyearselect == '2024' )  {  echo "selected";} ?> > <?php echo $yearnow?> </option>





                      ?>


                 </select>

                <input type="hidden" name="gcurresupv" value="<?= $curresupv ?>">
                <input name="form_nonce" type="hidden" value="<?=wp_create_nonce('staff-nonce')?>" />
               


               </form> 


             </div>
             <div class="left">
               <h4 class="text-medium mb-2"></h4>
             </div>


               <div class="right">
                 <div class="select-style-1 mb-2">
                       <p style="color:red; font-style: normal; ">We're making improvements to this page. Stay tuned for the new update!</p>               
                 </div>
                 <!-- end select -->
               </div>
             </div>
             <!-- End Title -->

             <?php

                //GET THE CURRENT ROLE OF THE USER INSIDE ULTIMATE MEMBER PLUGIN

               $current_user = wp_get_current_user();

                //FETCHING THE USER USING THE ID

                //  um_fetch_user( $current_user->ID );

                //DISPLAY ROLE
                //  echo   UM()->user()->get_role();

                // //Change user role
                // echo  UM()->roles()->set_role(3,'um_staff');

                $curidpros = $current_user->user_login;

                /*
                * GET STAFF UNDER SUPERVISOR LIST
                **/


                $staffilist = $wpdb->get_results("SELECT userid,  FROM `staff_almost_fullrecords` WHERE supervisors ='$curidpros' AND inactive ='No' ");

                foreach ($staffilist as $key => $crfvalue) {

                    $csupervisor = $crfvalue->userid;
                }





                    /**
                     * INSERTING A RECORD TO TMP TBL TO OPEN THE
                     * SIDE BAR OR THE PAGE DIRECT TO SPECIFIC 
                     * USER VIEW
                     */

                     $current_url = get_permalink(); //GET THE CURRENT URL PAGE

                     /**
                      * DELETE FIRST THE TEMP RECORDS 
                      * OF THE USER VIEW PAGE 
                      */
                     $delfirst = $wpdb->query($wpdb->prepare("DELETE FROM tmp_userview_currentpage WHERE user_ids ='$curid' "));

                     /**
                      * INSERT NEW RECORD TO THE TBL
                      */
                     $insernow = $wpdb->insert("tmp_userview_currentpage" ,array('user_view_page' => $current_url, 'user_ids'=> $curid));

                     


                 ?>
                

                                            <br>
                                            <h4>DTR Request List</h4>

                

                          <input type="hidden" id="gstaffidlist"  value="<?php echo $curidpros ?>">

                           <table  id="tbdtrrequestlist" style="width: 100%" >
                            <thead>

                            <tr>
                                <th>IDKY</th>
                                <th>Staff</th>
                                <th>Request Type</th>
                                <th>Dtr Time In</th>
                                <th>Dtr Time Out</th>
                                <th>Reasons</th>
                                <th>Date Filed</th>
                                <th>Status</th>
                                <th>Action</th>
                            </tr>


                            </thead>
                            <tbody >



                                        <?php



                                            $gyearselect  = $ydatesonly;   

                                        /**
                                        ** GET DTR LIST VIA SUPERVISOR
                                        **/

                                        $currensupvs = $current_user->user_login;
 


                                        /**
                                        ** GET ONLY DATE FROM THE FMONTH AND LAMONTH
                                        **/



                                        $gcurrentslits = $wpdb->get_results("SELECT userid,Name FROM `staff_almost_fullrecords` WHERE supervisors ='$currensupvs' AND ( inactive ='No' OR supervisors='$currensupvs') ");
                                       
                                        foreach ($gcurrentslits as $key => $sffvalue) {

                                            //SUPERVISOR LIST OF STAFF UNDER THEM

                                            $supstaflist = $sffvalue->userid; 

                                        



                                            /**
                                            ** PH TIMEZONES AND GET CURRENT DATE 
                                            **/

                                        $timezone  = + 8; //(GMT +8:00) Philippines
                                        $dtrnydatesonly = gmdate("m/d/Y", time() + 3600*($timezone+date("I")));

                                            
                                            


                                        $gallsupstafli = $wpdb->get_results("SELECT * FROM `staff_dtr_request_tabs`  WHERE staff_id = '$supstaflist'  AND datefiled BETWEEN  '$startdates' AND '$dtrnydatesonly' AND approval != 'WITHDRAW' AND YEAR(STR_TO_DATE(datefiled, '%m/%d/%Y')) = '$gyearselect'  ");
                                       
                                        foreach ($gallsupstafli as $key => $stfavalue) {

                                            $dtrstaffid = $stfavalue->staff_id;
                                            $request_type = $stfavalue->request_type;
                                            $dtr_timeout = $stfavalue->dtr_timeout;
                                            $dtr_timein = $stfavalue->dtr_timein;
                                            $reasons = $stfavalue->reasons;
                                            $approval = $stfavalue->approval;
                                            $datefiled = $stfavalue->datefiled;
                                            $idkey =  $stfavalue->idkey;

                                            if($approval == NULL){
                                            $echol = "PENDING";
                                            }else{
                                            $echol = $approval;
                                            }

                                            $gcreatedtrs = date_create($dtr_timein);
                                            $fnldrst = date_format($gcreatedtrs, "m/d/Y");


                                            $ggcreatedtrs = date_create($dtr_timeout);
                                            $ffnldrst = date_format($ggcreatedtrs, "m/d/Y");







                                        ?>
                                        <tr>
                                        <td><?= ++$count; ?></td>
                                        <td style="text-align: left; padding-left: 1%;width: auto">




                                            <?php


                                            /**
                                             ** DISPLAY STAFF FULLNAME
                                            **/

                                            $staffnames = $sffvalue->Name;
                                                echo   $staffnames;

                                             

                                            ?>



                                        </td>
                                        <td><?= $request_type; ?></td>
                                        <td><?= $dtr_timein; ?></td>
                                        <td><?= $dtr_timeout; ?></td>
                                        <td><?= $reasons; ?></td>
                                        <td><?= $datefiled; ?></td>
                                        <td><?= $approval; ?></td>

                                            <td>




                                            <form method="post">

                                                <input <?= $checbtns ?> type="hidden" name="dtrstflist[]" value="<?= $dtrstaffid ?>">
                                                <input type="hidden" name="getditfiled[]" value="<?= $idkey ?>">
                                                <input type="hidden" name="dtrtimein[]" value="<?=  $dtr_timein  ?> ">
                                                <input type="hidden" name="dtrtimeout[]" value="<?=  $dtr_timeout  ?> ">
                                                <input type="hidden" name="requestyps[]" value="<?=  $request_type  ?> ">

                                                    <input name="form_nonce" type="hidden" value="<?=wp_create_nonce('staff-nonce')?>" />

                                                    <?php

                                                    if($approval == 'APPROVED' || $approval == 'WITHDRAW' ||  $approval == 'DISAPPROVED'){

                                                        $btndisabled = "disabled";

                                                    }else {
                                                        $btndisabled = "";
                                                    }


                                                    ?>


                                                    <button <?= $btndisabled; ?> type="submit" name="dtrapproved" class="btn btn-success">

                                                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-check2" viewBox="0 0 16 16">
                                                            <path d="M13.854 3.646a.5.5 0 0 1 0 .708l-7 7a.5.5 0 0 1-.708 0l-3.5-3.5a.5.5 0 1 1 .708-.708L6.5 10.293l6.646-6.647a.5.5 0 0 1 .708 0z"/>
                                                        </svg>

                                                        </button>
                                                    <button   type="submit" name="dtrdisapproved" class="btn btn-danger">
                                                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-x" viewBox="0 0 16 16">
                                                    <path d="M4.646 4.646a.5.5 0 0 1 .708 0L8 7.293l2.646-2.647a.5.5 0 0 1 .708.708L8.707 8l2.647 2.646a.5.5 0 0 1-.708.708L8 8.707l-2.646 2.647a.5.5 0 0 1-.708-.708L7.293 8 4.646 5.354a.5.5 0 0 1 0-.708z"/>
                                                    </svg>
                                                    </button>

                                            </form>




                                            </td>



                                        </tr>

                                        <?php


                                        } // END LOOP FOR THE DTR REQUEST LIST
                                        } //END LOOP FOR THE SUPERVISOR STAFF LIST




                                        ?>

                                    </tbody>
                                   

                                      


                                <?php

        

                                    /**
                                    ** UPDATING THE STAFF RECORDS VIA RELOAD
                                    ** GET APPROVED BY SUPERVISOR IN DTR TABS
                                    ** GET DTR LIST VIA SUPERVISOR
                                    **/

                                    $currensupvs = $current_user->user_login;

                                    $gcurrentslits = $wpdb->get_results("SELECT userid FROM `staff_almost_fullrecords` WHERE supervisors ='$currensupvs' AND ( inactive ='No' OR supervisors='$currensupvs') ");
                                    foreach ($gcurrentslits as $key => $sffvalue) {

                                        $supstaflist = $sffvalue->userid;



                                    $dtrapproveds = $wpdb->get_results("SELECT * FROM `staff_dtr_request_tabs`  WHERE staff_id ='$supstaflist' AND approval = 'APPROVED' AND datefiled  BETWEEN  '$startdates' AND '$dtrnydatesonly' AND YEAR(STR_TO_DATE(datefiled, '%m/%d/%Y')) = '$gyearselect'");
                                   
                                    foreach ($dtrapproveds as $key => $gvlvalue) {

                                            $requestypes = $gvlvalue->request_type;
                                            $dtr_timein  = $gvlvalue->dtr_timein;
                                            $dtr_timeout  = $gvlvalue->dtr_timeout;
                                            $staff_id = $gvlvalue->staff_id;
                                            $user_action  =  $gvlvalue->user_action;


                                            /**
                                             * DO CHECKING OF DATA IF NULL OR NOT
                                             */

                                             if(!empty($dtr_timein)){

                                            /**
                                             * DO CHECKING IF THIS DATE ALREADY 
                                             * EXIST TO NCRECORDS THE TEMP TBL 
                                             * FOR ALL THE STAFF ONLINE TAP OR 
                                             * QRCODE TAP
                                             */

                                             /**
                                              * DO ENCODING FIRST THEN CHECK THE DATES
                                              */

                                            $encodeuid = str_rot13($staff_id);

                                            $dtr_timein  = $gvlvalue->dtr_timein;

                                            /**
                                             * CREATE DATE FOR INSERTING NEW
                                             * RECORDS TBL COLUMN NEED
                                             */

                                             $cdtrdates = date_create($dtr_timein);
                                             $dcformats = date_format($cdtrdates,"m/d/Y");

                                            $glistcheck = $wpdb->get_results("SELECT COUNT(dates) AS existdtx FROM `nrecording_staff_timesheets_records` WHERE staff_id ='$encodeuid' AND  clock_in_out='$dtr_timein' ");
                                            foreach ($glistcheck as $valuxe) {

                                                if($valuxe->existdtx > 0){
                                                
                                                }else{

                                                            /**
                                                             ** INSERT  SPECIFIC DATE
                                                            **/

                                                            $nulls = NULL;
                                                            $wholedcheckr = "DTRIN_APPROVED";
                                                            $gonlyhours = NULL;
                                                            $fcalcsidkey = $calcsidkey * 2;

                                                            $timeid="TSH". gmdate("h", time() + 3600*($timezone+date("I"))) . $fcalcsidkey;

                                                                $sqedl = $wpdb->insert("nrecording_staff_timesheets_records",
                                                                array(
                                                                   'timesheet_id' => $timeid,
                                                                     'dates'     => $dcformats,
                                                                     'clock_in_out' => $dtr_timein,
                                                                     'late' => $nulls,
                                                                     'undertime' => $nulls,
                                                                     'regular' => $nulls,
                                                                     'overtime' => $nulls,
                                                                     'total' => $nulls,
                                                                     'ot_total_hours' => $nulls,
                                                                     'total_hours' => $nulls,
                                                                     'status' => $nulls,
                                                                     'staff_id' => $encodeuid,
                                                                     'daybreak' => $wholedcheckr
                                                                ));

                                                }//CLOSING TAG IF NO DATA DUPLICATE OR EXIT INSERT NEW RECORDS TO NCRECORDS                                        
                                            }//CLOSING FOR LISTING AND CHECKING IF CLOCK IN OUT EXIST OR NOT

                                           


                                             }elseif(!empty($dtr_timeout)){


                                                /**
                                             * DO CHECKING IF THIS DATE ALREADY 
                                             * EXIST TO NCRECORDS THE TEMP TBL 
                                             * FOR ALL THE STAFF ONLINE TAP OR 
                                             * QRCODE TAP
                                             */

                                             /**
                                              * DO ENCODING FIRST THEN CHECK THE DATES
                                              */

                                            $encodeuid = str_rot13($staff_id);

                                            $dtr_timeouta  = $gvlvalue->dtr_timeout;

                                            /**
                                             * CREATE DATE FOR INSERTING NEW
                                             * RECORDS TBL COLUMN NEED
                                             */

                                             $cdtrdateso = date_create($dtr_timeout);
                                             $dcformatso = date_format($cdtrdateso,"m/d/Y");

                                            $glistcheck = $wpdb->get_results("SELECT COUNT(dates) AS existdtx FROM `nrecording_staff_timesheets_records` WHERE staff_id ='$encodeuid' AND  clock_in_out='$dtr_timeouta' ");
                                            foreach ($glistcheck as $valuxe) {

                                                if($valuxe->existdtx > 0){
                                                
                                                }else{

                                                            /**
                                                             ** INSERT  SPECIFIC DATE
                                                            **/

                                                            $nulls = NULL;
                                                            $wholedcheckr = "DTROUT_APPROVED";
                                                            $gonlyhours = NULL;
                                                            $fcalcsidkey = $calcsidkey * 2;

                                                            $timeid="TSH". gmdate("h", time() + 3600*($timezone+date("I"))) . $fcalcsidkey;

                                                                $sqedl = $wpdb->insert("nrecording_staff_timesheets_records",
                                                                array(
                                                                   'timesheet_id' => $timeid,
                                                                     'dates'     => $dcformatso,
                                                                     'clock_in_out' => $dtr_timeouta,
                                                                     'late' => $nulls,
                                                                     'undertime' => $nulls,
                                                                     'regular' => $nulls,
                                                                     'overtime' => $nulls,
                                                                     'total' => $nulls,
                                                                     'ot_total_hours' => $nulls,
                                                                     'total_hours' => $nulls,
                                                                     'status' => $nulls,
                                                                     'staff_id' => $encodeuid,
                                                                     'daybreak' => $wholedcheckr
                                                                ));

                                                    }//CLOSING TAG IF NO DATA DUPLICATE OR EXIT INSERT NEW RECORDS TO NCRECORDS                                        
                                                }//CLOSING FOR LISTING AND CHECKING IF CLOCK IN OUT EXIST OR NOT



                                             }//CLOSING TAG FOR CHECKING IF EMPTY OR NOT THE DTR IN OR OUT
                                         }//CLOSING FOR STAFF DTR TBL LIST
                                      }//CLOSING TAG FOR GETTING ALL THE STAFF WHO ARE LISTED UNDER THE SUPERVISOR

                                                       

                                                     



                               ?>

                             </tbody>

                           </table>









           </div>
         </div>
         <!-- End Col -->





         <!-- End Col -->
       </div>
       <!-- End Row -->
       <br>
       <!-- LEAVE REQUEST LIST -->
       <div class="row">
         <div class="col-lg-12">
           <div class="card-style mb-30">
             <div
               class="
                 title
                 d-flex
                 flex-wrap
                 align-items-center
                 justify-content-between
               "
             >
             <div class="left">
               <h4 class="text-medium mb-2">Leave Request List</h4>
             </div>
             <div class="left">

             </div>

               <div class="right">
                 <div class="select-style-1 mb-2">

                 </div>
                 <!-- end select -->
               </div>
             </div>
             <!-- End Title -->


              <table  style="width: 100%" id="leavefile" class="">
                <thead>
                    <th>IDK</th>

                    <th>Staff ID</th>
                    <th>Request Type</th>
                    <th>Type</th>
                    <th>Start Date</th>
                    <th>End Date</th>
                    <th>Reasons</th>

                    <th>Status</th>

                    <th>Actions</th>


                </thead>
                <tbody >
                  <?php





                    /**
                    ** GET DTR LIST VIA SUPERVISOR
                    **/

                    $currensupvs = $current_user->user_login;

                    $gcurrentslits = $wpdb->get_results("SELECT userid, Name FROM `staff_almost_fullrecords` WHERE supervisors ='$currensupvs' AND ( inactive ='No' OR supervisors='$currensupvs') ");
                    foreach ($gcurrentslits as $key => $sffvalue) {

                        $supstaflist = $sffvalue->userid;



                     /**
                       ** GET THE CURENT YEAR, MONTH AND DAY FOR DISPLAYING THE SPECIFIC
                       ** LIST OF REQUESTS OF THE STAFF VIA SUPERVISOR SELECT
                       **/




                     /**
                     ** START DATE RECREATE
                     **/
                     $recreatedate = date_create($fmonthday);
                     $displaystart = date_format($recreatedate, "m/d/Y H:i");



                  /**
                  ** END DATE RECREATE
                  **/


                



                  $endrecteae = date_create($ldayofmst);
                  $endrecsf = date_format($endrecteae, "Y-m-d");


                   $gallsupstafli = $wpdb->get_results("SELECT * FROM `staff_leave_request_tbl`  WHERE staff_id = '$supstaflist' AND datefiled BETWEEN '$fmonthday' AND '$ldayofmst' AND YEAR(STR_TO_DATE(datefiled, '%m/%d/%Y')) = '$gyearselect' ");
                   foreach ($gallsupstafli as $key => $leavvals) {

                     $leavstaffid = $leavvals->staff_id;
                     $request_type = $leavvals->leave_request_type;
                     $day_schedule_half_whole = $leavvals->day_schedule_half_whole;
                     $start_date = $leavvals->start_date;
                     $end_date = $leavvals->end_date;
                     $reasons = $leavvals->reasons;
                     $admin_status = $leavvals->admin_status;
                     $datefiled = $leavvals->datefiled;






                  ?>
                  <tr>
                    <td><?= ++$countsss; ?></td>
                    <td style="text-align: left">


                    <?php

                        echo $sffvalue->Name;

                    ?>


                    </td>
                    <td><?= $request_type; ?></td>
                    <td><?= $day_schedule_half_whole; ?></td>
                    <td><?= $start_date; ?></td>
                    <td><?= $end_date; ?></td>
                    <td><?= $reasons; ?></td>

                    <td><?= $admin_status; ?></td>
                    <td>




                      <form method="post">

                            <input <?= $checbtns ?> type="hidden" name="leavefist[]" value="<?= $leavstaffid ?>">
                            <input type="hidden" name="getditfiled[]" value="<?= $datefiled ?>">
                            <input name="form_nonce" type="hidden" value="<?=wp_create_nonce('staff-nonce')?>" />

                            <?php

                                if($admin_status == 'APPROVED' || $admin_status == 'DISAPPROVED' || $admin_status == 'WITHDRAW'){

                                    $btndisabled = "disabled";

                                }else {
                                    $btndisabled = "";
                                }

                            ?>


                            <button <?= $btndisabled; ?> type="submit" name="levapproved" class="btn btn-success">

                              <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-check2" viewBox="0 0 16 16">
                                    <path d="M13.854 3.646a.5.5 0 0 1 0 .708l-7 7a.5.5 0 0 1-.708 0l-3.5-3.5a.5.5 0 1 1 .708-.708L6.5 10.293l6.646-6.647a.5.5 0 0 1 .708 0z"/>
                                  </svg>

                                </button>
                            <button  type="submit" name="levdisapproved" class="btn btn-danger">
                              <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-x" viewBox="0 0 16 16">
                              <path d="M4.646 4.646a.5.5 0 0 1 .708 0L8 7.293l2.646-2.647a.5.5 0 0 1 .708.708L8.707 8l2.647 2.646a.5.5 0 0 1-.708.708L8 8.707l-2.646 2.647a.5.5 0 0 1-.708-.708L7.293 8 4.646 5.354a.5.5 0 0 1 0-.708z"/>
                              </svg>
                            </button>

                      </form>




                    </td>


                  </tr>

                  <?php
                      } // END LOOP FOR THE LEAVE REQUEST LIST
                    } //END LOOP FOR THE SUPERVISOR STAFF LIST


                        /**
                        ** ADD THE LEAVE REQUEST ONLY APPROVED
                        **/

                        $gleaveapprovs = $wpdb->get_results("SELECT * FROM `staff_leave_request_tbl`  WHERE staff_id = '$supstaflist' AND datefiled BETWEEN '$fmonthday' AND '$ldayofmst' AND admin_status = 'APPROVED'  AND YEAR(STR_TO_DATE(datefiled, '%m/%d/%Y')) = '$gyearselect'");


                        foreach ($gleaveapprovs as $key => $gleavsdply) {



                                  /**
                                  ** GET ONLY SICK LEAVE THAT ARE NOT WITHOUTH PAY
                                  **/

                                  $leavereqctypes = $gleavsdply->leave_request_type;

                                  if($leavereqctypes == 'VACATIONLEAVE_WITHOUTPAY' || $leavereqctypes == 'SICKLEAVE_WITHOUTPAY'){


                                  }else{


                                                            /**
                                                             ** GET ALL STAFF LEAVE REQUEST DATA
                                                            **/

                                                            $dstart_date = $gleavsdply->start_date;
                                                            $dend_date = $gleavsdply->end_date;
                                                            $stafidds = $gleavsdply->staff_id;


                                                            /**
                                                             ** CREATE DATE THAT WILL EQUAL TO STAFF TIMESHEETS RECORDS
                                                            **/

                                                            /**
                                                             ** START DATE
                                                            **/
                                                            $cgdateonly = date_create($dstart_date);
                                                            $cgfdateapp = date_format($cgdateonly, 'm/d/Y');

                                                            /**
                                                             ** END DATE
                                                            **/
                                                            $ecgdateonly = date_create($dend_date);
                                                            $ecgfdateapp = date_format($ecgdateonly, 'm/d/Y');



                                                                  




                                                            /**
                                                            ** CHECK IF THE DATE SELECTED ALREADY EXIST OF NOT
                                                            **/


        

                                                            /**
                                                            ** UPDATING THE STAFF RECORDS VIA RELOAD
                                                            ** GET APPROVED BY SUPERVISOR IN LEAVE TABS
                                                            ** GET LEAVE LIST VIA SUPERVISOR
                                                            **/
                        
                                                            $currensupvs = $current_user->user_login;
                        
                                                            $gcurrentslits = $wpdb->get_results("SELECT userid FROM `staff_almost_fullrecords` WHERE supervisors ='$currensupvs' AND ( inactive ='No' OR supervisors='$currensupvs') ");
                                                            foreach ($gcurrentslits as $key => $sffvalue) {
                        
                                                                $supstaflist = $sffvalue->userid;
                        
                        
                        
                                                            $dtrapproveds = $wpdb->get_results("SELECT * FROM `staff_leave_request_tbl`  WHERE staff_id ='$supstaflist' AND admin_status = 'APPROVED' AND datefiled  BETWEEN  '$startdates' AND '$currdaywhrs' AND YEAR(STR_TO_DATE(datefiled, '%m/%d/%Y')) = '$gyearselect'");
                                                           
                                                            foreach ($dtrapproveds as $key => $gvlvalue) {
                        
                                                                    $requestypes = $gvlvalue->day_schedule_half_whole;
                                                                    $start_date  = $gvlvalue->start_date;
                                                                    $end_date  = $gvlvalue->end_date;
                                                                    $staff_id = $gvlvalue->staff_id;
                                                                    $user_action  =  $gvlvalue->user_action;
                        
                        
                                                                    /**
                                                                     * DO CHECKING OF DATA IF FILED
                                                                     * LEAVE IS WHOLE DAY OR HALF DAY
                                                                     */
                        
                                                                     if($requestypes == 'Whole Day'){
                        
                                                                        /**
                                                                         * DO CHECKING IF THIS DATE ALREADY 
                                                                         * EXIST TO NCRECORDS THE TEMP TBL 
                                                                         * FOR ALL THE STAFF ONLINE TAP OR 
                                                                         * QRCODE TAP
                                                                         */
                            
                                                                        /**
                                                                         * DO ENCODING FIRST THEN CHECK THE DATES
                                                                        */
                            
                                                                        $encodeuid = str_rot13($staff_id);
                            
                                                                        $start_date  = $gvlvalue->start_date;
                                                                        $end_date  = $gvlvalue->end_date;
                            
                                                                        /**
                                                                         * CREATE DATE FOR INSERTING NEW
                                                                         * RECORDS TBL COLUMN NEED
                                                                         */
                            
                                                                        $cleaves = date_create($start_date);
                                                                        $cleavehrs = date_format($cleaves,"m/d/Y H:i");
                                                                        $cleadateonly = date_format($cleaves,"m/d/Y");


                            
                                                                        $glistcheck = $wpdb->get_results("SELECT COUNT(dates) AS existdtx FROM `nrecording_staff_timesheets_records` WHERE staff_id ='$encodeuid' AND  clock_in_out='$cleavehrs' ");
                                                                        foreach ($glistcheck as $valuxe) {
                            
                                                                            if($valuxe->existdtx > 0){
                                                                            
                                                                            }else{
                            
                                                                                        /**
                                                                                         ** INSERT  SPECIFIC DATE
                                                                                        **/
                            
                                                                                        $nulls = NULL;
                                                                                        $wholedcheckr = "WHOLEDAY_LEAVE_APPROVED";
                                                                                        $gonlyhours = NULL;
                                                                                        $fcalcsidkey = $calcsidkey * 2;
                            
                                                                                        $timeid="TSH". gmdate("h", time() + 3600*($timezone+date("I"))) . $fcalcsidkey;
                            
                                                                                            $sqedl = $wpdb->insert("nrecording_staff_timesheets_records",
                                                                                            array(
                                                                                            'timesheet_id' => $timeid,
                                                                                                'dates'     => $cleadateonly,
                                                                                                'clock_in_out' => $cleavehrs,
                                                                                                'late' => $nulls,
                                                                                                'undertime' => $nulls,
                                                                                                'regular' => $nulls,
                                                                                                'overtime' => $nulls,
                                                                                                'total' => $nulls,
                                                                                                'ot_total_hours' => $nulls,
                                                                                                'total_hours' => $nulls,
                                                                                                'status' => $nulls,
                                                                                                'staff_id' => $encodeuid,
                                                                                                'daybreak' => $wholedcheckr
                                                                                            ));
                            
                                                                            }//CLOSING TAG IF NO DATA DUPLICATE OR EXIT INSERT NEW RECORDS TO NCRECORDS                                        
                                                                        }//CLOSING FOR LISTING AND CHECKING IF CLOCK IN OUT EXIST OR NOT


                                                                         /**
                                                                         * CREATE DATE FOR INSERTING NEW
                                                                         * RECORDS TBL COLUMN NEED
                                                                         */
                            
                                                                         $cend_date = date_create($end_date);
                                                                         $ecleavehrs = date_format($cend_date,"m/d/Y H:i");
                                                                         $ecleadateonly = date_format($cleaves,"m/d/Y");
 
 
                             
                                                                         $glistcheck = $wpdb->get_results("SELECT COUNT(dates) AS eexistdtx FROM `nrecording_staff_timesheets_records` WHERE staff_id ='$encodeuid' AND  clock_in_out='$ecleavehrs' ");
                                                                         foreach ($glistcheck as $valuxe) {
                             
                                                                             if($valuxe->eexistdtx > 0){
                                                                             
                                                                             }else{
                             
                                                                                         /**
                                                                                          ** INSERT  SPECIFIC DATE
                                                                                         **/
                             
                                                                                         $nulls = NULL;
                                                                                         $wholedcheckr = "WHOLEDAY_LEAVE_APPROVED";
                                                                                         $gonlyhours = NULL;
                                                                                         $fcalcsidkey = $calcsidkey * 2;
                             
                                                                                         $timeid="TSH". gmdate("h", time() + 3600*($timezone+date("I"))) . $fcalcsidkey;
                             
                                                                                             $sqedl = $wpdb->insert("nrecording_staff_timesheets_records",
                                                                                             array(
                                                                                             'timesheet_id' => $timeid,
                                                                                                 'dates'     => $ecleadateonly,
                                                                                                 'clock_in_out' => $ecleavehrs,
                                                                                                 'late' => $nulls,
                                                                                                 'undertime' => $nulls,
                                                                                                 'regular' => $nulls,
                                                                                                 'overtime' => $nulls,
                                                                                                 'total' => $nulls,
                                                                                                 'ot_total_hours' => $nulls,
                                                                                                 'total_hours' => $nulls,
                                                                                                 'status' => $nulls,
                                                                                                 'staff_id' => $encodeuid,
                                                                                                 'daybreak' => $wholedcheckr
                                                                                             ));
                             
                                                                             }//CLOSING TAG IF NO DATA DUPLICATE OR EXIT INSERT NEW RECORDS TO NCRECORDS                                        
                                                                         }//CLOSING FOR LISTING AND CHECKING IF CLOCK IN OUT EXIST OR NOT
 




                            
                                                                    
                        
                        
                                                                     }elseif($requestypes == 'Half Day'){
                        
                        
                                                                    /**
                                                                     * DO CHECKING IF THIS DATE ALREADY 
                                                                     * EXIST TO NCRECORDS THE TEMP TBL 
                                                                     * FOR ALL THE STAFF ONLINE TAP OR 
                                                                     * QRCODE TAP
                                                                     */
                        
                                                                     /**
                                                                      * DO ENCODING FIRST THEN CHECK THE DATES
                                                                      */
                        
                                                                    $encodeuid = str_rot13($staff_id);
                        
                                                               

                                                                    $cleaves = date_create($start_date);
                                                                    $cleavehrs = date_format($cleaves,"m/d/Y H:i");
                                                                    $cleadateonly = date_format($cleaves,"m/d/Y");


                                                                    
                                                                    $cend_date = date_create($end_date);
                                                                    $ecleavehrs = date_format($cend_date,"m/d/Y H:i");
                                                                    $ecleadateonly = date_format($cleaves,"m/d/Y");





                                                                    $ifamorpm = $gdatesfiledstart;
                                                                    $ifampmtime = date_create($cleavehrs);
                                                                    $ifamorpmtimes = date_format($ifampmtime, 'a');

                                                                    if($ifamorpmtimes == 'AM'){

                                                                    /**
                                                                     * CREATE DATE FOR INSERTING NEW
                                                                     * RECORDS TBL COLUMN NEED
                                                                     */
                        
                                                                     $cleaves = date_create($start_date);
                                                                     $cleavehrs = date_format($cleaves,"m/d/Y H:i");
                                                                     $cleadateonly = date_format($cleaves,"m/d/Y");
                        
                                                                    $glistcheck = $wpdb->get_results("SELECT COUNT(dates) AS aexistdtx FROM `nrecording_staff_timesheets_records` WHERE staff_id ='$encodeuid' AND  clock_in_out='$cleavehrs' ");
                                                                    foreach ($glistcheck as $valuxe) {
                        
                                                                        if($valuxe->aexistdtx > 0){
                                                                        
                                                                        }else{
                        
                                                                                    /**
                                                                                     ** INSERT  SPECIFIC DATE
                                                                                    **/
                        
                                                                                    $nulls = NULL;
                                                                                    $wholedcheckr = "LEAVE_HALFDAY_AM_APPROVED";
                                                                                    $gonlyhours = NULL;
                                                                                    $fcalcsidkey = $calcsidkey * 2;
                        
                                                                                    $timeid="TSH". gmdate("h", time() + 3600*($timezone+date("I"))) . $fcalcsidkey;
                        
                                                                                        $sqedl = $wpdb->insert("nrecording_staff_timesheets_records",
                                                                                        array(
                                                                                           'timesheet_id' => $timeid,
                                                                                             'dates'     => $cleadateonly,
                                                                                             'clock_in_out' => $cleavehrs,
                                                                                             'late' => $nulls,
                                                                                             'undertime' => $nulls,
                                                                                             'regular' => $nulls,
                                                                                             'overtime' => $nulls,
                                                                                             'total' => $nulls,
                                                                                             'ot_total_hours' => $nulls,
                                                                                             'total_hours' => $nulls,
                                                                                             'status' => $nulls,
                                                                                             'staff_id' => $encodeuid,
                                                                                             'daybreak' => $wholedcheckr
                                                                                        ));
                        
                                                                            }//CLOSING TAG IF NO DATA DUPLICATE OR EXIT INSERT NEW RECORDS TO NCRECORDS                                        
                                                                        }//CLOSING FOR LISTING AND CHECKING IF CLOCK IN OUT EXIST OR NOT
                        
                        



                                                                    }elseif($ifamorpmtimes == 'PM'){

                                                                        
                                                                                /**
                                                                                 * CREATE DATE FOR INSERTING NEW
                                                                                 * RECORDS TBL COLUMN NEED
                                                                                 */
                                    
                                                                               
                                                                                $cend_date = date_create($end_date);
                                                                                $ecleavehrs = date_format($cend_date,"m/d/Y H:i");
                                                                                $ecleadateonly = date_format($cleaves,"m/d/Y");

                                    
                                                                                $glistcheck = $wpdb->get_results("SELECT COUNT(dates) AS aexistdtx FROM `nrecording_staff_timesheets_records` WHERE staff_id ='$encodeuid' AND  clock_in_out='$ecleavehrs' ");
                                                                                foreach ($glistcheck as $valuxe) {
                                    
                                                                                    if($valuxe->aexistdtx > 0){
                                                                                    
                                                                                    }else{
                                    
                                                                                                /**
                                                                                                 ** INSERT  SPECIFIC DATE
                                                                                                **/
                                    
                                                                                                $nulls = NULL;
                                                                                                $wholedcheckr = "LEAVE_HALFDAY_PM_APPROVED";
                                                                                                $gonlyhours = NULL;
                                                                                                $fcalcsidkey = $calcsidkey * 2;
                                    
                                                                                                $timeid="TSH". gmdate("h", time() + 3600*($timezone+date("I"))) . $fcalcsidkey;
                                    
                                                                                                    $sqedl = $wpdb->insert("nrecording_staff_timesheets_records",
                                                                                                    array(
                                                                                                    'timesheet_id' => $timeid,
                                                                                                        'dates'     => $ecleadateonly,
                                                                                                        'clock_in_out' => $ecleavehrs,
                                                                                                        'late' => $nulls,
                                                                                                        'undertime' => $nulls,
                                                                                                        'regular' => $nulls,
                                                                                                        'overtime' => $nulls,
                                                                                                        'total' => $nulls,
                                                                                                        'ot_total_hours' => $nulls,
                                                                                                        'total_hours' => $nulls,
                                                                                                        'status' => $nulls,
                                                                                                        'staff_id' => $encodeuid,
                                                                                                        'daybreak' => $wholedcheckr
                                                                                                    ));
                                    
                                                                                        }//CLOSING TAG IF NO DATA DUPLICATE OR EXIT INSERT NEW RECORDS TO NCRECORDS                                        
                                                                                    }//CLOSING FOR LISTING AND CHECKING IF CLOCK IN OUT EXIST OR NOT
                                    
                                    

                                                                        }//CLOSING TAG IF AM OR PM THE LEAVE REQUEST FOR HALF DAY ONLY
                                                                     }//CLOSING TAG FOR CHECKING IF EMPTY OR NOT THE DTR IN OR OUT
                                                                 }//CLOSING FOR STAFF DTR TBL LIST
                                                              }//CLOSING TAG FOR GETTING ALL THE STAFF WHO ARE LISTED UNDER THE SUPERVISOR
                        
                                                                               
                        
                                                                             
                        
                        
                        



                                }//CLOSING TAG FOR ELSE IF NOT UNLIMITED POINTS / WITHOUT PAYS
                            }// CLOSING TAG ALL APPROVED ONLY  BETWEEN CUT OFF PERIOD

                  ?>

                </tbody>
              </table>






           </div>
         </div>
         <!-- End Col -->















               <!-- End Col -->
             </div>
             <!-- End Row -->






             <!-- OVERTIME ROW START -->
             <br>

             <div class="row">
               <div class="col-lg-12">
                 <div class="card-style mb-30">
                   <div
                     class="
                       title
                       d-flex
                       flex-wrap
                       align-items-center
                       justify-content-between
                     "
                   >
                   <div class="left">
                     <h4 class="text-medium mb-2">Overtime List</h4>
                   </div>
                   <div class="left">

                   </div>

                     <div class="right">
                       <div class="select-style-1 mb-2">

                       </div>
                       <!-- end select -->
                     </div>
                   </div>
                   <!-- End Title -->


                   <table id="overtimfiles" style="width: 100%" class="">
                     <thead>
                       <tr>
                         <th>Date Filed</th>
                         <th>Staff ID</th>
                         <th>Timesheet</th>
                         <th>Overtime Start</th>
                         <th>Overtime End</th>
                         <th>Total Overtime</th>
                         <th>Reasons</th>
                         <th>Status</th>
                         <th>Actions</th>
                       </tr>





                     </thead>
                     <tbody >


                       <?php


                         /**
                         ** GET DTR LIST VIA SUPERVISOR
                         **/

                         $currensupvs = $current_user->user_login;

                         $gcurrentslits = $wpdb->get_results("SELECT userid, Name FROM `staff_almost_fullrecords` WHERE supervisors ='$currensupvs' AND ( inactive ='No' OR supervisors='$currensupvs') ");
                         foreach ($gcurrentslits as $key => $sffvalue) {

                             $supstaflist = $sffvalue->userid;

                             /**
                               ** GET THE CURENT YEAR, MONTH AND DAY FOR DISPLAYING THE SPECIFIC
                               ** LIST OF REQUESTS OF THE STAFF VIA SUPERVISOR SELECT
                               **/

                               /**
                               ** PH TIMEZONES AND GET ONLY YEAR
                               **/

                               $timezone  = + 8; //(GMT +8:00) Philippines
                               $mdydatesonly = gmdate("m/d/Y", time() + 3600*($timezone+date("I")));


                        $gallsupstafli = $wpdb->get_results("SELECT * FROM `staff_overtime_request_tabs`  WHERE staff_id = '$supstaflist' AND timesheets BETWEEN '$startdates' AND '$endsts'  AND YEAR(STR_TO_DATE(timesheets, '%m/%d/%Y')) = '$gyearselect'");
                        foreach ($gallsupstafli as $key => $overtimelist) {

                          $ovstaffid = $overtimelist->staff_id;
                          $overtime_timeout = $overtimelist->overtime_timeout;
                          $overtime_timein = $overtimelist->overtime_timein;
                          $timesheets = $overtimelist->timesheets;
                          $totalovertime = $overtimelist->totalovertime;
                          $reasons = $overtimelist->reasons;
                          $approval = $overtimelist->approval;
                          $datefiled = $overtimelist->datefiled;
                            $idkey = $overtimelist->idkey;





                       ?>
                       <tr>
                               <td><?= ++$countss; ?></td>
                               <td style="text-align: left">


                               <?php

                                   echo $sffvalue->Name;

                               ?>


                               </td>
                               <td><?= $timesheets; ?></td>
                               <td><?= $overtime_timein; ?></td>
                               <td><?= $overtime_timeout; ?></td>
                               <td><?= $totalovertime; ?></td>
                               <td><?= $reasons; ?></td>
                               <td><?= $approval; ?></td>
                               <td>




                           <form method="post">

                                 <input <?= $checbtns ?> type="hidden" name="overidlist[]" value="<?= $ovstaffid ?>">
                                 <input type="hidden" name="getditfiled[]" value="<?= $idkey ?>">
                                 <input name="form_nonce" type="hidden" value="<?=wp_create_nonce('staff-nonce')?>" />

                                 <?php

                                     if($approval == 'APPROVED' || $approval == 'DISAPPROVED' || $approval == 'WITHDRAW' ){

                                         $btndisabled = "disabled";

                                     }else {
                                         $btndisabled = "";
                                     }

                                 ?>


                                 <button <?= $btndisabled; ?> type="submit" name="overapproved" class="btn btn-success">

                                   <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-check2" viewBox="0 0 16 16">
                                         <path d="M13.854 3.646a.5.5 0 0 1 0 .708l-7 7a.5.5 0 0 1-.708 0l-3.5-3.5a.5.5 0 1 1 .708-.708L6.5 10.293l6.646-6.647a.5.5 0 0 1 .708 0z"/>
                                       </svg>

                                     </button>
                                 <button  type="submit" name="overdisapproved" class="btn btn-danger">
                                   <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-x" viewBox="0 0 16 16">
                                   <path d="M4.646 4.646a.5.5 0 0 1 .708 0L8 7.293l2.646-2.647a.5.5 0 0 1 .708.708L8.707 8l2.647 2.646a.5.5 0 0 1-.708.708L8 8.707l-2.646 2.647a.5.5 0 0 1-.708-.708L7.293 8 4.646 5.354a.5.5 0 0 1 0-.708z"/>
                                   </svg>
                                 </button>

                           </form>




                         </td>





                       </tr>

                       <?php
                            } // END LOOP FOR THE OVERTIME REQUEST LIST
                          } //END LOOP FOR THE SUPERVISOR STAFF LIST'





                            /**
                            ** GET TIMESHEETS DATES VIA APPROVED BY SUPERVISOR
                            **/

                            $gtimesheetdates = $wpdb->get_results("SELECT * FROM `staff_overtime_request_tabs`  WHERE supervisors = '$currensupvs' AND approval = 'APPROVED' ");
                            foreach ($gtimesheetdates as $key => $thvalue) {

                                $timehdate = $thvalue->timesheets;
                                $totalovertime = $thvalue->totalovertime;
                                $staff_idsf = $thvalue->staff_id;


                                /**
                                ** GET STAFF SPECIFIC TIMESHEET RECORDS
                                **/

                                $gstafftimes = $wpdb->get_results("SELECT * FROM `staff_timesheets_records`  WHERE dates = '$timehdate' AND staff_id ='$staff_idsf' LIMIT 1");
                                foreach ($gstafftimes as $key => $gsprecs) {

                                    $thsheetidates =  $gsprecs->dates;
                                    $idkeys = $gsprecs->idkeys;

                                }

                                $upovertimerec = $wpdb->query($wpdb->prepare("UPDATE staff_timesheets_records SET overtime ='$totalovertime' WHERE dates ='$thsheetidates' AND staff_id = '$staff_idsf' AND idkeys='$idkeys' "));


                            }




                       ?>


                      </tbody>
                    </table>






                 </div>
               </div>
               <!-- End Col -->















               <!-- End Col -->
             </div>
             <!-- OVERTIME END ROW  -->








             <!-- STAFF ROW LIST -->
             <br>

             <div class="row">
               <div class="col-lg-12">
                 <div class="card-style mb-30">
                   <div
                     class="
                       title
                       d-flex
                       flex-wrap
                       align-items-center
                       justify-content-between
                     "
                   >
                   <div class="left">
                     <h4 class="text-medium mb-2">Staff List</h4>
                   </div>
                   <div class="left">

                   </div>

                     <div class="right">
                       <div class="select-style-1 mb-2">

                       </div>
                       <!-- end select -->
                     </div>
                   </div>
                   <!-- End Title -->

                   <form  method="post">

                   <table  id="stafftsheet" style="width: 100%"  class="">
                     <thead>

                       <tr>
                         <th>IDK</th>
                         <th>Staff Name</th>
                         <th>Late</th>
                         <th>Undertime</th>
                         <th>Overtime</th>
                         <th>Total Hours</th>
                         <th>Status</th>
                         <th>VIEW | APPROVED</th>
                       </tr>


                     </thead>
                     <tbody >

                       <?php


                         /**
                         ** GET DTR LIST VIA SUPERVISOR
                         **/

                         $currensupvs = $current_user->user_login;


                         $ttalhours = 0;
                         $totallates = 0;
                         $totallatesunder =0;
                         $totalovtime = 0;



                         $gcurrentslits = $wpdb->get_results("SELECT userid, Name FROM `staff_almost_fullrecords` WHERE supervisors ='$currensupvs' AND ( inactive ='No' OR supervisors='$currensupvs') ");
                         foreach ($gcurrentslits as $key => $sffvalue) {

                             $supstaflist = $sffvalue->userid;



                        $stgallsupstafli = $wpdb->get_results("SELECT SUM(late) AS flate, SUM(undertime) AS funder, SUM(total_hours) AS fthrous, staff_id, SUM(overtime) AS fovetim, status FROM `staff_timesheets_records`  WHERE staff_id = '$supstaflist' AND dates BETWEEN '$startdates' AND '$endsts' GROUP BY staff_id, status ");

                     

                        foreach ($stgallsupstafli as $key => $staftsheet) {

                          $staffid = $staftsheet->staff_id;
                          $late = $staftsheet->late;
                          $undertime = $staftsheet->undertime;
                       
                          $overtime = $staftsheet->overtime;
                          $total_hours = $staftsheet->total_hours;
                         

                          $totallates = $totallates + $late;
                          $totallatesunder = $totallatesunder + $undertime;
                         
                          $totalovtime = $totalovtime + $overtime;

                          $status = $staftsheet->status;




                          /**
                           * IF GREATER THAN 8 HRS IT MUST BE OVERTIME
                           * AND MUST BE FILED VIA OVERTIME PAGE
                          */




                            if($total_hours > 8){

                                $ttalhours = $ttalhours + 8;
                            }else{

                                $ttalhours = $ttalhours + $total_hours;
                            }


                           

                        




                      
                        } // END LOOP FOR THE STAFF TIMESHEETS LIST



                         

                            /**
                             * STATUS TAG NAMING
                             * IF NULL = PENDING
                             * IF SUBMITTED = STAFF ALREADY SUBMITTED THE TIMESHEET
                             * IF APPOVED = SUPERVISOR ALREADY APPROVED THE TIMESHEET RECORDS
                             */


                            
                             if (is_null($status)) {

                                $dpstatus = "PENDING";
                                
                              } elseif (empty($status)) {


                                $dpstatus = "PENDING";

                             }elseif($status == 'SUBMITTED'){

                                $dpstatus = "SUBMITTED";

                             }elseif($status == "APPROVED"){

                                $dpstatus = "APPROVED";

                             }





                       

                       ?>
                       <tr>
                         <td><?= ++$counts; ?></td>
                         <td style="text-align: left">


                         <?php

                             echo $sffvalue->Name;

                         ?>


                         </td>
                         <td><?= $staftsheet->flate; ?></td>
                         <td><?= $staftsheet->funder; ?></td>
                         <td>
                           <?php


                             
                                       echo  $staftsheet->fovetim;
                              






                           ?>




                         </td>
                         <td><?= number_format($staftsheet->fthrous,2); ?></td>
                         <td><?= $dpstatus; ?></td>
                         <td>


                             

                             <button onclick="getStafTshee('<?php echo $supstaflist; ?>')" class="btn btn-success" type="button" name="button"  data-bs-toggle="modal" data-bs-target="#staticBackdrop">
                               <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-eye" viewBox="0 0 16 16">
                              <path d="M16 8s-3-5.5-8-5.5S0 8 0 8s3 5.5 8 5.5S16 8 16 8zM1.173 8a13.133 13.133 0 0 1 1.66-2.043C4.12 4.668 5.88 3.5 8 3.5c2.12 0 3.879 1.168 5.168 2.457A13.133 13.133 0 0 1 14.828 8c-.058.087-.122.183-.195.288-.335.48-.83 1.12-1.465 1.755C11.879 11.332 10.119 12.5 8 12.5c-2.12 0-3.879-1.168-5.168-2.457A13.134 13.134 0 0 1 1.172 8z"/>
                              <path d="M8 5.5a2.5 2.5 0 1 0 0 5 2.5 2.5 0 0 0 0-5zM4.5 8a3.5 3.5 0 1 1 7 0 3.5 3.5 0 0 1-7 0z"/>
                            </svg>
                             </button>
                             &nbsp;
                             <input <?= $checkbx ?> type="checkbox" name="gstaffidlist[]" value="<?= $supstaflist ?>">


                         </td>


                       </tr>


                       <?php

                       
                          } //END LOOP FOR THE SUPERVISOR STAFF LIST

                       ?>





                     </tbody>
                     <tbody>

                           <tr>

                             <td colspan="8">
                               <div style="float: right">
                                 <input name="form_nonce" type="hidden" value="<?=wp_create_nonce('staff-nonce')?>" />
                                 <input type="hidden" name="gmonth" value="<?= $gmonth ?> ">
                                 <input type="hidden" name="gcutoff" value="<?= $gcutoff ?> ">


                                  <button id="appsubms" class="btn btn-primary" type="Submit" name="approvedstaffsh">
                                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-check2" viewBox="0 0 16 16">
                                      <path d="M13.854 3.646a.5.5 0 0 1 0 .708l-7 7a.5.5 0 0 1-.708 0l-3.5-3.5a.5.5 0 1 1 .708-.708L6.5 10.293l6.646-6.647a.5.5 0 0 1 .708 0z"/>
                                      </svg>

                                      Submit

                                   </button>
                               </div>

                             </td>

                           </tr>

                     </tbody>
                   </table>



                   </form>



                 </div>
               </div>
               <!-- End Col -->














               <!-- End Col -->
             </div>
             <!-- STAFF END ROW -->


              <br>

              <!-- OBT LIST  -->

              <div class="row">
                <div class="col-lg-12">
                  <div class="card-style mb-30">
                    <div
                      class="
                        title
                        d-flex
                        flex-wrap
                        align-items-center
                        justify-content-between
                      "
                    >
                        <div class="left">
                          <h4 class="text-medium mb-2">OBT List</h4>
                        </div>
                        <div class="left">

                        </div>

                          <div class="right">
                            <div class="select-style-1 mb-2">

                            </div>

                          </div>
                    </div>



                    <table  id="obtsheets" style="width: 100%"  class="gobtsheets">
                      <thead>
                        <tr>
                          <th>Date</th>
                          <th>Staff ID</th>
                          <th>Request Type</th>
                          <th>OBT Start</th>
                          <th>OBT End</th>
                          <th>Reasons</th>
                          <th>Status</th>
                          <th>Actions</th>

                        </tr>

                      </thead>
                      <tbody >

                        <?php


                          /**
                          ** GET DTR LIST VIA SUPERVISOR
                          **/

                          $currensupvs = $current_user->user_login;

                          $gcurrentslits = $wpdb->get_results("SELECT userid, Name FROM `staff_almost_fullrecords` WHERE supervisors ='$currensupvs' AND ( inactive ='No' OR supervisors='$currensupvs') ");
                          foreach ($gcurrentslits as $key => $sffvalue) {

                              $supstaflist = $sffvalue->userid;



                         $allobtstftabs = $wpdb->get_results("SELECT * FROM staff_obt_request_tabs  WHERE staff_id = '$supstaflist'  AND obt_start BETWEEN '$fmonthday' AND '$ldayofmst'   AND YEAR(STR_TO_DATE(datefiled, '%m/%d/%Y')) = '$gyearselect'");
                         foreach ($allobtstftabs as $key => $obsheets) {

                           $obtstaffid = $obsheets->staff_id;
                           $request_type = $obsheets->request_type;
                           $obt_start = $obsheets->obt_start;
                           $obt_end = $obsheets->obt_end;
                           $overtime = $obsheets->overtime;
                           $reasons = $obsheets->reasons;
                           $approval = $obsheets->approval;
                           $datefiled = $obsheets->datefiled;
                           $idkeys = $obsheets->idkey;








                        ?>
                        <tr>
                          <td><?= ++$counts; ?></td>
                          <td style="text-align: left">


                          <?php

                              echo $sffvalue->Name;

                          ?>


                          </td>
                          <td><?= $request_type; ?></td>
                          <td><?= $obt_start; ?></td>
                          <td><?= $obt_end; ?></td>
                          <td><?= $reasons; ?></td>
                          <td><?= $approval; ?></td>
                          <td>




                            <form method="post">

                                <input <?= $checbtns ?> type="hidden" name="obtidlist[]" value="<?= $obtstaffid ?>">
                                <input type="hidden" name="getditfiled[]" value="<?= $idkeys ?>">
                                  <input name="form_nonce" type="hidden" value="<?=wp_create_nonce('staff-nonce')?>" />

                                  <?php

                                      if($approval == 'APPROVED' || $approval == 'DISAPPROVED'  || $approval == 'WITHDRAW'){

                                          $btndisabled = "disabled";

                                      }else {
                                          $btndisabled = "";
                                      }

                                  ?>


                                  <button <?= $btndisabled; ?> type="submit" name="obtapproved" class="btn btn-success">

                                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-check2" viewBox="0 0 16 16">
                                          <path d="M13.854 3.646a.5.5 0 0 1 0 .708l-7 7a.5.5 0 0 1-.708 0l-3.5-3.5a.5.5 0 1 1 .708-.708L6.5 10.293l6.646-6.647a.5.5 0 0 1 .708 0z"/>
                                        </svg>

                                      </button>
                                  <button   type="submit" name="obtdisapproved" class="btn btn-danger">
                                    <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-x" viewBox="0 0 16 16">
                                    <path d="M4.646 4.646a.5.5 0 0 1 .708 0L8 7.293l2.646-2.647a.5.5 0 0 1 .708.708L8.707 8l2.647 2.646a.5.5 0 0 1-.708.708L8 8.707l-2.646 2.647a.5.5 0 0 1-.708-.708L7.293 8 4.646 5.354a.5.5 0 0 1 0-.708z"/>
                                    </svg>
                                  </button>

                            </form>




                          </td>


                        </tr>


                        <?php

                           } // END LOOP FOR THE STAFF TIMESHEETS LIST
                           } //END LOOP FOR THE SUPERVISOR STAFF LIST


                           /**
                           ** OFFICIAL BUSINESS TRAVEL ADD FILED
                           ** TO TIMESHEET RECORDS
                           **/


                           /**
                           ** GET ALL OBT REQUEST THAT ARE APPROVED
                           **/

                           $obtappved = $wpdb->get_results("SELECT * FROM staff_obt_request_tabs  WHERE staff_id = '$obtstaffid'  AND datefiled BETWEEN '$fmonthday' AND '$ldayofmst' AND approval ='APPROVED' AND YEAR(STR_TO_DATE(datefiled, '%m/%d/%Y')) = '$gyearselect'");
                           foreach ($obtappved as $key => $obtvalrec) {

                             $gobtsdate = $obtvalrec->obt_start;
                             $obtedate =  $obtvalrec->obt_end;
                             $reqtype =  $obtvalrec->request_type;

                             if($reqtype =='Whole Day'){



                                  /**
                                  ** CALCULATE THE TWO DATE DIFFERENCE
                                  **/


                                   $first_date = new DateTime($gobtsdate);
                                   $second_date = new DateTime($obtedate);
                                   $interval = date_diff($first_date, $second_date);
                                   $totaldiff =  $interval->format('%a');
                                   $addstday = $totaldiff + 1;

                                   /**
                                   ** GET ONLY MONTH / DAY / YEAR
                                   **/

                                   $gdateonly = date_create($gobtsdate);
                                   $gfdateapp = date_format($gdateonly, 'm/d/Y');


                                   $obtstaffidenc = str_rot13($obtstaffid);

                                   /**
                                   ** CHECK IF THE DATES ALREADY EXIST TO THE TIMESHEET
                                   **/


                                   $chkdates = $wpdb->get_results("SELECT COUNT(*) AS dateexist FROM `nrecording_staff_timesheets_records` WHERE  dates = '$gfdateapp' AND staff_id= '$obtstaffidenc' ");
                                   foreach ($chkdates as $key => $exvalue) {

                                         $dexistnow = $exvalue->dateexist;



                                         if($dexistnow > 0){

                                           /**
                                           ** IF THERES A RECORD IT WILL BE SKIP TO ADD OBT
                                           **/


                                         }else{

                                                /**
                                                 ** IF NOT EXIST CREATE DATES AND ADD
                                                 ** TO THE SPECIFIC TIMESHEET RECORD
                                                 **/


                                                    /**
                                                    ** CREATE
                                                    ** INCREMENTED DAYS
                                                    **/


                                                    for ($i=0; $i < $addstday ; $i++) {

                                                      $intervals = 'P'. $i. 'D';

                                                      $obtincmdate = new DateTime($gobtsdate);
                                                      $obtincmdate->add(new DateInterval($intervals)); // increment days
                                                      $incrementedys =  $obtincmdate->format('m/d/Y');






                                                        /**
                                                        ** GET STAFF START TIME AND END TIME
                                                        **/

                                                        $gsendtimeonly = $wpdb->get_results("SELECT work_starts, work_ends  FROM `staff_almost_fullrecords` WHERE userid ='$obtstaffid' AND ( inactive ='No' OR supervisors='$currensupvs')");
                                                        foreach ($gsendtimeonly as $key => $stclvalue) {

                                                          $workstart =  $stclvalue->work_starts;
                                                          $work_ends = $stclvalue->work_ends;



                                                          $nulls = "NULL";
                                                          $obtaction = "OBT";

                                                         $fcalcsidkey = $calcsidkey * 2;

                                                         $timeid="TSH". gmdate("h", time() + 3600*($timezone+date("I"))) . $fcalcsidkey;

                                                                 /**
                                                                    ** INSERT  SPECIFIC DATE
                                                                **/
                                    
                                                                $nulls = NULL;
                                                                $wholedcheckr = "OBT_WHOLEDAY_APPROVED";
                                                                $gonlyhours = NULL;
                                                                $fcalcsidkey = $calcsidkey * 2;

                                                                $combinestrd = $incrementedys ." " .$workstart;
                                                           

                                                                    $sqedl = $wpdb->insert("nrecording_staff_timesheets_records",
                                                                    array(
                                                                    'timesheet_id' => $timeid,
                                                                        'dates'     => $incrementedys,
                                                                        'clock_in_out' => $combinestrd,
                                                                        'late' => $nulls,
                                                                        'undertime' => $nulls,
                                                                        'regular' => $nulls,
                                                                        'overtime' => $nulls,
                                                                        'total' => $nulls,
                                                                        'ot_total_hours' => $nulls,
                                                                        'total_hours' => $nulls,
                                                                        'status' => $nulls,
                                                                        'staff_id' => $obtstaffidenc,
                                                                        'daybreak' => $wholedcheckr
                                                                    ));



                                                                  /**
                                                                 ** INSERT  SPECIFIC DATE
                                                                **/
                                    
                                                                $nulls = NULL;
                                                                $wholedcheckr = "OBT_WHOLEDAY_APPROVED";
                                                                $gonlyhours = NULL;
                                                                $fcalcsidkey = $calcsidkey * 2;

                                                    
                                                                $combineend = $incrementedys ." " .$work_ends;

                                                                    $sqedl = $wpdb->insert("nrecording_staff_timesheets_records",
                                                                    array(
                                                                    'timesheet_id' => $timeid,
                                                                        'dates'     => $incrementedys,
                                                                        'clock_in_out' => $combineend,
                                                                        'late' => $nulls,
                                                                        'undertime' => $nulls,
                                                                        'regular' => $nulls,
                                                                        'overtime' => $nulls,
                                                                        'total' => $nulls,
                                                                        'ot_total_hours' => $nulls,
                                                                        'total_hours' => $nulls,
                                                                        'status' => $nulls,
                                                                        'staff_id' => $obtstaffidenc,
                                                                        'daybreak' => $wholedcheckr
                                                                    ));



                                                    }// FOREACH ADDING STARTING AND ENDING STAFF END

                                                  }// FOR LOOP DATES INCREMENT


                                         }//CLOSING TAG FOR ELSE IF NO RECORD EXIST YET

                                   }//CLOSING TAG FOR CHECKING EXIST RECORD IN TIMESHEET


                             }elseif ($reqtype =='Half Day') {

                                $obtstaffidenc = str_rot13($obtstaffid);


                                   /**
                                   ** GET ONLY MONTH / DAY / YEAR
                                   **/

                                   $gdateonly = date_create($gobtsdate);
                                   $gfdateapp = date_format($gdateonly, 'm/d/Y');
                                   $gfdateappwhr = date_format($gdateonly, 'm/d/Y H:i');
                                   $forpmam = date_format($gdateonly, 'A');


                                  
                                   $gobtenddate = date_format($obtedate, 'm/d/Y H:i');




                                   if($forpmam == 'AM'){

                                    
                                        /**
                                        ** CHECK IF THE DATES ALREADY EXIST TO THE TIMESHEET
                                        **/




                                    $chkdatesh = $wpdb->get_results("SELECT COUNT(*) AS zdateexist FROM `nrecording_staff_timesheets_records` WHERE  clock_in_out = '$gobtsdate' AND staff_id= '$obtstaffidenc' ");
                                    foreach ($chkdatesh as $key => $hexvalue) {

                                            $hdexistnow = $hexvalue->zdateexist;



                                            if($hdexistnow > 0){

                                            /**
                                             ** IF THERES A RECORD IT WILL BE SKIP TO ADD OBT
                                            **/


                                            }else{

                                                    
                                                            /**
                                                            ** ADDITIONAL HALF DAY CHECK IF RECORD ALREADY EXIST
                                                            **/


                                                                    /**
                                                                    ** IF NO RECORD EXIST ADD NEW
                                                                    **/

                                                                    $nulls = "NULL";
                                                                    $obtaction = "OBT";

                                                                $fcalcsidkey = $calcsidkey * 2;

                                                                $timeid="TSH". gmdate("h", time() + 3600*($timezone+date("I"))) . $fcalcsidkey;

                                                                /**
                                                                    ** INSERT  SPECIFIC DATE
                                                                **/
                                    
                                                                $nulls = NULL;
                                                                $wholedcheckr = "OBT_HALFDAY_APPROVED";
                                                                $gonlyhours = NULL;
                                                                $fcalcsidkey = $calcsidkey * 2;

                                                                

                                                                    $sqedl = $wpdb->insert("nrecording_staff_timesheets_records",
                                                                    array(
                                                                    'timesheet_id' => $timeid,
                                                                        'dates'     => $gfdateapp,
                                                                        'clock_in_out' => $gobtsdate,
                                                                        'late' => $nulls,
                                                                        'undertime' => $nulls,
                                                                        'regular' => $nulls,
                                                                        'overtime' => $nulls,
                                                                        'total' => $nulls,
                                                                        'ot_total_hours' => $nulls,
                                                                        'total_hours' => $nulls,
                                                                        'status' => $nulls,
                                                                        'staff_id' => $obtstaffidenc,
                                                                        'daybreak' => $wholedcheckr
                                                                    ));



                                                }//CLOSING TAG FOR ELSE IF NO RECORD EXIST YET

                                        }//CLOSING TAG FOR CHECKING EXIST RECORD IN TIMESHEET

                                   }elseif($forpmam == 'PM'){

                                        /**
                                        ** CHECK IF THE DATES ALREADY EXIST TO THE TIMESHEET
                                        **/
                                        $obtedatesf = date_create($obtedate);
                                        $gobtenddateonly = date_format($obtedatesf, 'm/d/Y');

                                        $obtstaffidenc = str_rot13($obtstaffid);

                                        $chkdatesh = $wpdb->get_results("SELECT COUNT(*) AS dateexisto FROM `nrecording_staff_timesheets_records` WHERE  clock_in_out = '$gobtenddate' AND staff_id= '$obtstaffidenc' ");
                                        foreach ($chkdatesh as $key => $hexvalue) {
    
                                                $hdexistnoweob = $hexvalue->dateexisto;
    
    
    
                                                if($hdexistnoweob > 0){
    
                                                /**
                                                 ** IF THERES A RECORD IT WILL BE SKIP TO ADD OBT
                                                **/
    
    
                                                }else{
    
                                                        
                                                                /**
                                                                ** ADDITIONAL HALF DAY CHECK IF RECORD ALREADY EXIST
                                                                **/
    
    
                                                                        /**
                                                                        ** IF NO RECORD EXIST ADD NEW
                                                                        **/
    
                                                                    $nulls = "NULL";
                                                                    $obtaction = "OBT";
    
                                                                    $fcalcsidkey = $calcsidkey * 2;
    
                                                                    $timeid="TSH". gmdate("h", time() + 3600*($timezone+date("I"))) . $fcalcsidkey;
    
                                                                    /**
                                                                        ** INSERT  SPECIFIC DATE
                                                                    **/
                                        
                                                                    $nulls = NULL;
                                                                    $wholedcheckr = "OBT_HALFDAY_APPROVED";
                                                                    $gonlyhours = NULL;
                                                                    $fcalcsidkey = $calcsidkey * 2;
    
                                                                    
    
                                                                        $sqedl = $wpdb->insert("nrecording_staff_timesheets_records",
                                                                        array(
                                                                        'timesheet_id' => $timeid,
                                                                            'dates'     => $gobtenddateonly,
                                                                            'clock_in_out' => $obtedate,
                                                                            'late' => $nulls,
                                                                            'undertime' => $nulls,
                                                                            'regular' => $nulls,
                                                                            'overtime' => $nulls,
                                                                            'total' => $nulls,
                                                                            'ot_total_hours' => $nulls,
                                                                            'total_hours' => $nulls,
                                                                            'status' => $nulls,
                                                                            'staff_id' => $obtstaffidenc,
                                                                            'daybreak' => $wholedcheckr
                                                                        ));
    
    
    
                                                     }//CLOSING TAG FOR ELSE IF NO RECORD EXIST YET
                                             }//CLOSING TAG FOR CHECKING EXIST RECORD IN TIMESHEET
                                         }//CLOSING TAG FOR HALFDAY IF AM OR PM





                                         
                                  }//CLOSING TAG FOR HALF DAY
                           }//CLOSING TAG FOR OBT APPROVED LIST





                        ?>





                      </tbody>
                    </table>





                  </div>
                </div>

              </div>

              <!-- OBT END -->








            <!-- TIMESHEET MODAL -->

            <div class="modal fade" id="staticBackdrop" data-bs-backdrop="static" data-bs-keyboard="false" tabindex="-1" aria-labelledby="staticBackdropLabel" aria-hidden="true">
              <div class="modal-dialog modal-xl" data-bs-backdrop="static" data-bs-keyboard="false">
                <div class="modal-content">
                  <div class="modal-header">
                    <h1 class="modal-title fs-5" id="staticBackdropLabel">TIMESHEET</h1>
                    <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                  </div>
                  <div class="modal-body">
                    <table id="tshedataf" style="width: 100%" >
                      <thead>
                          <th>Date</th>
                          <th>Staff ID</th>
                          <th>Clock In</th>
                          <th>Clock Out</th>
                          <th>Total Hours</th>
                          <th>Late</th>
                          <th>Undertime</th>
                          <th>OT</th>

                      </thead>
                      <tbody id="tshedata">


                      </tbody>
                    </table>
                  </div>
                  <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>

                  </div>
                </div>
              </div>
            </div>


            <!-- END TIMESHEET MODAL -->








           <button
                style="z-index: 9999;"
                type="button"
                class="btn btn-primary btn-floating btn-lg"
                id="btn-back-to-top"
                >
                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor" class="bi bi-arrow-up-circle-fill" viewBox="0 0 16 16">
            <path d="M16 8A8 8 0 1 0 0 8a8 8 0 0 0 16 0zm-7.5 3.5a.5.5 0 0 1-1 0V5.707L5.354 7.854a.5.5 0 1 1-.708-.708l3-3a.5.5 0 0 1 .708 0l3 3a.5.5 0 0 1-.708.708L8.5 5.707V11.5z"/>
          </svg>
        </button>


       <!-- End lEAVE REQUEST Row -->
     </div>
     <!-- end container -->
   </section>


   <!-- ========== section end ========== -->

   <!-- ========== footer start =========== -->
   <footer class="footer">
     <div class="container-fluid">
       <div class="row">
         <div class="col-md-6 order-last order-md-first">
           <div class="copyright text-center text-md-start">

           </div>
         </div>
         <!-- end col-->
         <div class="col-md-6">
           <div
             class="
               terms
               d-flex
               justify-content-center justify-content-md-end
             "
           >
             <a href="#0" class="text-sm">Term & Conditions</a>
             <a href="#0" class="text-sm ml-15">Privacy & Policy</a>
           </div>
         </div>
       </div>
       <!-- end row -->
     </div>
     <!-- end container -->
   </footer>
   <!-- ========== footer end =========== -->
 </main>
 <!-- ======== main-wrapper end =========== -->




    <script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.29.1/moment-with-locales.min.js" integrity="sha512-LGXaggshOkD/at6PFNcp2V2unf9LzFq6LE+sChH7ceMTDP0g2kn6Vxwgg7wkPP7AAtX+lmPqPdxB47A0Nz0cMQ==" crossorigin="anonymous"></script>

    <script src="https://code.jquery.com/jquery-3.5.1.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery.form/4.3.0/jquery.form.min.js" integrity="sha384-qlmct0AOBiA2VPZkMY3+2WqkHtIQ9lSdAsAn5RUJD/3vA5MKDgSGcdmIv4ycVxyn" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/flatpickr"></script>


    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.4/jquery.min.js"></script>

    <script src="<?php echo plugin_dir_url( __FILE__ ) . 'assets/js/staff_allinone_app.js'?>" ></script>

    <script type="text/javascript">

    /***
    *** GET STAFF DETAILED TIMESHEETS
    ***/


        function getStafTshee(stafid){

          console.log(stafid)


          const tbshedataf = $('#tshedataf').DataTable();

            tbshedataf.clear().destroy();


          let thislecm =   $("#cgmonth").val();
          let thicutoffperiod =   $("#gccutoffpds").val();


          console.log(thislecm);


          $.post("https://igsl-portal.igsl.asia/timesheets-all-functions-version-2", {

            stafid:stafid,
            thislecm:thislecm,
            thicutoffperiod:thicutoffperiod


          },  function(data,status){

                  const staffidlist = JSON.parse(data);





                 $("#tshedataf").DataTable({



                       data:staffidlist,

                       "columns":[



                              { data: "dates"},
                              { data: "staff_id"},
                              { data: "clock_in" },
                               { data: "clock_out"},
                              { data: "total_hours"},
                              { data: "late"},
                              { data: "undertime"},
                              { data: "overtime"}



                       ],
                      // CREATING A BUTTON INSIDE THE TABLE
                    //    "columnDefs": [
                    //      {
                    //           targets: [2],
                    //           data:"clock_out",
                    //           "render": function ( data, type, row, meta ) {
                    //
                    //            let  clock_out = data;
                    //            let  cremovtext = clock_out.substr(11);
                    //            return '<p>'+cremovtext+'</p>';
                    //           }
                    //
                    //        },
                    //
                    //
                    //
                    //
                    // ],

                       "lengthMenu": [[-1, 700, 1500, 2000], ["ALL", 700, 1500, 2000]],
                       "processing": false,

                       // buttons: [
                       //        {
                       //            text: 'ADD',
                       //            className: "btn btn-success add glyphicon glyphicon-plus",
                       //            action: function ( e, dt, node, config ) {
                       //            window.location.replace("https://alumni.igsl.asia/add-new-alumni/");
                       //            }
                       //        },
                       //
                       //        {
                       //            text: ' SendMail',
                       //            className: "btn btn-success add glyphicon glyphicon-send",
                       //            action: function ( e, dt, node, config ) {
                       //            window.location.replace("https://alumni.igsl.asia/alumni-send-mail/");
                       //            }
                       //        }
                       //    ],
                      dom: '<dtlifBterspacer>',
                      responsive: true
                   });






               });











        }


    </script>





      <script>
      function showTime(){
          var date = new Date();
          var h = date.getHours(); // 0 - 23
          var m = date.getMinutes(); // 0 - 59
          var s = date.getSeconds(); // 0 - 59
          var session = "AM";

          if(h == 0){
              h = 12;
          }

          if(h > 12){
              h = h - 12;
              session = "PM";
          }

          h = (h < 10) ? "0" + h : h;
          m = (m < 10) ? "0" + m : m;
          s = (s < 10) ? "0" + s : s;

          var time = h + ":" + m + ":" + s + " " + session;
          document.getElementById("MyClockDisplay").innerText = time;
          document.getElementById("MyClockDisplay").textContent = time;

          setTimeout(showTime, 1000);

      }

      showTime();

      </script>



      <script src="<?php echo plugin_dir_url( __FILE__ ) . 'plain-template-main/assets/js/bootstrap.bundle.min.js'?>"></script>
      <script src="<?php echo plugin_dir_url( __FILE__ ) . 'plain-template-main/assets/js/Chart.min.js'?>"></script>
      <script src="<?php echo plugin_dir_url( __FILE__ ) . 'plain-template-main/assets/js/dynamic-pie-chart.js'?>"></script>
      <script src="<?php echo plugin_dir_url( __FILE__ ) . 'plain-template-main/assets/js/moment.min.js'?>"></script>
      <script src="<?php echo plugin_dir_url( __FILE__ ) . 'plain-template-main/assets/js/fullcalendar.js'?>"></script>
      <script src="<?php echo plugin_dir_url( __FILE__ ) . 'plain-template-main/assets/js/jvectormap.min.js'?>"></script>
      <script src="<?php echo plugin_dir_url( __FILE__ ) . 'plain-template-main/assets/js/world-merc.js'?>"></script>
      <script src="<?php echo plugin_dir_url( __FILE__ ) . 'plain-template-main/assets/js/polyfill.js'?>"></script>
      <script src="<?php echo plugin_dir_url( __FILE__ ) . 'plain-template-main/assets/js/main.js'?>"></script>


<!-- ALL SCRIPT HERE -->




  <script src="https://cdn.jsdelivr.net/npm/flatpickr"></script>
  <script type="text/javascript" charset="utf8" src="https://cdn.datatables.net/1.11.4/js/jquery.dataTables.js"></script>
  <script src="https://cdn.datatables.net/buttons/2.2.2/js/dataTables.buttons.min.js"> </script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jszip/3.1.3/jszip.min.js"> </script>
  <script src="https://cdn.datatables.net/1.11.4/js/dataTables.bootstrap.min.js"></script>
  <script src="https://cdn.datatables.net/responsive/2.2.9/js/dataTables.responsive.min.js"></script>

  
 <!-- IGSL JQUERY LIBRARY SELF HOST CDN -->

    <script src="https://cdn.igsl.asia/igsl-jquery/jquery-3.7.1.js"></script>
    <script src="https://cdn.igsl.asia/igsl-jquery/popper.2.11.6.min.js"></script>


       <!-- DATATABLES JS CDN SELF HOST -->

      <script type="text/javascript"  src="https://cdn.igsl.asia/igsl-jquery/jquery.dataTables.1.11.4.js"></script>
      <script type="text/javascript"  src="https://cdn.igsl.asia/igsl-jquery/dataTables.buttons.2.2.2.min.js"></script>

       <script type="text/javascript"  src="https://cdn.igsl.asia/igsl-jquery/jszip.min.js"></script>
       <script type="text/javascript"  src="https://cdn.igsl.asia/igsl-jquery/dataTables.bootstrap.min.js"></script>
       <script type="text/javascript"  src="https://cdn.igsl.asia/igsl-jquery/dataTables.reponsive.min.js"></script>
       <script type="text/javascript"  src="https://cdn.igsl.asia/igsl-jquery/flatpickr.4.6.13.js"></script>

      <!-- DATATABLES JS CDN SELF HOST END-->

   <!-- IGSL JQUERY LIBRARY SELF HOST CDN -->

<script>

  //Get the button
  let mybutton = document.getElementById("btn-back-to-top");

  // When the user scrolls down 20px from the top of the document, show the button
  window.onscroll = function () {
  scrollFunction();
  };

  function scrollFunction() {
  if (
    document.body.scrollTop > 20 ||
    document.documentElement.scrollTop > 20
  ) {
    mybutton.style.display = "block";
  } else {
    mybutton.style.display = "none";
  }
  }
  // When the user clicks on the button, scroll to the top of the document
  mybutton.addEventListener("click", backToTop);

  function backToTop() {
  document.body.scrollTop = 0;
  document.documentElement.scrollTop = 0;
  }
</script>

<script src="//cdn.jsdelivr.net/npm/sweetalert2@11"></script>
<script>
// calendar js here
flatpickr("input[type=date]", {
});

</script>





<script type="text/javascript">



        $('#obtsheets').DataTable( {
          responsive: true,
           order: [[0, 'desc']],
          "lengthMenu": [[20, 100, 200, -1], [20, 100, 200, "All"]],
           dom: 'Blrtip',
           responsive: true


        } );



          $('#stafftsheet').DataTable( {
            responsive: true,
             order: [[0, 'desc']],
            "lengthMenu": [[20, 100, 200, -1], [20, 100, 200, "All"]],
             dom: 'Blrtip',
             responsive: true


          } );





          $('#leavefile').DataTable( {
            responsive: true,
            "lengthMenu": [[20, 100, 200, -1], [20, 100, 200, "All"]],
             dom: 'Blrtip',
             responsive: true

          } );





          $('#overtimfiles').DataTable( {
            responsive: true,
            "lengthMenu": [[20, 100, 200, -1], [20, 100, 200, "All"]],
             dom: 'Blrtip',
             responsive: true


          } );





          $('#tbdtrrequestlist').DataTable( {
            responsive: true,
            "lengthMenu": [[20, 100, 200, -1], [20, 100, 200, "All"]],
             dom: 'Blrtip',
             responsive: true


          } );





</script>

<script>
  <?php

  /**
   *  EVERY TIME THE USER VIEW THIS PAGE
   *  THIS FUNCTION WILL AUTOMATICALLY TRIGGER
   *   WILL AUTOMATICALLY CHECKS THE RECORDS
   *   AND IF NOT YET REFLECTED TO THE STAFF SIDE
   *  IT WILL AUTOMATICALLY CREATE AND INSERT 
   *  NEW RECORDS.
   * 
   * VERSION: 2
   * PATCH NO: 072024 
   * DEV: RAPRAP
   * PHP: apir_supervisor_approvall_crud.php
   */
  
  ?>
 

  function onloadchecks(){

            //GET VALS
            let gcurruser = '<?php echo $current_user->user_login;?>';

            console.log(gcurruser);

                    
                      $.post("https://igsl-portal.igsl.asia/api-supervisor-approval-crud/", {

                        gcurruser:gcurruser,
                    


                      },  function(data,status){

                         //STATUS WHEN THE PROCESS IS NOT ERROR

                            const checkstats = JSON.parse(data);

                            console.log(checkstats.status);


                    });
                    


                    



}


onloadchecks();


</script>


  </body>
</html>



<?php


  /**
  ** THIS FUNCTION WILL UPDATE THE STAFF lEAVE REQUEST STATUS APPROVAL VIA SUPERVISOR
  **/


if(isset($_POST['levapproved'])){


  /**
  ** GET ALL THE SUBMITTED DATA THEN RECHANGE THE SELECTED
  **/

  $nonce = $_POST['form_nonce'];

  if (!wp_verify_nonce($nonce,'staff-nonce'))

  {
     wp_redirect( "https://igsl-portal.igsl.asia/",  302 );

  }else

  {

    /**
    ** GET STAFF LIST SUBMITTED
    **/
    $staffileav = $_POST['leavefist'];
    $lgetditfiled = $_POST['getditfiled'];

    /**
    ** GET CURRENT SUPERVISOR
    **/

    $curresupvs = $current_user->user_login;


    /**
    ** UPDATE OBT STATUS
    **/




   foreach($lgetditfiled as $staflevls)
         {


           foreach($staffileav as $staflevs)
                 {

            $suplevapp = $wpdb->query($wpdb->prepare("UPDATE staff_leave_request_tbl SET admin_status ='APPROVED' WHERE staff_id='$staflevs' AND datefiled= '$staflevls'  "));


                }


         }





      if($suplevapp){
        $location = "https://igsl-portal.igsl.asia/admin-supervisor-approval-page/";
        echo wp_redirect(   $location , 302 );

      }





  }




  }






    /**
    ** THIS FUNCTION WILL UPDATE THE OBT STATUS APPROVAL VIA SUPERVISOR
    **/


if(isset($_POST['levdisapproved'])){


    /**
    ** GET ALL THE SUBMITTED DATA THEN RECHANGE THE SELECTED
    **/

    $nonce = $_POST['form_nonce'];

    if (!wp_verify_nonce($nonce,'staff-nonce'))

    {
       wp_redirect( "https://igsl-portal.igsl.asia/",  302 );

    }else

    {

      /**
      ** GET STAFF LIST SUBMITTED
      **/
      $staffileav = $_POST['leavefist'];
      $getditfiled = $_POST['getditfiled'];

      /**
      ** GET CURRENT SUPERVISOR
      **/

      $curresupv = $current_user->user_login;


      /**
      ** UPDATE STAFF LEAVES STATUS
      **/




     foreach($getditfiled as $staflevls)
           {

             $staffid="";
             foreach($staffileav as $staflevs)

                   {

                    /**
                    ** GET RECORDED LEAVES POINTS AND ADD TO THE TOTAL REMAINING BALANCES
                    ** THE CONDITION WILL DEFEND ON WHAT LEAVE REQUEST TYPE AND
                    ** THE CHECKING WILL BE DEFENDS VIA WHOSE STAFF REQUESTED
                    **/

                    $gstafflevreq = $wpdb->get_results("SELECT * FROM `staff_leave_request_tbl` WHERE staff_id='$staflevs' AND datefiled = '$staflevls'  ");
                    foreach ($gstafflevreq as $key => $lvvalue) {

                      $leave_request_type = $lvvalue->leave_request_type;
                      $leaves_points = $lvvalue->leaves_points;

                      if($leaves_points == 0.50){

                        $flpoints = $leaves_points;

                        /**
                        ** ADD THE LEAVE POINTS TO THE SPECIFIC LEAVE NAME
                        ** AND REMOVED RECORDED LEAVES COUNTS PER RECORD
                        **/


                        $gstfybalnces = $wpdb->get_results("SELECT * FROM `staff_yearleave_balances` WHERE staff_userid='$staflevs' AND leaves_names LIKE '%$leave_request_type' ");
                        foreach ($gstfybalnces as $key => $upvvalue) {

                            $gleavenames = $upvvalue->leaves_names;
                            $gleavrembals = $upvvalue->Remaining_Balances;

                            /**
                            ** CALCULATE THE REMAINING BALANCE AND THE REJECTED BALANCE
                            **/


                            $totalrembals = $gleavrembals + $flpoints;


                          /**
                          ** UPDATE THE SPECIFIC YEARLY LEAVE BALANCE
                          **/

                            $upleavesbal = $wpdb->query($wpdb->prepare("UPDATE staff_yearleave_balances SET  Remaining_Balances ='$totalrembals' WHERE staff_userid ='$staflevs' AND leaves_names LIKE '%$gleavenames'   "));

                        }


                      }elseif ($leaves_points == 0.99) {

                          $flpoints = 1;

                          /**
                          ** ADD THE LEAVE POINTS TO THE SPECIFIC LEAVE NAME
                          ** AND REMOVED RECORDED LEAVES COUNTS PER RECORD
                          **/


                          $gstfybalnces = $wpdb->get_results("SELECT * FROM `staff_yearleave_balances` WHERE staff_userid='$staflevs' AND leaves_names LIKE '%$leave_request_type' ");
                          foreach ($gstfybalnces as $key => $upvvalue) {

                              $gleavenames = $upvvalue->leaves_names;
                              $gleavrembals = $upvvalue->Remaining_Balances;

                              /**
                              ** CALCULATE THE REMAINING BALANCE AND THE REJECTED BALANCE
                              **/


                              $totalrembals = $gleavrembals + $flpoints;


                            /**
                            ** UPDATE THE SPECIFIC YEARLY LEAVE BALANCE
                            **/

                              $upleavesbal = $wpdb->query($wpdb->prepare("UPDATE staff_yearleave_balances SET  Remaining_Balances ='$totalrembals' WHERE staff_userid ='$staflevs' AND leaves_names LIKE '%$gleavenames'   "));

                          }

                      }






                    }




                    $suplevappout = $wpdb->query($wpdb->prepare("UPDATE staff_leave_request_tbl SET admin_status ='DISAPPROVED' WHERE staff_id='$staflevs'  AND datefiled ='$staflevls' "));




                  }


           }





        if($suplevappout){
          $location = "https://igsl-portal.igsl.asia/admin-supervisor-approval-page/";
          echo wp_redirect(   $location , 302 );
        }



    }



    }







?>

<?php


  /**
  ** WHEN FORM SUBMIT RECORD THE SELECTED MONTH AND CUTOFFPERIOD
  **/


if(isset($_POST['yearmonth'])){


  /**
  ** GET ALL THE SUBMITTED DATA THEN RECHANGE THE SELECTED
  **/

  $nonce = $_POST['form_nonce'];

  if (!wp_verify_nonce($nonce,'staff-nonce'))

  {
     wp_redirect( "https://igsl-portal.igsl.asia/",  302 );

  }else

  {

    $gggmonth = $_POST['yearmonth'];
    $gcutoffper = $_POST['cufoffperd'];
    $supervisor = $_POST['gcurresupv'];
    $YearOnly = $_POST['gyearview'];


    /**
    ** DELETE SUPERVISOR RECORD FIRST THEN ADD NEW
    **/


    $supvaddn = $wpdb->query($wpdb->prepare("DELETE FROM supervisor_timesheet_view WHERE Supervisors = '$supervisor' "));

    /**
    ** INSER NEW RECORD
    **/

    $insrects = $wpdb->insert("supervisor_timesheet_view",
    array(
    'Month' => $gggmonth,
    'CutoffPeriod' => $gcutoffper,
    'Supervisors' => $supervisor,
    'YearOnly' =>$YearOnly ));



      if($insrects){
        $location = "https://igsl-portal.igsl.asia/admin-supervisor-approval-page/";
        echo wp_redirect(   $location , 302 );
      }



  }




  }





?>


<?php


  /**
  ** THIS FUNCTION WILL UPDATE THE OBT STATUS APPROVAL VIA SUPERVISOR
  **/


if(isset($_POST['obtapproved'])){


  /**
  ** GET ALL THE SUBMITTED DATA THEN RECHANGE THE SELECTED
  **/

  $nonce = $_POST['form_nonce'];

  if (!wp_verify_nonce($nonce,'staff-nonce'))

  {
     wp_redirect( "https://igsl-portal.igsl.asia/",  302 );

  }else

  {

    /**
    ** GET STAFF LIST SUBMITTED
    **/
    $staffidobt = $_POST['obtidlist'];
    $getditfiled = $_POST['getditfiled'];

    /**
    ** GET CURRENT SUPERVISOR
    **/

    $curresupv = $current_user->user_login;


    /**
    ** UPDATE OBT STATUS
    **/




   foreach($getditfiled as $dfiledsobt)
         {

           $staffid="";
           foreach($staffidobt as $staffidobtid)
                 {

            $supvaddnobt = $wpdb->query($wpdb->prepare("UPDATE staff_obt_request_tabs SET approval ='APPROVED' WHERE staff_id = '$staffidobtid' AND supervisor = '$curresupv' AND idkey ='$dfiledsobt' "));


                }


         }





      if($supvaddnobt){
        $location = "https://igsl-portal.igsl.asia/admin-supervisor-approval-page/";
        echo wp_redirect(   $location , 302 );
      }



  }




  }






    /**
    ** THIS FUNCTION WILL UPDATE THE OBT STATUS APPROVAL VIA SUPERVISOR
    **/


if(isset($_POST['obtdisapproved'])){


    /**
    ** GET ALL THE SUBMITTED DATA THEN RECHANGE THE SELECTED
    **/

    $nonce = $_POST['form_nonce'];

    if (!wp_verify_nonce($nonce,'staff-nonce'))

    {
       wp_redirect( "https://igsl-portal.igsl.asia/",  302 );

    }else

    {

      /**
      ** GET STAFF LIST SUBMITTED
      **/
      $staffidobt = $_POST['obtidlist'];
      $getditfiled = $_POST['getditfiled'];

      /**
      ** GET CURRENT SUPERVISOR
      **/

      $curresupv = $current_user->user_login;


      /**
      ** UPDATE OBT STATUS
      **/




     foreach($getditfiled as $dfiledsobta)
           {

             $staffid="";
             foreach($staffidobt as $staffidobtid)
                   {

              $supvaddnobt = $wpdb->query($wpdb->prepare("UPDATE staff_obt_request_tabs SET approval ='DISAPPROVED' WHERE  staff_id = '$staffidobtid' AND supervisor = '$curresupv' AND idkey ='$dfiledsobta' "));


                  }


           }





        if($supvaddnobt){
          $location = "https://igsl-portal.igsl.asia/admin-supervisor-approval-page/";
          echo wp_redirect(   $location , 302 );
        }



    }




    }







?>
<?php


  /**
  ** THIS FUNCTION WILL UPDATE THE DTR REQUEST STATUS APPROVED VIA SUPERVISOR
  **/


if(isset($_POST['dtrapproved'])){


  /**
  ** GET ALL THE SUBMITTED DATA THEN RECHANGE THE SELECTED
  **/

  $nonce = $_POST['form_nonce'];

  if (!wp_verify_nonce($nonce,'staff-nonce'))

  {
     wp_redirect( "https://igsl-portal.igsl.asia/",  302 );

  }else

  {

    /**
    ** GET STAFF LIST SUBMITTED
    **/
    $staffidtro= $_POST['dtrstflist'];
    $getditfiled = $_POST['getditfiled'];
    $requestypes = $_POST['requestyps'];
    $dtrtimein = $_POST['dtrtimein'];
    $dtrtimeout = $_POST['dtrtimeout'];


    /**
    ** GET CURRENT SUPERVISOR
    **/

    $curresupv = $current_user->user_login;


    /**
    ** UPDATE OBT STATUS
    **/



   /**
   ** DTR FILED DATE LIST
   **/

   foreach($getditfiled as $dtrfiled)
         {



          /**
          ** DTR STAFF ID LIST
          **/

           foreach($staffidtro as $staffidobt)

                 {

                   /**
                   ** GET THE APPROVED DTR STAFF AND UPDATE THE SPECIFIC RECORD
                   **/





            $supdtrreq = $wpdb->query($wpdb->prepare("UPDATE staff_dtr_request_tabs SET approval ='APPROVED' WHERE idkey ='$dtrfiled' "));




                }


         }





      if($supdtrreq){




        $location = "https://igsl-portal.igsl.asia/admin-supervisor-approval-page/";
        echo wp_redirect(   $location , 302 );
      }



  }




  }






    /**
    ** THIS FUNCTION WILL UPDATE THE OBT STATUS APPROVAL VIA SUPERVISOR
    **/


if(isset($_POST['dtrdisapproved'])){


    /**
    ** GET ALL THE SUBMITTED DATA THEN RECHANGE THE SELECTED
    **/

    $nonce = $_POST['form_nonce'];

    if (!wp_verify_nonce($nonce,'staff-nonce'))

    {
       wp_redirect( "https://igsl-portal.igsl.asia/",  302 );

    }else

    {

      /**
      ** GET STAFF LIST SUBMITTED
      **/
      $staffidtrout = $_POST['dtrstflist'];
      $getditfiled = $_POST['getditfiled'];

      /**
      ** GET CURRENT SUPERVISOR
      **/

      $curresupv = $current_user->user_login;


      /**
      ** UPDATE OBT STATUS
      **/




         foreach($getditfiled as $dtrfiled)
               {

                 $staffid="";
                 foreach($staffidtrout as $staffiddtors)
                       {

                  $supdtrreqdis = $wpdb->query($wpdb->prepare("UPDATE staff_dtr_request_tabs SET approval ='DISAPPROVED' WHERE  idkey ='$dtrfiled' "));


                      }


               }



        if($supdtrreqdis){
          $location = "https://igsl-portal.igsl.asia/admin-supervisor-approval-page/";
        //  echo wp_redirect(   $location , 302 );
        }



    }




    }







?>

<?php


  /**
  ** THIS FUNCTION WILL UPDATE THE OBT STATUS APPROVAL VIA SUPERVISOR
  **/


if(isset($_POST['overapproved'])){


  /**
  ** GET ALL THE SUBMITTED DATA THEN RECHANGE THE SELECTED
  **/

  $nonce = $_POST['form_nonce'];

  if (!wp_verify_nonce($nonce,'staff-nonce'))

  {
     wp_redirect( "https://igsl-portal.igsl.asia/",  302 );

  }else

  {

    /**
    ** GET STAFF LIST SUBMITTED
    **/
    $staffidover = $_POST['overidlist'];
    $getditfiled = $_POST['getditfiled'];

    //
    // /**
    // ** GET ONLY DATE
    // **/
    //
    // $ovrfulldates =  date_create($getditfiled);
    // $getditfiled = date_format($ovrfulldates, "m/d/Y");




    /**
    ** GET CURRENT SUPERVISOR
    **/

    $curresupv = $current_user->user_login;


    /**
    ** UPDATE OBT STATUS
    **/




   foreach($getditfiled as $overdfiled)
         {



           foreach($staffidover as $staffovr)
                 {

            $supviover = $wpdb->query($wpdb->prepare("UPDATE staff_overtime_request_tabs SET approval ='APPROVED' WHERE staff_id='$staffovr' AND idkey ='$overdfiled' "));


                }


         }





      if($supviover){
        $location = "https://igsl-portal.igsl.asia/admin-supervisor-approval-page/";
        echo wp_redirect(   $location , 302 );
      }



  }




  }






    /**
    ** THIS FUNCTION WILL UPDATE THE OBT STATUS APPROVAL VIA SUPERVISOR
    **/


if(isset($_POST['overdisapproved'])){


    /**
    ** GET ALL THE SUBMITTED DATA THEN RECHANGE THE SELECTED
    **/

    $nonce = $_POST['form_nonce'];

    if (!wp_verify_nonce($nonce,'staff-nonce'))

    {
       wp_redirect( "https://igsl-portal.igsl.asia/",  302 );

    }else

    {
        /**
        ** GET STAFF LIST SUBMITTED
        **/
        $staffidover = $_POST['overidlist'];
        $getditfiled = $_POST['getditfiled'];

        /**
        ** GET CURRENT SUPERVISOR
        **/

        $curresupv = $current_user->user_login;


        /**
        ** UPDATE OBT STATUS
        **/




       foreach($getditfiled as $overdfiled)
             {



               foreach($staffidover as $staffovr)
                     {

                $supviover = $wpdb->query($wpdb->prepare("UPDATE staff_overtime_request_tabs SET approval ='DISAPPROVED' WHERE staff_id='$staffovr' AND datefiled ='$overdfiled' "));


                    }


             }





          if($supviover){
            $location = "https://igsl-portal.igsl.asia/admin-supervisor-approval-page/";
            echo wp_redirect(   $location , 302 );
          }



      }



    }







?>






<?php


if(isset($_POST['approvedstaffsh'])){



      /**
      ** GET ALL THE SUBMITTED DATA THEN RECHANGE THE SELECTED
      **/

      $nonce = $_POST['form_nonce'];

      if (!wp_verify_nonce($nonce,'staff-nonce'))

      {
         wp_redirect( "https://igsl-portal.igsl.asia/",  302 );

      }else

      {

            $gmonth = $_POST['gmonth'];
            $gcutoff = $_POST['gcutoff'];
            $staffidlist = $_POST['gstaffidlist'];



            $curresupv = $current_user->user_login;

                                /**
                                ** APPROVED SPECIFIC STAFF ID
                                **/

                                /**
                                ** GET THE CURENT YEAR, MONTH AND DAY FOR DISPLAYING THE SPECIFIC
                                ** LIST OF REQUESTS OF THE STAFF VIA SUPERVISOR SELECT
                                **/

                                /**
                                ** PH TIMEZONES AND GET ONLY YEAR
                                **/

                                $timezone  = + 8; //(GMT +8:00) Philippines
                                $ydatesonly = gmdate("Y", time() + 3600*($timezone+date("I")));



                                $gmonth = $timesheetsmonth;
                                $gcutoff = $timesheetscufof;



                                  if($gmonth == "January"){




                                        if($gcutoff == 'firstCutoff'){


                                            $fmonthday = "01/01/" . $ydatesonly;
                                            $ldayofmst = "01/15/".$ydatesonly;



                                         }elseif ($gcutoff == 'seCondCutoff') {



                                                  $fmonthday = "01/16/" . $ydatesonly;
                                                  $ldayofmst = "01/31/".$ydatesonly;

                                             }



                                    }elseif ($gmonth == "February") {



                                            //GET WHAT CUTOFF FIRST OR SECOND CUT OFF AFTER GETTING THE MONTH


                                              if($gcutoff == 'firstCutoff'){

                                                  $fmonthday = "02/01/" . $ydatesonly;

                                                   $ldayofmst = "02/15/".$ydatesonly;


                                              }elseif ($gcutoff == 'seCondCutoff') {




                                                $fmonthday = "02/16/" . $ydatesonly;

                                                   $ldayofmst = "02/31/".$ydatesonly;

                                              }



                                        }elseif ($gmonth == "March") {



                                                   //GET WHAT CUTOFF FIRST OR SECOND CUT OFF AFTER GETTING THE MONTH


                                                   if($gcutoff == 'firstCutoff'){



                                                        $fmonthday = "03/01/" . $ydatesonly;
                                                        $ldayofmst = "03/15/".$ydatesonly;


                                                    }elseif ($gcutoff == 'seCondCutoff') {




                                                        $fmonthday = "03/16/" . $ydatesonly;

                                                        $ldayofmst = "03/31/".$ydatesonly;

                                                       }


                                       }elseif ($gmonth == "April") {


                                                       //GET WHAT CUTOFF FIRST OR SECOND CUT OFF AFTER GETTING THE MONTH


                                                       if($gcutoff == 'firstCutoff'){

                                                            $fmonthday = "04/01/" . $ydatesonly;
                                                            $ldayofmst = "04/15/".$ydatesonly;


                                                       }elseif ($gcutoff == 'seCondCutoff') {

                                                            $fmonthday = "04/16/" . $ydatesonly;
                                                            $ldayofmst = "04/31/".$ydatesonly;

                                                       }




                                         }elseif ($gmonth == "May") {




                                               //GET WHAT CUTOFF FIRST OR SECOND CUT OFF AFTER GETTING THE MONTH


                                               if($gcutoff == 'firstCutoff'){

                                                 $fmonthday = "05/01/" . $ydatesonly;
                                                  $ldayofmst = "01/15/".$ydatesonly;


                                               }elseif ($gcutoff == 'seCondCutoff') {


                                                    $fmonthday = "04/16/" . $ydatesonly;
                                                    $ldayofmst = "04/31/".$ydatesonly;

                                               }




                                         }elseif ($gmonth == "June") {


                                              //GET WHAT CUTOFF FIRST OR SECOND CUT OFF AFTER GETTING THE MONTH


                                              if($gcutoff == 'firstCutoff'){

                                                   $fmonthday = "06/01/" . $ydatesonly;
                                                   $ldayofmst = "06/15/".$ydatesonly;


                                              }elseif ($gcutoff == 'seCondCutoff') {

                                                   $fmonthday = "06/16/" . $ydatesonly;
                                                   $ldayofmst = "06/31/".$ydatesonly;

                                              }



                                           }elseif ($gmonth == "July") {


                                                //GET WHAT CUTOFF FIRST OR SECOND CUT OFF AFTER GETTING THE MONTH


                                                if($gcutoff == 'firstCutoff'){

                                                    $fmonthday = "07/01/" . $ydatesonly;
                                                     $ldayofmst = "07/15/".$ydatesonly;


                                                }elseif ($gcutoff == 'seCondCutoff') {

                                                    $fmonthday = "07/16/" . $ydatesonly;
                                                     $ldayofmst = "07/31/".$ydatesonly;

                                                }



                                         }elseif ($gmonth == "August") {


                                              //GET WHAT CUTOFF FIRST OR SECOND CUT OFF AFTER GETTING THE MONTH


                                              if($gcutoff == 'firstCutoff'){

                                                   $fmonthday = "08/01/" . $ydatesonly;
                                                   $ldayofmst = "08/15/".$ydatesonly;


                                              }elseif ($gcutoff == 'seCondCutoff') {

                                                   $fmonthday = "08/16/" . $ydatesonly;
                                                   $ldayofmst = "08/31/".$ydatesonly;

                                              }



                                       }elseif ($gmonth == "September") {


                                            //GET WHAT CUTOFF FIRST OR SECOND CUT OFF AFTER GETTING THE MONTH


                                            if($gcutoff == 'firstCutoff'){

                                                 $fmonthday = "09/01/" . $ydatesonly;
                                                 $ldayofmst = "09/15/".$ydatesonly;


                                            }elseif ($gcutoff == 'seCondCutoff') {

                                                $fmonthday = "09/16/" . $ydatesonly;
                                                 $ldayofmst = "09/31/".$ydatesonly;

                                            }






                                         }elseif ($gmonth == "October") {


                                              //GET WHAT CUTOFF FIRST OR SECOND CUT OFF AFTER GETTING THE MONTH


                                              if($gcutoff == 'firstCutoff'){

                                                   $fmonthday = "10/01/" . $ydatesonly;
                                                   $ldayofmst = "10/15/".$ydatesonly;


                                              }elseif ($gcutoff == 'seCondCutoff') {

                                                  $fmonthday = "10/16/" . $ydatesonly;
                                                   $ldayofmst = "10/31/".$ydatesonly;

                                              }



                                         }elseif ($gmonth == "November") {


                                              //GET WHAT CUTOFF FIRST OR SECOND CUT OFF AFTER GETTING THE MONTH


                                              if($gcutoff == 'firstCutoff'){

                                                  $fmonthday = "11/01/" . $ydatesonly;
                                                   $ldayofmst = "11/15/".$ydatesonly;


                                              }elseif ($gcutoff == 'seCondCutoff') {

                                                   $fmonthday = "11/16/" . $ydatesonly;
                                                   $ldayofmst = "11/31/".$ydatesonly;

                                              }



                                           }elseif ($gmonth == "December") {



                                                        if($gcutoff == 'firstCutoff'){

                                                            $fmonthday = "12/01/" . $ydatesonly;
                                                             $ldayofmst = "12/15/".$ydatesonly;


                                                        }elseif ($gcutoff == 'seCondCutoff') {


                                                            $fmonthday = "12/16/" . $ydatesonly;
                                                             $ldayofmst = "12/31/".$ydatesonly;

                                                        }


                                           }



                                           //DELETE ALL RECS FIRST

                                           //$wpdb->query($wpdb->prepare("DELETE  FROM staff_cutoffs_records WHERE Month = '$gmonth' AND year_tshperiod ='$ydatesonly'  "));



                                           //GET ALL THE DATES TIMESHEETS ALL BETWEEN


                                           foreach($staffidlist as $staffidk)
                                                 {
                                                   /**
                                                   ** UPDATE THE STATUS OF THE APPROVED VIA SUPERVISOR
                                                   **/

                                                   $gallsheetsrecsf = $wpdb->get_results("SELECT clock_in, staff_id, clock_out, dates, late, undertime, overtime FROM `staff_timesheets_records` WHERE staff_id='$staffidk'  AND dates BETWEEN '$fmonthday' AND '$ldayofmst' GROUP by staff_id, clock_out, clock_in, late, undertime, dates");


                                                          $tlatefs = 0;
                                                          $funderthrs = 0;

                                                   foreach ($gallsheetsrecsf as $key => $ftgvalue) {



                                                     ////////////////////////////////
                                                     //GET HOURS CLOCK IN
                                                     ////////////////////////////////

                                                     $dfcreatecin =  date_create($ftgvalue->clock_in);
                                                     $fdcinf = date_format($dfcreatecin, "H");

                                                     //GET CLOCK OUT

                                                     $edcreateout =  date_create($ftgvalue->clock_out);
                                                     $fdcoutf = date_format($edcreateout, "H");

                                                     $thousfprd = 0;
                                                     $thours = 0;

                                                     /////////////////////////////////////////////
                                                     //CALCULATE TOTAL HOURS PER MONTH PERIOD
                                                     //////////////////////////////////////////



                                                      $thousfprd = $fdcoutf - $fdcinf;

                                                      /////////////////////////////////////////////////////////////
                                                      //IF STAFF HOUR IS GREATER THAN 8 HRS must be file as Overtime
                                                      /////////////////////////////////////////////////////////////

                                                      if($thousfprd > 8){
                                                          $thousfprd = 8;
                                                          $thours = $thours + $thousfprd;
                                                      }




                                                      $tlatehrs = 0;
                                                      $combinedhrsmin = 0;
                                                      $convertedhrs = 0;



                                                      /////////////////////////////////////////////
                                                      //CALCULATE TOTAL LATE AND UNDERTIME
                                                      //LATE  HOURS
                                                      //////////////////////////////////////////

                                                      $latehrs =  date_create($ftgvalue->late);
                                                      $flatehrs = date_format($latehrs, "H");

                                                      $tlatehrs = $tlatehrs + $flatehrs;


                                                      //////////////////////////////
                                                      //CONVERT HOURS TO MINUTES
                                                      ///////////////////////////////

                                                     $convertedhrs = $tlatehrs * 60;

                                                      /////////////////
                                                      //LATE MINUTES
                                                      ///////////////


                                                      $latemn =  date_create($ftgvalue->late);
                                                      $flatemnt = date_format($latemn, "i");

                                                      $tlatefs = $tlates + $flatemnt;


                                                      ///////////////////////////////////////
                                                      //COMBINED CONVERTED HOURS AND MINUTES
                                                      ////////////////////////////////////////

                                                      $combinedhrsmin = $convertedhrs + $tlatefs;



                                                      /////////////////////////////////////////////
                                                      //CALCULATE TOTAL LATE AND UNDERTIME
                                                      //UNDERTIME  HOURS
                                                      ////////////////////////////////////////////



                                                      $tundertime = 0;


                                                      $underthrs =  date_create($ftgvalue->undertime);
                                                      $funderthrs = date_format($underthrs, "H");


                                                      $tundertime = $tundertime + $ftgvalue->undertime;


                                                     ///////////////////////////////////////////////////










                                                      ///////////////////////////
                                                      /////DECLARE VALS
                                                      /////////////////////////


                                                      $staffid  = $ftgvalue->staff_id;
                                                      $dates  = $ftgvalue->dates;
                                                      $late  = $combinedhrsmin;
                                                      $undertime  = $tundertime;
                                                      $regular  = $thours;
                                                      $overtime  = $ftgvalue->overtime;
                                                      $total_hours  = $ftgvalue->total_hours;
                                                      $ThisMonth =  $gmonth;
                                                      $cutoffperiod = $gcutoff;
                                                      $supervisors_ldhr_approval = "APPROVED";



                                                      $getsupvnmae = $wpdb->get_results("SELECT supervisors FROM `staff_almost_fullrecords` WHERE userid = '$staffid' AND inactive ='No' ");
                                                      foreach ($getsupvnmae as $key => $vspvtalue) {

                                                            $gsupvisors = $vspvtalue->supervisors;



                                                                  //INSERTING NEW RECORD

                                                                  // $sqlcout = $wpdb->insert("staff_cutoffs_records",
                                                                  // array(
                                                                  //     'staff_id' => $staffid,
                                                                  //     'dates'     => $dates,
                                                                  //     'late' => $late,
                                                                  //     'undertime' => $undertime,
                                                                  //     'regular' => $regular,
                                                                  //     'overtime' => $overtime,
                                                                  //     'total_hours' => $finaltotalhrs,
                                                                  //     'starting_cufoff' => $fmonthday,
                                                                  //     'ending_cufoff' => $ldayofmst,
                                                                  //     'supervisor' => $gsupvisors,
                                                                  //     'Month' => $ThisMonth,
                                                                  //     'cutoffperiod' => $cutoffperiod,
                                                                  //     'supervisors_ldhr_approval' => $supervisors_ldhr_approval

                                                                  // ));


                                                      }








                                                      ////////////////////////////////////////////////////////////////////////////
                                                      ///CALCULATING THE LATE AND UNDERTIME AND MINUS TO OVER ALL REGULAR HOURS
                                                     /////////////////////////////////////////////////////////////////////////////

                                                     $totallateuninmin = 0;
                                                     $finaltotalhrs  = 0;
                                                      $finalovtimes = 0;

                                                     $callateunder = $wpdb->get_results("SELECT  total_hours, dates, SUM(regular) as regular, SUM(late) as late, SUM(overtime) as overtime, SUM(undertime) as undertime, staff_id FROM `staff_cutoffs_records`  WHERE staff_id ='$staffid' AND Month = '$ThisMonth' GROUP BY staff_id, undertime,overtime, late, regular,dates,total_hours ");

                                                       foreach ($callateunder as $key => $fthoursvalue) {

                                                           $fnallateminutes = $fthoursvalue->late;
                                                           $fnalundertimnutes = $fthoursvalue->undertime;
                                                           $stffids = $fthoursvalue->staff_id;
                                                           $gfgdates = $fthoursvalue->dates;


                                                           /**
                                                           * GET THE TOTAL OVERTIME PER CUT OFF
                                                           */




                                                           $finaovertimes = $fthoursvalue->overtime;
                                                           $finalovtimes = $finalovtimes + $finaovertimes;


                                                           //ADD LATE AND UNDERTIME MINUTES THEN CONVERT TO HOUR
                                                           // THEN DIFF TO TOTAL REGULAR HOURS

                                                           $totallateuninmin = $fnallateminutes + $fnalundertimnutes;

                                                           //CONVERT TO HOUR

                                                           $convertedhrmins = $totallateuninmin / 60;

                                                           //GET TOTAL REGULAR HOURS THEN DIFF / MINUS THE TOTAL LATE AND UNDERTIME

                                                           $fftotalhrsff = $fthoursvalue->regular;


                                                           $finaltotalhrs = $finaltotalhrs + $fftotalhrsff;



                                                                 //INSERTING NEW RECORD

                                                                 $sqlcout = $wpdb->update("staff_cutoffs_records",
                                                                 array(

                                                                     'total_hours' => $finaltotalhrs


                                                                 ),
                                                               array('staff_id' => $stffids));

                                                               //UPDATING RECORDS

                                                               //$updnquery = $wpdb->query($wpdb->prepare("UPDATE staff_cutoffs_records SET overtime => '$finalovtimes' WHERE dates => '$gfgdates' "));




                                                       }










                                                   }





                                                 }



                                                $location = "https://igsl-portal.igsl.asia/admin-supervisor-approval-page/";
                                                wp_redirect( $location, $status = 302 );



      }



  }

?>


<?php


        /**
        ** OFFICIAL BUSINESS TRAVEL ADD FILED
        ** TO TIMESHEET RECORDS
        **/


        /**
        ** GET ALL OBT REQUEST THAT ARE APPROVED
        **/

            $timezone  = + 8; //(GMT +8:00) Philippines
            $gdatetoday = gmdate("d", time() + 3600*($timezone+date("I")));
            $gmonta = gmdate("m", time() + 3600*($timezone+date("I")));
            $gyearta = gmdate("Y", time() + 3600*($timezone+date("I")));

        if($gdatetoday > 5){

                $createdstt = $ldayofmst;

        }elseif ($gdatetoday < 6) {

            $gdatetoday = 5;
            $nexmonth = date('m', strtotime($fmonthday . ' +1 month'));


            $createdstt = $nexmonth . "/". $gdatetoday . "/" . $gyearta;
        }



        $obtappved = $wpdb->get_results("SELECT * FROM staff_obt_request_tabs  WHERE datefiled BETWEEN '$fmonthday' AND '$createdstt'  AND approval ='APPROVED' ");

        foreach ($obtappved as $key => $obtvalrec) {

        $gobtsdate = $obtvalrec->obt_start;
        $obtedate =  $obtvalrec->obt_end;
        $reqtype =  $obtvalrec->request_type;
        $obtstaffid = $obtvalrec->staff_id;

        if ($reqtype =='Hourly') {


             /**
             ** GET ONLY MONTH / DAY / YEAR
             **/

             $gdateonly = date_create($gobtsdate);
             $gfdateapp = date_format($gdateonly, 'm/d/Y');



              /**
              ** CHECK IF THE DATES ALREADY EXIST TO THE TIMESHEET
              **/

              /**
              ** CALCULATE THE TWO DATE DIFFERENCE
              **/





               $first_date = new DateTime($gobtsdate);
               $second_date = new DateTime($obtedate);
               $interval = date_diff($first_date, $second_date);
               $totaldiff =  $interval->format('%a');
               $addstday = $totaldiff + 1;


              $chkdatesh = $wpdb->get_results("SELECT COUNT(*) AS dateexist FROM `staff_timesheets_records` WHERE  dates = '$gfdateapp' AND staff_id= '$obtstaffid' ");
              foreach ($chkdatesh as $key => $hexvalue) {

                    $hdexistnow = $hexvalue->dateexist;



                    if($hdexistnow > 0){


                                 /**
                                  ** IF  EXIST UPDATE DATES
                                  ** TO THE SPECIFIC TIMESHEET RECORD
                                  **/


                                $gobtsdateh = $obtvalrec->obt_start;
                                $obtedateh =  $obtvalrec->obt_end;



                                $obtstaffid = $obtvalrec->staff_id;



                                $oifamorpm = $gobtsdateh;
                                $oifampmtime = date_create($oifamorpm);
                                $oifamorpmtimes = date_format($oifampmtime, 'a');
                                $uppercaseString = strtoupper($oifamorpmtimes);



                                if($uppercaseString == 'AM'){

                                  /**
                                  ** START DATE
                                  ** HALF DAY UPDATING OF DATE
                                  **/

                                  $stardaftesf = date_create($gobtsdateh);
                                  $ocfgfdatfeapp = date_format($stardaftesf, 'm/d/Y');


                                 /**
                                 ** UPDATE AM START TIME
                                 **/

                                 $ostardaftesfam = date_create($gobtsdateh);
                                 $ogtimeonlysas = date_format($ostardaftesfam, 'H:i');

                                 $starupdate = $wpdb->query($wpdb->prepare("UPDATE staff_timesheets_records SET clock_in ='$ogtimeonlysas' WHERE staff_id ='$obtstaffid' AND dates='$ocfgfdatfeapp' "));



                                }elseif ($uppercaseString == 'PM') {

                                  /**
                                  ** START DATE
                                  ** HALF DAY UPDATING OF DATE
                                  **/

                                  $stardaftesf = date_create($gdatesfiledstart);
                                  $cfgfdatfeapp = date_format($stardaftesf, 'm/d/Y');


                                /**
                                ** START DATE
                                ** HALF DAY UPDATING OF DATE
                                **/

                                $stardaftesf = date_create($gobtsdateh);
                                $ocfgfdatfeapp = date_format($stardaftesf, 'm/d/Y');




                                   /**
                                   ** UPDATE AM START TIME
                                   **/



                                   $ostardaftesfama = date_create($obtedateh);
                                   $oagtimeonlysas = date_format($ostardaftesfama, 'H:i');

                                   $starupdate = $wpdb->query($wpdb->prepare("UPDATE staff_timesheets_records SET clock_out ='$oagtimeonlysas' WHERE staff_id ='$obtstaffid' AND dates='$ocfgfdatfeapp' "));



                                }






                              }//CLOSING TAG FOR CHECKING EXIST RECORD IN TIMESHEET












                }//CLOSING TAG FOR OBT APPROVED LIST

    }
  }
?>


<?php
}else{
      echo "<br/>";
      echo "<h3 style='text-align:center'>You are not allowed to view this page</h3>";
      echo "<p style='text-align:center'>If you have any concerns regarding this, you can email us at: igsl-portal@igsl.asia</p>";
      echo "<br/>";

      if(!is_user_logged_in()) {
                 wp_redirect( home_url( '/wp-login.php' ), 302 );
                 exit();
                 }

}
 // closing tag for who are allowed roles

} //closing tag for login redirect
?>
