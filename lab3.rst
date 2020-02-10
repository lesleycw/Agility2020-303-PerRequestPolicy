NOTE: This lab has a publication error which I am currently correcting and will be completed by 2/10/2020


Lab 3: Custom Per Request Policy - Extended
===========================================

The purpose of this lab is to change the behavior of the custom Per Request Policies
built during Lab 2.  Lab attendees will expand policies by incorporating HTTP_Connector
agents to query external API's and incorporate Gating Criteria to enforce policy behavior
while accessing the lab application.
Students will configure the various aspects of this lab using the Visual Policy Editor,
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
|    entered for the purposes of this lab, these could have been referenced variables set      |
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
|    This configured resource uses a previously obtained oAuth Bearer Token and queries the    |
|                                                                                              |
|    Microsoft Graph API for the queried user's profile information.                           |
|                                                                                              |
|    Note: The Application (client_id) has been granted API Permissions for User.Read.All      |
+----------------------------------------------------------------------------------------------+
| |image007|                                                                                   |
|                                                                                              |
| |image008|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK 3: Extended Logon Subroutine
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. Navigate to **Access -> Profiles/Policies -> Per-Request Policies** and then click the    |
|                                                                                              |
|    **Edit** link for the **app.acme.com_prp** Per Request Policy.                            |
|                                                                                              |
|    Note: This may already be open.                                                           |
+----------------------------------------------------------------------------------------------+
| |image100|                                                                                   |
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
| |image009|                                                                                   |
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
| |image011|                                                                                   |
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
| |image012|                                                                                   |
|                                                                                              |
| |image013|                                                                                   |
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
| |image014|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| Note: The extending of Per Request Policies using the HTTP Connector can be leveraged to     |
|                                                                                              |
| query any Web Service or API endpoint.  In this case, MS Graph API is being leveraged to     |
|                                                                                              |
| retrieve additional information regarding a logged in user.                                  |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 10. In the **Logon** subroutine click the link for the **Variable Assign**.                  |
+----------------------------------------------------------------------------------------------+
| |image015|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 11. In the resulting **Variable Assign** window, in the **Variable Assign** section, click   |
|                                                                                              |
|     the **Add new entry** button three(3) times. Click the **change** link in the first      |
|                                                                                              |
|     **empty** row.                                                                           |
+----------------------------------------------------------------------------------------------+
| |image016|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 12. In the resulting assignment window use the following values:                             |
|                                                                                              |
|     **LEFT SIDE**                                                                            |
|                                                                                              |
|     - **Custom Variable**                                                                    |
|                                                                                              |
|     - **Unsecure**                                                                           |
|                                                                                              |
|     - **Text Window:** **session.custom.displayName**                                        |
|                                                                                              |
|     **RIGHT SIDE**                                                                           |
|                                                                                              |
|     - **Session Variable**                                                                   |
|                                                                                              |
|     - **Text Window:** **subsession.http_connector.body.displayName**                        |
|                                                                                              |
| 13. Click **Finished** once complete.                                                        |
+----------------------------------------------------------------------------------------------+
| |image017|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 14. Repeat the process again for the remaining two(2) **empty** rows using the values shown  |
|                                                                                              |
|     below.                                                                                   |
|                                                                                              |
| **ROW 2**                                                                                    |
|                                                                                              |
|   **LEFT SIDE**                                                                              |
|                                                                                              |
|   - **Custom Variable**                                                                      |
|                                                                                              |
|   - **Unsecure**                                                                             |
|                                                                                              |
|   - **Text Window:** **session.custom.jobTitle**                                             |
|                                                                                              |
|   **RIGHT SIDE**                                                                             |
|                                                                                              |
|   - **Session Variable**                                                                     |
|                                                                                              |
|   - **Text Window:** **subsession.http_connector.body.jobTitle**                             |
|                                                                                              |
| **ROW 3**                                                                                    |
|                                                                                              |
| - **LEFT SIDE**                                                                              |
|                                                                                              |
| -- **Custom Variable**                                                                       |
|                                                                                              |
| -- **Unsecure**                                                                              |
|                                                                                              |
| -- **Text Window:** **session.custom.mobilePhone**                                           |
|                                                                                              |
| - **RIGHT SIDE**                                                                             |
|                                                                                              |
| -- **Session Variable**                                                                      |
|                                                                                              |
| -- **Text Window:** **subsession.http_connector.body.mobilePhone**                           |
+----------------------------------------------------------------------------------------------+
| |image018|                                                                                   |
|                                                                                              |
| |image019|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 15. Review the **Variable Assign** and click **Save** once completed.                        |
+----------------------------------------------------------------------------------------------+
| |image020|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 16. In the **Per-Request Policy** section, click the **+ (Plus Symbol) on the **Allow**      |
|                                                                                              |
|     branch following the **Logon** subroutine and the **URL Branching** agent.               |
+----------------------------------------------------------------------------------------------+
| |image021|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 17. In the pop-up window, select the **General Purpose** tab, then click the radio button    |
|                                                                                              |
|     on the **HTTP Headers** action line, then click **Add Item**.                            |
+----------------------------------------------------------------------------------------------+
| |image022|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 18. In the resulting **HTTP Headers** window, click the **Add new entry** button three(3)    |
|                                                                                              |
|   times to add three(3) rows in the **Header Modify Section**.  Use the following values to  |
|                                                                                              |
|   complete each added row.                                                                   |
|                                                                                              |
| **ROW 1**                                                                                    |
|                                                                                              |
| - **Header Operation:** **replace**                                                          |
|                                                                                              |
| - **Header Name:** **displayName**                                                           |
|                                                                                              |
| - **Header Value:** **%{session.custom.displayName}**                                        |
|                                                                                              |
| **ROW 2**                                                                                    |
|                                                                                              |
| - **Header Operation:** **replace**                                                          |
|                                                                                              |
| - **Header Name:** **jobTitle**                                                              |
|                                                                                              |
| - **Header Value:** **%{session.custom.jobTitle}**                                           |
|                                                                                              |
| **ROW 3**                                                                                    |
|                                                                                              |
| - **Header Operation:** **replace**                                                          |
|                                                                                              |
| - **Header Name:** **mobilePhone**                                                           |
|                                                                                              |
| - **Header Value:** **%{session.custom.mobilePhone}**                                        |
|                                                                                              |
| 19. Click **Save** once completed.                                                           |
+----------------------------------------------------------------------------------------------+
| |image023|                                                                                   |
|                                                                                              |
| |image024|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK 4: Testing & Reviewing the Extended Logon Subroutine
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. Return to Firefox on the **Jumphost** test access to the **app.acme.com** application and |
|                                                                                              |
|    access App1.                                                                              |
+----------------------------------------------------------------------------------------------+
| |image025|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 2. Note the newly injected headers into **Application 1's** display page.                    |
+----------------------------------------------------------------------------------------------+
| |image026|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 3. Return to **bigip1.f5lab.local**, navigate to **Access -> Overview -> Active Sessions**.  |
|                                                                                              |
|    Expand the **+ (Plus Symbol)** to see the subsession.                                     |
|                                                                                              |
| 4. Click on the **View** link in the **Variables** column for the listed subsession.         |
+----------------------------------------------------------------------------------------------+
| |image027|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 5  Review the variables collected via the HTTP Connector Requests.                           |
+----------------------------------------------------------------------------------------------+
| |image028|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 6. Navigate to **Access -> Overview -> Active Sessions**. Click on the **View** link in the  |
|                                                                                              |
|    **Variables** column for the listed session.                                              |
+----------------------------------------------------------------------------------------------+
| |image100|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 7  Review the actions in the Session log, particularly those associated with HTTP Connector  |
|                                                                                              |
|    Requests.                                                                                 |
+----------------------------------------------------------------------------------------------+
| |image029|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK 5: Configuring Gating Criteria 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. Navigate to **Access -> Profiles/Policies -> Per-Request Policies** and then click the    |
|                                                                                              |
|    **Edit** link for the **app.acme.com_prp** Per Request Policy.                            |
|                                                                                              |
|    Note: This may already be open.                                                           |
+----------------------------------------------------------------------------------------------+
| |image100|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 2. In the resulting Visual Policy Editor window for **app.acme.com_prp**, expand the         |
|                                                                                              |
|    **Logon** subroutine and click the **Subroutine Settings/Rename** link.                   |
+----------------------------------------------------------------------------------------------+
| |image030|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 3. In the pop-up window, in the **Gating Criteria** field, enter                             |
|                                                                                              |
|    **perflow.client.ip.address** and click **Save**.                                         |
+----------------------------------------------------------------------------------------------+
| |image031|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK 6: Testing Gating Criteria 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. Return to Firefox on the **Jumphost** test access to the **app.acme.com** application and |
|                                                                                              |
|    access App1. Re-login to the application if necessary.                                    |
+----------------------------------------------------------------------------------------------+
| |image100|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 2. Confirm on that your session is active on **bigip1.f5lab.local**, by navigating to        |
|                                                                                              |
|    **Access -> Overview -> Active Sessions**. Expand the **+ (Plus Symbol)** to see the      |
|                                                                                              |
|     subsession.                                                                              |
+----------------------------------------------------------------------------------------------+
| |image100|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 3. Return to the **Jumphost**.  Do **NOT** close the browser and the already opened          |
|                                                                                              |
|    application.                                                                              |
|                                                                                              |
| 4. Navigate to the Jumphost desktop and click on the **Change IP 10.1.10.11** link (Confirm  |
|                                                                                              |
|    the elevated Administrator privlege).                                                     |
|                                                                                              |
| 5. Return to Firefox and the **app.acme.com** application by accessing App1 again. Note that |
|                                                                                              |
|    you will be re-prompted for access.                                                       |
+----------------------------------------------------------------------------------------------+
| |image100|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 6. Return to **bigip1.f5lab.local**, and navigate to **Access -> Overview -> Active**        |
|                                                                                              |
|    **Sessions**. Expand the **+ (Plus Symbol)** to see the two(2) subsessions now associated |
|                                                                                              |
|     with your session. (You may alternatively refresh the screen if already opened.          |
+----------------------------------------------------------------------------------------------+
| |image100|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| Note: The are multiple examples of Gating Criteria. In this example, client IP was used to   |
|                                                                                              |
| show that any changes in the connecting entity can result in establishing a new subsession.  |
|                                                                                              |
| What happens in new subsessions, the number of subsessions and how they are controlled is    |
|                                                                                              |
| based on customer/application need.                                                          |
+----------------------------------------------------------------------------------------------+
| |image100|                                                                                   |
+----------------------------------------------------------------------------------------------+


TASK 7: End of Lab3
~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. This concludes Lab3, feel free to review and test the configuration.                      |
+----------------------------------------------------------------------------------------------+
| |image000|                                                                                   |
+----------------------------------------------------------------------------------------------+

.. |image001| image:: media/lab3-001.png
   :width: 4.5in
   :height: 2.32in
.. |image002| image:: media/lab3-002.png
   :width: 4.5in
   :height: 2.32in
.. |image003| image:: media/lab3-003.png
   :width: 4.5in
   :height: 2.32in
.. |image004| image:: media/lab3-004.png
   :width: 4.5in
   :height: 2.32in
.. |image005| image:: media/lab3-005.png
   :width: 4.5in
   :height: 2.32in
.. |image006| image:: media/lab3-006.png
   :width: 4.5in
   :height: 2.32in
.. |image007| image:: media/lab3-007.png
   :width: 4.5in
   :height: 2.32in
.. |image008| image:: media/lab3-008.png
   :width: 4.5in
   :height: 2.32in
.. |image009| image:: media/lab3-009.png
   :width: 4.5in
   :height: 2.32in
.. |image010| image:: media/lab3-010.png
   :width: 4.5in
   :height: 2.32in
.. |image011| image:: media/lab3-011.png
   :width: 4.5in
   :height: 2.32in
.. |image012| image:: media/lab3-012.png
   :width: 4.5in
   :height: 2.32in
.. |image013| image:: media/lab3-013.png
   :width: 4.5in
   :height: 2.32in
.. |image014| image:: media/lab3-014.png
   :width: 4.5in
   :height: 2.32in
.. |image015| image:: media/lab3-015.png
   :width: 4.5in
   :height: 2.32in
.. |image016| image:: media/lab3-016.png
   :width: 4.5in
   :height: 2.32in
.. |image017| image:: media/lab3-017.png
   :width: 4.5in
   :height: 2.32in
.. |image018| image:: media/lab3-018.png
   :width: 4.5in
   :height: 2.32in
.. |image019| image:: media/lab3-019.png
   :width: 4.5in
   :height: 2.32in
.. |image020| image:: media/lab3-020.png
   :width: 4.5in
   :height: 2.32in
.. |image021| image:: media/lab3-021.png
   :width: 4.5in
   :height: 2.32in
.. |image022| image:: media/lab3-022.png
   :width: 4.5in
   :height: 2.32in
.. |image023| image:: media/lab3-023.png
   :width: 4.5in
   :height: 2.32in
.. |image024| image:: media/lab3-024.png
   :width: 4.5in
   :height: 2.32in
.. |image025| image:: media/lab3-025.png
   :width: 4.5in
   :height: 2.32in
.. |image026| image:: media/lab3-026.png
   :width: 4.5in
   :height: 2.32in
.. |image027| image:: media/lab3-027.png
   :width: 4.5in
   :height: 2.32in
.. |image028| image:: media/lab3-028.png
   :width: 4.5in
   :height: 2.32in
.. |image029| image:: media/lab3-029.png
   :width: 4.5in
   :height: 2.32in
.. |image030| image:: media/lab3-030.png
   :width: 4.5in
   :height: 2.32in
.. |image031| image:: media/lab3-031.png
   :width: 4.5in
   :height: 2.32in
.. |image032| image:: media/lab3-032.png
   :width: 4.5in
   :height: 2.32in
.. |image033| image:: media/lab3-033.png
   :width: 4.5in
   :height: 2.32in
.. |image034| image:: media/lab3-034.png
   :width: 4.5in
   :height: 2.32in
.. |image035| image:: media/lab3-035.png
   :width: 4.5in
   :height: 2.32in
.. |image036| image:: media/lab3-036.png
   :width: 4.5in
   :height: 2.32in
.. |image037| image:: media/lab3-037.png
   :width: 4.5in
   :height: 2.32in
.. |image038| image:: media/lab3-038.png
   :width: 4.5in
   :height: 2.32in
.. |image039| image:: media/lab3-039.png
   :width: 4.5in
   :height: 2.32in
.. |image040| image:: media/lab3-040.png
   :width: 4.5in
   :height: 2.32in
.. |image041| image:: media/lab3-041.png
   :width: 4.5in
   :height: 2.32in
.. |image042| image:: media/lab3-042.png
   :width: 4.5in
   :height: 2.32in
.. |image043| image:: media/lab3-043.png
   :width: 4.5in
   :height: 2.32in
.. |image044| image:: media/lab3-044.png
   :width: 4.5in
   :height: 2.32in
.. |image045| image:: media/lab3-045.png
   :width: 4.5in
   :height: 2.32in
.. |image046| image:: media/lab3-046.png
   :width: 4.5in
   :height: 2.32in
.. |image047| image:: media/lab3-047.png
   :width: 4.5in
   :height: 2.32in
.. |image048| image:: media/lab3-048.png
   :width: 4.5in
   :height: 2.32in
.. |image049| image:: media/lab3-049.png
   :width: 4.5in
   :height: 2.32in
.. |image050| image:: media/lab3-050.png
   :width: 4.5in
   :height: 2.32in
.. |image051| image:: media/lab3-051.png
   :width: 4.5in
   :height: 2.32in
.. |image052| image:: media/lab3-052.png
   :width: 4.5in
   :height: 2.32in
.. |image053| image:: media/lab3-053.png
   :width: 4.5in
   :height: 2.32in
.. |image054| image:: media/lab3-054.png
   :width: 4.5in
   :height: 2.32in
.. |image055| image:: media/lab3-055.png
   :width: 4.5in
   :height: 2.32in
.. |image056| image:: media/lab3-056.png
   :width: 4.5in
   :height: 2.32in
.. |image057| image:: media/lab3-057.png
   :width: 4.5in
   :height: 2.32in
.. |image058| image:: media/lab3-058.png
   :width: 4.5in
   :height: 2.32in
.. |image059| image:: media/lab3-059.png
   :width: 4.5in
   :height: 2.32in
.. |image060| image:: media/lab3-060.png
   :width: 4.5in
   :height: 2.32in
.. |image061| image:: media/lab3-061.png
   :width: 4.5in
   :height: 2.32in
.. |image062| image:: media/lab3-062.png
   :width: 4.5in
   :height: 2.32in   
.. |image063| image:: media/lab3-063.png
   :width: 4.5in
   :height: 2.32in  
.. |image064| image:: media/lab3-064.png
   :width: 4.5in
   :height: 2.32in
.. |image065| image:: media/lab3-065.png
   :width: 4.5in
   :height: 2.32in