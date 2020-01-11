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

TASK 2: Name Congiguration and define Device Posture  
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

+----------------------------------------------------------------------------------------------+
| 1. In the **Configuration Name** dialogie box, enter **agc-app.acme.com                      |
|                                                                                              |
| 2. Click **Save & Next" at the bottom of the dislogue window.                                |
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
| 3. Click the **Checkbox** next to the previously created **app.f5demo.com** and select       |                                                                                              |                                                                                              |
|    **Bind/Unbind IdP Connectors** button at the bottom of the GUI.                           | 
+----------------------------------------------------------------------------------------------+
| |image006|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 3. In the **Edit SAML IdP’s that use this SP** dialogue box click the **Add New Row** button |
|                                                                                              |
| 4. In the added row click the **Down Arrow** under **SAML IdP Connectors** and select the    |
|                                                                                              |
|    **/Common/idp.partner.com** SAML IdP Connector previously created.                        |
|                                                                                              |
| 5. Click the **Update** button and the **OK** button at the bottom of the dialogue box.      |
+----------------------------------------------------------------------------------------------+
| |image007|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 6. Under the **Access** -> **Federation** -> **SAML Service Provider** ->                    |
|                                                                                              |
|    **Local SP Services** menu you should now see the following (as shown):                   |
|                                                                                              |
|    -  **Name**: **app.f5demo.com**                                                           |
|                                                                                              |
|    -  **SAML IdP Connectors**: **idp.partner.com**                                           |
+----------------------------------------------------------------------------------------------+
| |image008|                                                                                   |
+----------------------------------------------------------------------------------------------+
 
TASK 4: Configure the SAML SP Access Policy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Refer to the instructions and screen shots below:

+----------------------------------------------------------------------------------------------+
| 1. Begin by selecting: **Access** -> **Profiles/Policies** -> **Access Profiles**            |
|    **(Per-Session Policies)**                                                                |
|                                                                                              |
| 2. Click the **Create** button (far right)                                                   |
+----------------------------------------------------------------------------------------------+
| |image009|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 3. In the **New Profile** window, key in the following as shown:                             |
|                                                                                              |
|    -  **Name**: **app.f5demo.com-policy**                                                    |
|                                                                                              |
|    -  **Profile Type**: **All** (from drop down)                                             |
|                                                                                              |
|    -  **Profile Scope**: **Profile** (default)                                               |
|                                                                                              |
| 4. Scroll to the bottom of the **New Profile** window to the **Language Settings**           |
|                                                                                              |
| 5. Select **English** from the **Factory Built-in Languages** menu on the right and click    |
|                                                                                              |
|    the **Double Arrow (<<)**, then click the **Finished** button.                            |
+----------------------------------------------------------------------------------------------+
| |image010|                                                                                   |
+----------------------------------------------------------------------------------------------+
 
+----------------------------------------------------------------------------------------------+
| 6. From the **Access** -> **Profiles/Policies** -> **Access Profiles**                       |
|    **(Per-Session Policies)**,                                                               |
|                                                                                              |
|    click the **Edit** link on the previously created **app.f5demo.com-policy** line.         |
+----------------------------------------------------------------------------------------------+
| |image011|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 7. In the **Visual Policy Editor** window for the **/Common/app.f5demo.com-policy**, click   |
|                                                                                              |
|    the **Plus (+) Sign** between **Start** and **Deny**.                                     |
|                                                                                              |
| 8. In the pop-up dialogue box select the **Authentication** tab and then click the **Radio** |
|                                                                                              | 
|    **Button** next to **SAML Auth**. Once selected click the **Add Item** button.            |
+----------------------------------------------------------------------------------------------+
| |image012|                                                                                   |
|                                                                                              |
| |image013|                                                                                   |
+----------------------------------------------------------------------------------------------+
  
+----------------------------------------------------------------------------------------------+
| 9. In the **SAML Auth** configuration window, select **/Common/app.f5demo.com** from the     |
|                                                                                              |
|    **SAML Authentication**, **AAA Server** drop down menu.                                   |
|                                                                                              | 
| 10. Click the **Save** button at the bottom of the configuration window.                     |  
+----------------------------------------------------------------------------------------------+
| |image014|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 11. In the **Visual Policy Editor** select the **Deny** along the **Successful** branch      |
|                                                                                              |
|    following the **SAML Auth**                                                               |
|                                                                                              |
| 12. From the **Select Ending** dialogue box select the **Allow Radio Button** and then       |
|                                                                                              |
|    click **Save**.                                                                           |
+----------------------------------------------------------------------------------------------+
| |image015|                                                                                   |
+----------------------------------------------------------------------------------------------+

+----------------------------------------------------------------------------------------------+
| 13. In the **Visual Policy Editor** click the **Apply Access Policy** (top left) and close   |
|                                                                                              |
|    the **Visual Policy Editor**.                                                             |
|                                                                                              |
| *Note: Additional actions can be taken in the Per Session policy (Access Policy). The lab*   |
|                                                                                              |
| *is simply completing authentication. Other access controls can be implemented based on the* |
|                                                                                              |
| *use case*                                                                                   |
+----------------------------------------------------------------------------------------------+
| |image016|                                                                                   |
+----------------------------------------------------------------------------------------------+

TASK 5: Create the SP Virtual Server & Apply the SP Access Policy
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Refer to the instructions and screen shots below:

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

.. |image001| image:: media/lab1-001.PNG
   :width: 4.5in
   :height: 0.74in
.. |image002| image:: media/lab1-002.PNG
   :width: 4.5in
   :height: 3.37in
.. |image003| image:: media/lab1-003.PNG
   :width: 4.5in
   :height: 3.38in
.. |image004| image:: media/lab1-004.PNG
   :width: 4.5in
   :height: 0.73in
.. |image005| image:: media/lab1-005.PNG
   :width: 4.5in
   :height: 3.37in
.. |image006| image:: media/lab1-006.PNG
   :width: 4.5in
   :height: 1.15in
.. |image007| image:: media/lab1-007.PNG
   :width: 4.5in
   :height: 2.28in
.. |image008| image:: media/lab1-008.PNG
   :width: 4.5in
   :height: 0.96in
.. |image009| image:: media/lab1-009.PNG
   :width: 4.5in
   :height: 1.69in
.. |image010| image:: media/lab1-010.PNG
   :width: 4.5in
   :height: 2.94in
.. |image011| image:: media/lab1-011.PNG
   :width: 4.5in
   :height: 0.80in
.. |image012| image:: media/lab1-012.PNG
   :width: 4.5in
   :height: 1.12in
.. |image013| image:: media/lab1-013.PNG
   :width: 4.5in
   :height: 4.00in
.. |image014| image:: media/lab1-014.PNG
   :width: 4.5in
   :height: 1.48in
.. |image015| image:: media/lab1-015.PNG
   :width: 4.5in
   :height: 1.12in
.. |image016| image:: media/lab1-016.PNG
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
.. |image002| image:: media/lab1-022.PNG
   :width: 4.5in
   :height: 3.37in
.. |image003| image:: media/lab1-023.PNG
   :width: 4.5in
   :height: 3.38in
.. |image004| image:: media/lab1-024.PNG
   :width: 4.5in
   :height: 0.73in
.. |image005| image:: media/lab1-025.PNG
   :width: 4.5in
   :height: 3.37in
.. |image006| image:: media/lab1-026.PNG
   :width: 4.5in
   :height: 1.15in
.. |image007| image:: media/lab1-027.PNG
   :width: 4.5in
   :height: 2.28in
.. |image008| image:: media/lab1-028.PNG
   :width: 4.5in
   :height: 0.96in
.. |image009| image:: media/lab1-029.PNG
   :width: 4.5in
   :height: 1.69in
.. |image010| image:: media/lab1-030.PNG
   :width: 4.5in
   :height: 2.94in
.. |image011| image:: media/lab1-031.PNG
   :width: 4.5in
   :height: 0.80in
.. |image012| image:: media/lab1-032.PNG
   :width: 4.5in
   :height: 1.12in
.. |image013| image:: media/lab1-033.PNG
   :width: 4.5in
   :height: 4.00in
.. |image014| image:: media/lab1-034.PNG
   :width: 4.5in
   :height: 1.48in
.. |image015| image:: media/lab1-035.PNG
   :width: 4.5in
   :height: 1.12in
.. |image016| image:: media/lab1-036.PNG
   :width: 4.5in
   :height: 1.54in
.. |image017| image:: media/lab1-037.png
   :width: 4.5in
   :height: 1.29in
.. |image018| image:: media/lab1-038.png
   :width: 4.5in
   :height: 5.46in
.. |image019| image:: media/lab1-039.png
   :width: 4.5in
   :height: 2.13in
.. |image020| image:: media/lab1-040.png
   :width: 4.5in
   :height: 1.01in
.. |image021| image:: media/lab1-041.png
   :width: 4.5in
   :height: 1.93in
