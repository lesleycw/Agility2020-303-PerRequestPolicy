Lab 1: Access Guided Configuration - PerRequest Policy
======================================================

The purpose of this lab is to leverage Access Guided Configuration (AGC) to 
deploy an Identity Aware Proxy extended by Per Request Policies (PRP) access 
controls. The Per Request Policies will restict access based on AD Group 
Membership and the URI accessed. Students will configure the various aspects 
of the application using strictly AGC, review the configuration and perform 
tests of the deployment.

Objective:
----------

-  Gain an understanding of Access Guided Configruration configurations and
   its various configurations and deployment models

-  Gain an initial understanding of Per Request Policies and their applicability
   in various delivery and control scenarios

Lab Requirements:
-----------------

-  All Lab requirements will be noted in the tasks that follow

-  Estimated completion time: 30 minutes

Lab 1 Tasks:
-----------------

TASK 1: Intialize Access Guided Configuration (AGC)
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. Login to your provided lab Virtual Edition: **bigp1.f5lab.local**                         |
|                                                                                              |
| 2. Navigate to:  **Access -> Guided Configuration**                                          |
|                                                                                              |
| 3. Click the **Zero Trust** graphic as shown.                                                |
+----------------------------------------------------------------------------------------------+
| |image001|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 4. Click on the **Identity Aware Proxy**  dialogue box click under **Zero Trust**            |
|                                                                                              |
|    in the navigation as shown.                                                               | 
+----------------------------------------------------------------------------------------------+
| |image002|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 5. Review the **Identity Aware Proxy Application** configuration example presented.          |
|                                                                                              |
| 6. Scroll through and review the remaining element of the dialogue box to the bottom of the  |
|                                                                                              |
|    screen and click "Next"                                                                   |
+----------------------------------------------------------------------------------------------+
| |image003|                                                                                   |
| |image004|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK 2: Name Configuration and define Device Posture  
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. In the **Configuration Name** dialogue box, enter **agc-app.acme.com**                    |
|                                                                                              |
| 2. Click **Save & Next** at the bottom of the dialogue window.                               |
+----------------------------------------------------------------------------------------------+
| |image005|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK: 3: Configure Virtual Server Properties 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. Select the **Create New** radio button under **Virtual Server**                           |
|                                                                                              |
| 2. Select the **Host** radio button under **Destination Address**                            |
|                                                                                              |
| 3. Enter the IP Address **10.1.10.100** in the dialogue box for **Destination Address**.     |
|                                                                                              |
| 4. Confirm the **Rediect Port** is **80** and **HTTP**.                                      |                                                                                             
|                                                                                              |
| 5. Select the **Use Existing** radio button under **Client SSL Profile**                     |
|                                                                                              |
| 6. Move the **f5demo** Client SSL Profile to the left, **Selected**                          |
|                                                                                              |
| 7. Click **Save & Next** at the bottom of the dialogue window.                               |
+----------------------------------------------------------------------------------------------+
| |image006|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK: 4: Configure User Identity  
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. Enter **agc-f5lab-AD** in the **Name** field                                              |
|                                                                                              |
| 2. Confirm **Authentication Type** is **AAA**                                                |
|                                                                                              |
| 3. Confirm **Choose Authentication Server Type** is **Active Directory**                     |
|                                                                                              |
| 4. Select **f5lab.local** from the **Choose Authentication Server** drop down.               |
|                                                                                              |
| 5. Check the **Active Directory Query Properties** checkbox.                                 |
|                                                                                              |
| 6. Check the **Fetch Nested Group** checkbox.                                                |
|                                                                                              |
| 7. Move the **memberOf** to the left under **Required Attributes**                           |
|                                                                                              |
| 8. Click **Save & Next** at the bottom of the dialogue window.                               |
+----------------------------------------------------------------------------------------------+
| |image007|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 9. In the dialogue window that follows for **User Identity**, confirm **agc-f5lab-AD** is    |
|                                                                                              |
|    listed, then click **Save & Next** at the bottom if the dialogue window.                  |
+----------------------------------------------------------------------------------------------+
| |image008|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK 5: Multi Factor Authentication
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. In the **Multi Factor Authenticatio** dialogue box, click **Save & Next** at the bottom   |
|                                                                                              |
|    of the dialogue window.                                                                   |
+----------------------------------------------------------------------------------------------+
| |image009|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK 6: Single Sign-on & HTTP Header
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. Check **Enable Single Sign-on (Optional)** checkbox in the                                |
|                                                                                              |
|    **Single Sign-on & HTTP Header** dialogue window.                                         |
+----------------------------------------------------------------------------------------------+
| |image010|                                                                                   |
+----------------------------------------------------------------------------------------------+
 
+----------------------------------------------------------------------------------------------+
| 2. Enter **agc-app-header** in the **Name** field in the **Single Sign-on & HTTP Header**    |
|                                                                                              |
|    **Properties** dialogue window.                                                           |
|                                                                                              |
| 3. Select the **HTTP Headers** radio button under **Type**                                   |
|                                                                                              |
| 4. Click the **+ (Plus Symbol)** in the **Action** column of the **SSO Headers** section.    |
|                                                                                              |
| 5. In the new **SSO Headers** row, enter the following values:                               |
|                                                                                              |
|    - **Header Operation**: **replace**                                                       |
|                                                                                              |
|    - **Header Name**: **agc-app-uid**                                                        |
|                                                                                              |
|    - **Header Value**: **%{subsession.logon.last.username}**                                 |
|                                                                                              |
| 6. Repeat steps 4 & 5 with the following values:                                             |
|                                                                                              |
|    - **Header Operation**: **replace**                                                       |
|                                                                                              |
|    - **Header Name**: **agc-app-uid**                                                        |
|                                                                                              |
|    - **Header Value**: **%{subsession.logon.last.username}**                                 |
|                                                                                              |
| 7. At the bottom of the screen, click **Save**                                               |
+----------------------------------------------------------------------------------------------+
| |image011|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 8. In the dialogue window that follows for **Single Sign-on & HTTP Header**, confirm         |
|                                                                                              |
|    **agc-app-header** is listed, then click **Save & Next** at the bottom if the             |
|                                                                                              |
|    dialogue window.                                                                          |
+----------------------------------------------------------------------------------------------+
| |image012|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK 7: Applications
~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. Check **Enable Single Sign-on (Optional)** checkbox in the                                |
|                                                                                              |
|    **Single Sign-on & HTTP Header** dialogue window.                                         |
+----------------------------------------------------------------------------------------------+
| |image013|                                                                                   |
+----------------------------------------------------------------------------------------------+
  
+----------------------------------------------------------------------------------------------+
| 2. **Application Properties** dialogue window, click *Show Advanced Setting** in the upper   |
|                                                                                              |
|    right hand corner of the dialogue window.                                                 |
|                                                                                              |
| 3. In the **Name** field enter **agc-app.acme.com**.                                         |
|                                                                                              |
| 4. In the **FQDN** field enter **app.acme.com**.                                             |
|                                                                                              |
| 5. In the **Subpath Pattern** field enter **/apps/app1* **.                                  |
|                                                                                              |
| 6. On the **Subpath Pattern** row entered in Step 5, click the **+ (Plus Symbol)** twice     |
|                                                                                              |
|    to add to more rows.                                                                      |
|                                                                                              |
| 7. In the two new rows add **/apps/app2* ** and **/apps/app3* ** respectively.               |
|                                                                                              |
| 8. In the **Pool Configuration** section, under **Health Monitors** area move                |
|                                                                                              |
|    **/Common/http** to the left **Selected** side.                                           |
|                                                                                              |
| 9. In the **Pool Configuration** section, under **Load Balancing Method** area select        |
|                                                                                              |
|    **/Common/10.1.20.6** from the **IP Address/Node name**                                   |
|                                                                                              |
| 10. Click the **Save** button at the bottom of the dialogue window.                          |
+----------------------------------------------------------------------------------------------+
| |image014|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 11. In the **Applications** dialogue window that follows, expand the **Subpaths** and ensure |
|                                                                                              |
|    app are present for the **agc-app.acme.com row.                                           |
|                                                                                              |
| 12. Click the **Save & Next** button at the bottom of the dialogue window.                   |
+----------------------------------------------------------------------------------------------+
| |image015|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK 8: Application Groups
~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. Check the **Enable Application Groups** checkbox in the **Application Groups**            |
|                                                                                              |
|    dialogue window.                                                                          |
+----------------------------------------------------------------------------------------------+
| |image016|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 2. **Application Group Properties** dialogue window, enter **app1** in the **Field**.        |
|                                                                                              |
| 3. Move **/apps/app1\* ** from the **Available** side to the **Selected** side under          |
|                                                                                              |
|    **Application List**.                                                                     |
|                                                                                              |
| 4. Click the **Save** button at the bottom of the dialogue window.                           |
+----------------------------------------------------------------------------------------------+
| |image017|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 5. Click the **Add* button in the *Application Groups** dialogue window that follows and     |
|                                                                                              |
|    repeat steps 2 through 4 using the following values:                                      |
|                                                                                              |
|    - **Name**: app2, **Selected**: **/apps/app2\* **                                          |
|                                                                                              |
|    - **Name**: app3, **Selected**: **/apps/app3\* **                                          |
|                                                                                              |
|    - **Name**: base, **Selected**: **/**                                                     |
+----------------------------------------------------------------------------------------------+
| |image018|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 6. Review the **Applications Groups** dialogue window following completion of step 5 and     |
|                                                                                              |
| 7. Click the **Save & Next** button at the bottom of the dialogue window.                                                       |
+----------------------------------------------------------------------------------------------+
| |image019|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK 9: Contextual Access
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. Begin by selecting: **Local Traffic** -> **Virtual Servers**                              |
|                                                                                              |
| 2. Click the **Create** button (far right)                                                   |   
+----------------------------------------------------------------------------------------------+
| |image017|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 3. In the **New Virtual Server** window, key in the following as shown:                      |
|                                                                                              |
|    -  **Name**: **app.f5demo.com**                                                           |
|                                                                                              |
|    -  **Destination Address/Mask**: **10.1.10.100**                                          |
|                                                                                              |
|    -  **Service Port**: **443**                                                              |
|                                                                                              |
|    -  **HTTP Profile:** **http** (drop down)                                                 |
|                                                                                              |
|    -  **SSL Profile (client):** **app.f5demo.com-clientssl**                                 |
|                                                                                              |
|    -  **Source Address Translation:**  **Auto Map**                                          |
|                                                                                              |
| 4. Scroll to the **Access Policy** section                                                   |
|                                                                                              |
|    -  **Access Profile**: **app.f5demo.com-policy**                                          |
|                                                                                              |
|    -  **Per-Request Policy:** **saml\_policy**                                               |
|                                                                                              |
| 5. Scroll to the Resource section                                                            |
|                                                                                              |
|    -  **Default Pool**: **app.f5demo.com\_pool**                                             |
|                                                                                              |
| 6. Scroll to the bottom of the configuration window and click **Finished**                   |
|                                                                                              |
| *Note: The use of the Per-Request Policy is to provide header injection and other controls.* |
|                                                                                              |
| *These will be more utilized later in the lab.*                                              |
+----------------------------------------------------------------------------------------------+
| |image018|                                                                                   |
|                                                                                              |
| |image019|                                                                                   | 
+----------------------------------------------------------------------------------------------+

TASK 6: Test the SAML SP
~~~~~~~~~~~~~~~~~~~~~~~~

Refer to the instructions and screen shots below:

+----------------------------------------------------------------------------------------------+
| 1. Using your browser from the Jump Host click on the provided bookmark or navigate to       |
|                                                                                              |
|    https://app.f5demo.com . The SAML SP that you have just configured.                       |
+----------------------------------------------------------------------------------------------+
| |image020|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 2. Did you successfully redirect to the IdP?                                                 |
|                                                                                              |
| 3. Login to the iDP, were you successfully authenticated? (use credentials provided in the   |
|                                                                                              |
|    Authentication Information section at the beginning of this guide)                        |
|                                                                                              |
|    -  **Username**: **user**                                                                 |
|                                                                                              |
|    -  **Password**: **Agility1**                                                             |
|                                                                                              |
| 4. After successful authentication, were you returned to the SAML SP?                        |
|                                                                                              |
| 5. Were you successfully authenticated (SAML)?                                               |
|                                                                                              |
| 6. Review your **Active Sessions** (**Access Overview** -> **Active Sessions**)              |
|                                                                                              |
| 7. Review your Access Report Logs (**Access** -> **Overview Access Reports**)                |
+----------------------------------------------------------------------------------------------+
| |image021|                                                                                   |
+----------------------------------------------------------------------------------------------+

.. |image001| image:: media/lab1-001.png
   :width: 4.5in
   :height: 0.74in
.. |image002| image:: media/lab1-002.png
   :width: 4.5in
   :height: 3.37in
.. |image003| image:: media/lab1-003.png
   :width: 4.5in
   :height: 3.38in
.. |image004| image:: media/lab1-004.png
   :width: 4.5in
   :height: 0.73in
.. |image005| image:: media/lab1-005.png
   :width: 4.5in
   :height: 3.37in
.. |image006| image:: media/lab1-006.png
   :width: 4.5in
   :height: 1.15in
.. |image007| image:: media/lab1-007.png
   :width: 4.5in
   :height: 2.28in
.. |image008| image:: media/lab1-008.png
   :width: 4.5in
   :height: 0.96in
.. |image009| image:: media/lab1-009.png
   :width: 4.5in
   :height: 1.69in
.. |image010| image:: media/lab1-010.png
   :width: 4.5in
   :height: 2.94in
.. |image011| image:: media/lab1-011.png
   :width: 4.5in
   :height: 0.80in
.. |image012| image:: media/lab1-012.png
   :width: 4.5in
   :height: 1.12in
.. |image013| image:: media/lab1-013.png
   :width: 4.5in
   :height: 4.00in
.. |image014| image:: media/lab1-014.png
   :width: 4.5in
   :height: 1.48in
.. |image015| image:: media/lab1-015.png
   :width: 4.5in
   :height: 1.12in
.. |image016| image:: media/lab1-016.png
   :width: 4.5in
   :height: 1.54in
.. |image017| image:: media/lab1-017.png
   :width: 4.5in
   :height: 1.29in
.. |image018| image:: media/lab1-018.png
   :width: 4.5in
   :height: 5.46in
.. |image019| image:: media/lab1-019.png
   :width: 4.5in
   :height: 2.13in
.. |image020| image:: media/lab1-020.png
   :width: 4.5in
   :height: 1.01in
.. |image021| image:: media/lab1-021.png
   :width: 4.5in
   :height: 1.93in
.. |image022| image:: media/lab1-022.png
   :width: 4.5in
   :height: 3.37in
.. |image023| image:: media/lab1-023.png
   :width: 4.5in
   :height: 3.38in
.. |image024| image:: media/lab1-024.png
   :width: 4.5in
   :height: 0.73in
.. |image025| image:: media/lab1-025.png
   :width: 4.5in
   :height: 3.37in
.. |image026| image:: media/lab1-026.png
   :width: 4.5in
   :height: 1.15in
.. |image027| image:: media/lab1-027.png
   :width: 4.5in
   :height: 2.28in
.. |image028| image:: media/lab1-028.png
   :width: 4.5in
   :height: 0.96in
.. |image029| image:: media/lab1-029.png
   :width: 4.5in
   :height: 1.69in
.. |image030| image:: media/lab1-030.png
   :width: 4.5in
   :height: 2.94in
.. |image031| image:: media/lab1-031.png
   :width: 4.5in
   :height: 0.80in
.. |image032| image:: media/lab1-032.png
   :width: 4.5in
   :height: 1.12in
.. |image033| image:: media/lab1-033.png
   :width: 4.5in
   :height: 4.00in
.. |image034| image:: media/lab1-034.png
   :width: 4.5in
   :height: 1.48in
.. |image035| image:: media/lab1-035.png
   :width: 4.5in
   :height: 1.12in
.. |image036| image:: media/lab1-036.png
   :width: 4.5in
   :height: 1.54in
.. |image037| image:: media/lab1-037.png
   :width: 4.5in
   :height: 1.29in
.. |image038| image:: media/lab1-038.png
   :width: 4.5in
   :height: 5.46in
.. |image039| image:: media/lab1-039.png
   :width: 4.5in
   :height: 2.13in
.. |image040| image:: media/lab1-040.png
   :width: 4.5in
   :height: 1.01in
.. |image041| image:: media/lab1-041.png
   :width: 4.5in
   :height: 1.93in
.. |image041| image:: media/lab1-042.png
   :width: 4.5in
   :height: 1.93in
.. |image041| image:: media/lab1-043.png
   :width: 4.5in
   :height: 1.93in
.. |image041| image:: media/lab1-044.png
   :width: 4.5in
   :height: 1.93in
