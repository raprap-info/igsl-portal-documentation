


# IGSL Dashboard Plugin - API and Template Files

This document outlines various API endpoints and template files found within the `igsl_dashboard` plugin, along with their descriptions. These files are crucial for the plugin's functionality, serving data or rendering specific views.

---

## API Endpoints

The following PHP files serve as API endpoints, providing data to different parts of the application or external services:

* **`api_all_igslbooked.php`**
    * **Description:** This API endpoint is responsible for fetching and providing data related to **all booked items or services within IGSL**. This could include room bookings, equipment reservations, or event registrations.

* **`api_allmaintenances.php`**
    * **Description:** This API provides a comprehensive list of **all maintenance requests or records**. It is likely used to display ongoing, pending, or completed maintenance tasks across various facilities or equipment.

* ****`api_all_userencoded_users.php`**
    * **Description:** This API is designed to retrieve data for **all users encoded or registered within the system**. It might provide details like user IDs, names, and other relevant information for administrative purposes.

* **`api_vanrequest.php`**
    * **Description:** This API endpoint serves a list of **all van transportation requests**. It's crucial for managing and tracking vehicle requests for staff or students.

* **`api_all_sports_reqlist.php`**
    * **Description:** This API provides a list of **all sports-related requests**. This could include bookings for sports facilities, equipment requests, or participation registrations for sports activities.

* **`api_trust_account_finan.php`**
    * **Description:** This API is dedicated to fetching **financial data related to trust accounts**. It likely provides details for financial reporting and management within the IGSL context.

* **`api_alluserfportaldash.php`**
    * **Description:** This API is used to **fetch data for all WordPress users** that are displayed or managed via the user portal dashboard. It acts as a bridge to pull user information into the custom dashboard interface.

* **`api_latest_rc_list.php`**
    * **Description:** This API provides the **most current list of Responsibility Centers (RCs)**. This is essential for ensuring that financial and administrative data is categorized under the correct RCs.

* **`api_all_original_rc_vendorlist.php`**
    * **Description:** This API serves a comprehensive list of **all original Responsibility Centers and Vendor Names**. This likely acts as a master reference for financial transactions and vendor management.

---


## Path URLs

Here are the available API endpoints:

- **Maintenance API**  
  `/api/maintenance/`

- **IGSL Facilities API**  
  `/api/igsl-facilities/`

- **Van Request API**  
  `/api/vanrequest/`

- **Trust Account API**  
  `/api/trust-account/`

- **Sports API**  
  `/api/sports/`

- **Trust API**  
  `/api/trust-account/`

- **RC Centre API**  
  `/api/latest-responsibility-centre-api/`

  - **RC Centre API**  
  `/api/latest-responsibility-centre-api/`

  - **Portal User API**  
  `/api/portal-all-wp-users/`

