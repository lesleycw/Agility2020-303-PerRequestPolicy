Lab 3: Custom Per Request Policy - Extended
===========================================

The purpose of this lab is change the behaviour of the custom Per Request Policies
built during Lab2.  Lab attendees will expand policies by incoporating HTTP_Connector
agents to query external API's and incorporate gating critera to enforce policy behavior
while accessing the provided application.
Students will configure the various aspects using the Visual Policy Editor,
review the configuration and perform tests of the deployment.

Objective:
----------

-  Gain a deeper understanding of Per Request Policies and their applicability
   in various delivery and control scenarios.

-  Gain a further understanding of Per Request Policy Subroutines and their
   expandaility with HTTP_Connector and gating criteria.

Lab Requirements:
-----------------

-  All Lab requirements will be noted in the tasks that follow

-  Estimated completion time: 20 minutes.

Lab 3 Tasks:
-----------------

TASK 1: Prepare Lab Environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. On **bigip1.f5lab.local**, navigate to **Access -> Overview -> Active Sessions** and      |
|                                                                                              |
|    confirm all active sessions have been killed.                                             |
|                                                                                              |
| 2. If any sessions are active, click all checkboxes by the active session and the click      |
|                                                                                              |
|    **Kill Selected Sessions** button.  In the resulting dialogue window ensure the           |
|                                                                                              |
|    **Session ID/Subsession ID** is checked and click the **Delete** button.                  |
|                                                                                              |
| 3. Close any open browser windows on the Jumphost desktop.                                   |
|                                                                                              |
|    This prepares the environment for further user testing.                                   |
+----------------------------------------------------------------------------------------------+
| |image001|                                                                                   |
|                                                                                              |
| |image002|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK 2: Review HTTP Connector Configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. On **bigip1.f5lab.local**, navigate to **Access -> Authentication -> HTTP Connector ->**  |
|                                                                                              |
|    **HTTP Connector Transport**.                                                             |
|                                                                                              |
| 2. Click on the **http_connector_transport** link.                                           |
|                                                                                              |
|    This configured resource provides DNS resolution and HTTPS functionality enabling access  |
|                                                                                              |
|    to queried Web Service and API endpoints.                                                 |
+----------------------------------------------------------------------------------------------+
| |image003|                                                                                   |
|                                                                                              |
| |image004|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 1. Navigate to **Access -> Authentication -> HTTP Connector -> HTTP Connector Request**.     |
|                                                                                              |
| 2. Click on the **MSGraphAPI_RequestToken** link.                                            |
|                                                                                              |
|    This configured resource retrieves an oAuth Bearer Token to be used to query the          |
|                                                                                              |
|    Microsoft Graph API.                                                                      |
|                                                                                              |
|    Note: While values like tenant_id, client_id & client_secret have been statically         |
|                                                                                              |
|    entered for the purposes of this lab, these could have been referenced varibles set       |
|                                                                                              |
|    in the Per Request Policy flow.                                                           |
+----------------------------------------------------------------------------------------------+
| |image005|                                                                                   |
|                                                                                              |
| |image006|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 1. Navigate to **Access -> Authentication -> HTTP Connector -> HTTP Connector Request**.     |
|                                                                                              |
| 2. Click on the **MSGraphAPI_GetUserProfile** link.                                          |
|                                                                                              |
|    This configured resource uses a previsouly obtained oAuth Bearer Token and queries the    |
|                                                                                              |
|    Microsoft Graph API for the queried user's proflie information.                           |
|                                                                                              |
|    Note: The Application (client_id) has been granted API Permissions for User.Read.All      |
+----------------------------------------------------------------------------------------------+
| |image007|                                                                                   |
|                                                                                              |
| |image008|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK 3: Extened Logon Subroutine
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. Navigate to **Access -> Profiles/Policies -> Per-Request Policies** and then click the    |
|                                                                                              |
|    **Edit** link for the **app.acme.com_prp** Per Request Policy.                            |
|                                                                                              |
|    Note: This may already be open.                                                           |
+----------------------------------------------------------------------------------------------+
| |image009| (lab2 image 9)                                                                    |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 2. In the resulting Visual Policy Editor window for the On  **app.acme.com_prp**, expand the |
|                                                                                              |
|    **Logon** subroutine and click the **+ (Plus Symbol) on the **Successful** branch         |
|                                                                                              |
|    following the **AD Query** and before the **Variable Assign**.                            |
|                                                                                              |
| 3. In the pop-up window, select the **General Purpose** tab, then click the radio button     |
|                                                                                              |
|    on the **HTTP Connector** action line, then click **Add Item**.                           |
+----------------------------------------------------------------------------------------------+
| |image010|                                                                                   |
|                                                                                              |
| |image010|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 4. In the resulting **HTTP Connector** window, change the **Name** field to **MSGraphAPI**   |
|                                                                                              |
|    **Request Token**.                                                                        |
|                                                                                              |
| 5. In the **HTTP Connector** section, Select **/Common/MSGraphAPI_RequestToken** from the    |
|                                                                                              |
|    the drop down for **HTTP Connector Request** and then click **Save**.                     |
+----------------------------------------------------------------------------------------------+
| |image010|                                                                                   |
|                                                                                              |
| |image010|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 6. In the **Logon** subroutine and click the **+ (Plus Symbol) on the **Successful** branch  |
|                                                                                              |
|    following the **MSGraphAPI Request Token** and before the **Variable Assign**.            |    
|                                                                                              |
| 7. In the pop-up window, select the **General Purpose** tab, then click the radio button     |
|                                                                                              |
|    on the **HTTP Connector** action line, then click **Add Item**.                           |
+----------------------------------------------------------------------------------------------+
| |image010|                                                                                   |
|                                                                                              |
| |image010|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 8. In the resulting **HTTP Connector** window, change the **Name** field to **MSGraphAPI**   |
|                                                                                              |
|    **Get User Profile**.                                                                     |
|                                                                                              |
| 9. In the **HTTP Connector** section, Select **/Common/MSGraphAPI_GetUserProfile** from the  |
|                                                                                              |
|    the drop down for **HTTP Connector Request** and then click **Save**.                     |
+----------------------------------------------------------------------------------------------+
| |image010|                                                                                   |
|                                                                                              |
| |image010|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| Note: The extending of Per Request Policies using the HTTP Connector can be leveraged to     |
|                                                                                              |
|       query any Web Service or API endpoint.  In this case, MS Graph API is being leveraged  |
|                                                                                              |
|       to retrieve additional information regarding a logged in user.                         |
+----------------------------------------------------------------------------------------------+
| |image010|                                                                                   |
|                                                                                              |
| |image010|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 10. In the **Logon** subroutine click the link for the **Variable Assign**.                  |    
+----------------------------------------------------------------------------------------------+
| |image010|                                                                                   |
|                                                                                              |
| |image010|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 11. In the resulting **Variable Assign** window, in the **Variable Assign** section, click   |
|                                                                                              |
|     the **Add new entry** button three(3) times. Click the **change** link in the first      |
|                                                                                              |
|     **empty** row.                                                                           |
|                                                                                              |
| 12. In the resulting assignment window use the following values:                             |
|                                                                                              |
|     **LEFT SIDE**                                                                            |
|                                                                                              |
|     - **Custom Variable**                                                                    |
|                                                                                              |
|     - **Unsecure**                                                                           |
|                                                                                              |
|     - Text Window: **session.custom.displayName**                                            |
|                                                                                              |
|     **RIGHT SIDE**                                                                           |
|                                                                                              |
|     - **Session Variable**                                                                   |
|                                                                                              |
|     - Text Window: **subsession.http_connector.body.displayName**                            |
|                                                                                              |
| 13. Click **Finished** once complete.                                                        |
+----------------------------------------------------------------------------------------------+
| |image010|                                                                                   |
|                                                                                              |
| |image010|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 14. Repeat the process again for the remaing two(2) **empty** rows using the values shown    |
|                                                                                              |
|     below.                                                                                   |
|                                                                                              |
| ROW 2                                                                                        |
|                                                                                              |
|     **LEFT SIDE**                                                                            |
|                                                                                              |
|     - **Custom Variable**                                                                    |
|                                                                                              |
|     - **Unsecure**                                                                           |
|                                                                                              |
|     - Text Window: **session.custom.jobTitle**                                               |
|                                                                                              |
|     **RIGHT SIDE**                                                                           |
|                                                                                              |
|     - **Session Variable**                                                                   |
|                                                                                              |
|     - Text Window: **subsession.http_connector.body.jobTitle**                               |
|                                                                                              |
| ROW 3                                                                                        |
|                                                                                              |
|     **LEFT SIDE**                                                                            |
|                                                                                              |
|     - **Custom Variable**                                                                    |
|                                                                                              |
|     - **Unsecure**                                                                           |
|                                                                                              |
|     - Text Window: **session.custom.mobilePhone**                                            |
|                                                                                              |
|     **RIGHT SIDE**                                                                           |
|                                                                                              |
|     - **Session Variable**                                                                   |
|                                                                                              |
|     - Text Window: **subsession.http_connector.body.mobilePhone**                            |
+----------------------------------------------------------------------------------------------+
| |image010|                                                                                   |
|                                                                                              |
| |image010|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 15. Review the **Variable Assign** and click **Save** once completed.                        |
+----------------------------------------------------------------------------------------------+
| |image010|                                                                                   |
|                                                                                              |
| |image010|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 16. In the **Per-Request Policy** section, click the **+ (Plus Symbol) on the **Allow**      |
|                                                                                              |
|     branch following the **Logon** subroutine and the **URL Branching** agent.               |
|                                                                                              |
| 17. In the pop-up window, select the **General Purpose** tab, then click the radio button    |
|                                                                                              |
|     on the **HTTP Headers** action line, then click **Add Item**.                            |
+----------------------------------------------------------------------------------------------+
| |image010|                                                                                   |
|                                                                                              |
| |image010|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 18. In the resulting **HTTP Headers** window, click the **Add new entry** button three(3)    |
|                                                                                              |
|    times to add three(3) rows in the **Header Modify Section**.  Use the following values to |
|                                                                                              |
|    complete each added row.                                                                  |
|                                                                                              |
| ROW 1                                                                                        |
|                                                                                              |
|     **Header Operation:** **replace**                                                        |
|                                                                                              |
|     **Header Name:** **displayName**                                                         |
|                                                                                              |
|     **Header Value:** **%{session.custom.displayName} **                                     |
|                                                                                              |
| ROW 2                                                                                        |
|                                                                                              |
|     **Header Operation:** **replace**                                                        |
|                                                                                              |
|     **Header Name:** **jobTitle**                                                            |
|                                                                                              |
|     **Header Value:** **%{session.custom.jobTitle} **                                        |
|                                                                                              |
| ROW 3                                                                                        |
|                                                                                              |
|     **Header Operation:** **replace**                                                        |
|                                                                                              |
|     **Header Name:** **mobilePhone**                                                         |
|                                                                                              |
|     **Header Value:** **%{session.custom.mobilePhone} **                                     |
+----------------------------------------------------------------------------------------------+
| |image010|                                                                                   |
|                                                                                              |
| |image010|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 19. Click **Save** once completed.                                                           |
+----------------------------------------------------------------------------------------------+
| |image010|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK 4: Testing the Extened Logon Subroutine
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. Return to Firefox on the **Jumphost** test access to the **app.acme.com** application and |
|                                                                                              |
|    access App1.                                                                              |
+----------------------------------------------------------------------------------------------+
| |image009| (lab2 image 9)                                                                    |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 2. In the resulting Visual Policy Editor window for the On  **app.acme.com_prp**, expand the |
|                                                                                              |
|    **Logon** subroutine and click the **+ (Plus Symbol) on the **fallback** branch following |
|                                                                                              |
|    the **Variable Assign**.                                                                  |
|                                                                                              |
| 3. In the pop-up window, select the **General Purpose** tab, then click the radio button     |
|                                                                                              |
|    on the **HTTP Connector** action line, then click **Add Item**.                           |
+----------------------------------------------------------------------------------------------+
| |image010|                                                                                   |
|                                                                                              |
| |image010|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 4. In the resulting HTTP Connector window, change the **Name** field to **MSGraphAPI**       |
|                                                                                              |
|    **Request Token**.                                                                        |
|                                                                                              |
| 5. In the **HTTP Connector** section, Select **/Common/MSGraphAPI_RequestToken** from the    |
|                                                                                              |
|    the drop down for **HTTP Connector Request** and then click **Save**.                     |
+----------------------------------------------------------------------------------------------+
| |image010|                                                                                   |
|                                                                                              |
| |image010|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 6. In the **Logon** subroutine and click the **+ (Plus Symbol) on the **Successful** branch  |
|                                                                                              |
|    following the **MSGraphAPI Request Token**.                                               |    
|                                                                                              |
| 7. In the pop-up window, select the **General Purpose** tab, then click the radio button     |
|                                                                                              |
|    on the **HTTP Connector** action line, then click **Add Item**.                           |
+----------------------------------------------------------------------------------------------+
| |image010|                                                                                   |
|                                                                                              |
| |image010|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 8. In the resulting HTTP Connector window, change the **Name** field to **MSGraphAPI**       |
|                                                                                              |
|    **Get User Profile**.                                                                     |
|                                                                                              |
| 9. In the **HTTP Connector** section, Select **/Common/MSGraphAPI_GetUserProfile** from the  |
|                                                                                              |
|    the drop down for **HTTP Connector Request** and then click **Save**.                     |
+----------------------------------------------------------------------------------------------+
| |image010|                                                                                   |
|                                                                                              |
| |image010|                                                                                   |
+----------------------------------------------------------------------------------------------+


+----------------------------------------------------------------------------------------------+
| Note: The extending of Per Request Policies using the HTTP Connector can be leveraged to     |
|                                                                                              |
|       query any Web Service or API endpoint.  In the case, MS Graph API is being leveraged   |
|                                                                                              |
|       to retrieve additional information regarding a logged in user.                         |
+----------------------------------------------------------------------------------------------+
| |image010|                                                                                   |
|                                                                                              |
| |image010|                                                                                   |
+----------------------------------------------------------------------------------------------+


.. |image001| image:: media/lab3-001.png
   :width: 4.5in
   :height: 2.32in
