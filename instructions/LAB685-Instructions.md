# LAB685 - Deploy Copilot with confidence: Find & protect exposed sensitive data

In this lab, you will classify financial information, configure data loss prevention for Copilot and AI websites, and connect endpoint protection to insider risk. Use only the fictional sample data described in the exercises.

## Lab sign-in

Use the browser inside your lab virtual machine and the assigned tenant accounts below. Do not use a personal or production account. Select the administrator account for administration tasks and the Alex Wilber account where an exercise requests it.

| Account | Assigned sign-in |
| --- | --- |
| Administrator username | +++@lab.CloudCredential(WWLM365E7).AdministrativeUsername+++ |
| Administrator password | +++@lab.CloudCredential(WWLM365E7).AdministrativePassword+++ |
| Alex Wilber username | +++AlexW@@lab.CloudCredential(WWLM365E7).TenantName+++ |
| Alex Wilber password | +++@lab.CloudCredential(WWLM365E7).UserPassword+++ |
| Temporary Access Pass, when requested | +++@lab.CloudCredential(WWLM365E7).AlexWTAP+++ |

Keep credentials inside the lab. Do not include passwords or access passes in screenshots, notes or messages. Open the Microsoft Purview portal at https://purview.microsoft.com to begin.

## Exercises

1. Information Protection: labels, publishing, auto-labeling and a sample document.
2. Data Loss Prevention: Copilot restrictions, endpoint policy and alerts.
3. Insider Risk Management: AI risk detection.
4. Agent 365: Analyst interaction, Copilot activity and agent usage review.

Policy synchronization, analytics and risk processing can outlast the session. Follow each exercise's completion criteria; do not treat a configured policy as proof that a live block occurred.

> [+]Environment
> 
> | Item | Detail |
> | :--- | :----- |
> | **Description** | Windows 11 Desktop with Edge |
> | **Operating System** | Windows 11 Desktop |
> | **Software/Configuration** | Microsoft MS Edge in Windows Kiosk Mode |
> | **Platform/Fabric** | Hyper-V Virtual Machine |
> | **Hardware** | 2 CPU, 4GB Memory |
> | **Networking** | Internet access provided |
> |  |  |

>[+] End User Licensing Agreement
>
> <Center>
> ![Skillable Logo](instructions359483/LAB685-Skillable-License-Logo.png)
> </Center>
> 
> **TERMS OF USE**
> 
> Last Updated and Effective as of: June 24, 2024 **Effective Date**
> 
> Hands-On Learning Solutions LLC *d.b.a.* Skillable ("**Skillable**") grants you the right to access and use the Skillable produced templates located within the Skillable Studio ("**Skillable Template**") to enable you to build custom labs for your authorized end users ("**End Users**") on Skillable's cloud based enterprise learning platform that delivers hands-on learning experiences that help you and End Users to develop and validate technical and digital skills ("**Platform**") subject to your compliance with these Terms of Use ("**ToU**"), which are subject to and governed by your MSA (as defined below). If there is a conflict between these ToU and the MSA, the terms and conditions of these ToU will control.
> 
> **IMPORTANT**. PLEASE READ THESE TOU BEFORE ACCESSING OR USING THE SKILLABLE TEMPLATES. YOU ACKNOWLEDGE AND AGREE THAT, BY ACCESSING OR USING THE SKILLABLE TEMPLATES , YOU (a) HAVE READ, UNDERSTAND AND AGREE TO BE BOUND BY ALL OF THE TERMS AND CONDITIONS HEREIN, AND (b) AGREE TO COMPLY WITH ALL APPLICABLE LAWS, RULES, REGULATIONS, TREATIES, DIRECTIVES, AND ORDINANCES ASSOCIATED WITH YOUR USE OF THE SKILLABE TEMPLATES (COLLECTIVELY, "**APPLICABLE LAWS**"). IF YOU DO NOT AGREE TO ALL OF THE TERMS AND CONDITIONS HEREIN, YOU ARE NOT PERMITTED AND ARE NOT AUTHORIZED TO ACCESS OR USE THE SKILLABLE TEMPLATES. You may use the Skillable Templates only if you have reached the age of majority in your jurisdiction, and can enter into a binding agreement with Skillable. If you accept or agree to these ToU on behalf of a company ("**Representative**"), you represent and warrant that you have the authority to enter that company into and bind such company to these ToU. The terms "**you**" and "**your**" as used herein refer to, as applicable, the individual accepting these ToU on your own behalf, or the company that Representative is entering into these ToU.
> 
> 1.  **License to the Skillable** **Templates**. Subject to your compliance with these ToU and the terms of your Skillable Master Services Agreement or other agreement entered into with Skillable to access and use the Platform ("**MSA**"), Skillable grants, and you accept a limited, nonexclusive, nontransferable right to access, clone, and use the Skillable Templates located at https://labondemand.com/ to help you create custom labs during the term of the MSA solely for use on the Platform and your internal training purposes. A Skillable Template includes a software environment that has been designed to work correctly on the Platform, and may include one or more additional software products installed and configured therein as set forth in the Skillable Template documentation. A Skillable Template may be optimized for use on the Platform, which may alter the normal default behavior of the installed software products.
> 2.  **Proprietary Rights**. The Skillable Templates, including all software and other content contained therein are protected under Applicable Laws, including United States and international copyright, trademark, patent, trade secret, and other intellectual property laws. All Skillable Templates are the sole and exclusive property of Skillable and/or its licensors. The Skillable Templates, including the compilation (meaning the selection, collection, arrangement, and assembly) of all software and other content contained in the Skillable Templates, is the sole and exclusive property of Skillable and/or its licensors. Unauthorized copying or use of the Skillable Templates (including use on any other website, platform, or application) violates Applicable Laws. No license or rights are granted to you with respect to the Skillable Templates except as expressly set forth herein, and all implied licenses and rights are reserved by Skillable and/or its licensors.
> 3.  **Responsibility for Usage of Skillable Templates**. You are solely responsible for and acknowledge and agree that you and each End User have their own licensed copy of the applicable software associated with and/or included in the Skillable Templates you use ("**Underlying Software**"). Additionally, you are solely responsible and liable for compliance by End Users with each end user license agreement ("**EULA**") for the Underlying Software, the maintenance, security, performance, and functionality of the Skillable Templates you use, including the Underlying Software, and the acts and/or omissions of End Users in connection with access to and use of the custom labs created utilizing the Skillable Templates.
> 4.  **Restrictions on Use**. You may not: (a) reverse engineer, decompile, or otherwise attempt to discover the source code or underlying ideas or any algorithms of the Skillable Templates; (b) modify, translate or create derivative works based on the Skillable Templates except to create the custom labs subject to these ToU and the MSA; (c) rent, lease, distribute, license, sublicense, sell, or resell the Skillable Templates; (d) make the Skillable Templates available to any third party not specifically authorized herein; (e) violate any Applicable Law in connection with your use of, or any act and/or omission in connection with, the Skillable Templates; (f) remove or destroy any proprietary markings, notices, confidential legends or any trademarks or trade names of Skillable and/or its licensors placed upon or contained within the Skillable Templates; (g) access the Skillable Templates in order to (i) build a competitive product or service, or (ii) copy any features, functions, designs, or graphics of the Skillable Templates; (h) access or use the Skillable Templates if you are (1) identified on any applicable sanctions-related list of designated persons, which include those maintained by the United States, member countries of the European Economic Area, including the European Union, the United Kingdom, Switzerland, and the United Nations Security Council, such as the U.S. Department of the Treasury's Office of Foreign Assets Control's list of Specially Designated Nationals and Blocked Persons List, the European Union's Consolidated List of Persons, Groups, and Entities Subject to European Union Financial Sanctions, and the United Kingdom's HM Treasury's Consolidated List of Sanctions Targets, and/or (2) located in a country or territory that is the target of comprehensive Sanctions; (i) interfere with or disrupt the integrity or performance of the Skillable Templates or any software, content, or data contained therein, or attempt to gain unauthorized access to the Skillable Templates, or Skillable systems or networks; or (j) in connection with use of the Skillable Templates store or transmit (1) infringing, libelous, or otherwise unlawful, or tortious material, (2) material in violation of third-party privacy rights, (3) malicious code, or (4) information for any End User that is a minor as defined under Applicable Law.
> 5.  **Fees**. There are no additional fees to access and/or use the Skillable Templates except the lab developer license fees set forth in your MSA.
> 6.  **Indemnity**. You will indemnify, defend and hold harmless Skillable and its subsidiaries, affiliates, and its and their partners, officers, directors, shareholders, managers, members, employees, consultants, and agents (collectively, "**Skillable Indemnitees**") from all claims, whether actual or alleged (collectively, "**Claims**"), that arise out of or in connection with (a) your breach of these ToU, (b) your (i) access and/or use of the Skillable Templates and/or Underlying Software, and/or (ii) violation of Applicable Law and/or the rights of any third party, and/or (c) any content, information, or data you submit, post, transmit, modify or otherwise make available through or in connection with the Skillable Templates and/or Underlying Software. You are solely responsible for defending all Claims against each Skillable Indemnitee, subject to such Skillable Indemnitee's right to participate with counsel of its own choosing, at its own expense, and for payment of all judgments, settlements, damages, losses, liabilities, costs, and expenses, including reasonable attorneys' fees, resulting from all Claims against each Skillable Indemnitee, provided that you will not agree to any settlement that imposes any obligation or liability on any Skillable Indemnitee without its prior express written consent.
> 7.  **Disclaimer of Warranties**. TO THE MAXIMUM EXTENT PERMITTED BY APPLICABLE LAW, THE SKILLABLE TEMPLATES ARE PROVIDED ON AN "AS IS" BASIS WITHOUT REPRESENTATION, WARRANTY, CONDITION, OR GUARANTEE OF ANY KIND, AND SKILLABLE DISCLAIMS ANY AND ALL REPRESENTATIONS, WARRANTIES AND CONDITIONS, WHETHER EXPRESS OR IMPLIED, INCLUDING IMPLIED REPRESENTATIONS, WARRANTIES, CONDITIONS, AND/OR GUARANTEES, AND ANY WARRANTIES OF MERCHANTABILITY, SATISFACTORY QUALITY, TITLE, NONINFRINGEMENT, OR FITNESS FOR A PARTICULAR PURPOSE. Some states do not allow the exclusion of implied or express warranties, so the above disclaimers may not apply to you.
> 8.  **Limitation of Liability**. TO THE MAXIMUM EXTENT PERMITTED BY APPLICABLE LAW, AND IN ADDITION TO ANY OTHER LIMITATION IN THESE TOU, NEITHER SKILLABLE NOR ITS SUBSIDIARTIES OR AFFILIATES ARE LIABLE FOR ANY INDIRECT, INCIDENTAL, SPECIAL, CONSEQUENTIAL OR EXEMPLARY DAMAGES, INCLUDING DAMAGES FOR LOST PROFITS, LOST REVENUE, GOODWILL, LOSS OF DATA, OR OTHER INTANGIBLE LOSSES ARISING OUT OF, OR IN CONNECTION WITH YOUR ACCESS AND/OR USE OF THE SKILLABLE TEMPLATES AND UNDERLYING SOFTWARE, EVEN IF SKILLABLE AND/OR ITS SUBSIDIARIES AND/OR AFFILIATES HAVE BEEN ADVISED OF THE POSSIBILITY OF SUCH DAMAGES. NOTWITHSTANDING THE FAILURE OF THE ESSENTIAL PURPOSE OF ANY REMEDY PROVIDED HEREIN, THE MAXIMUM LIABILITY OF SKILLABLE AND ITS SUBSIDIARIES AND AFFILIATES, UNDER ANY CAUSE OF ACTION OR THEORY, IS \$500.
> 9.  **Term; Termination; Suspension; Survival**. You may continue to access and use the Skillable Templates during the term of your MSA. Notwithstanding anything to the contrary in these ToU or the MSA, Skillable may immediately suspend, impose restrictions, or terminate your access to and use of the Skillable Templates at any time without written notice if Skillable: (a) determines that your use of the Skillable Templates causes or may cause harm or liability, whether legal, financial, reputational or otherwise, to other Skillable Template users, a third party, or Skillable or its subsidiaries and/or affiliates; (b) is legally obligated to do so; (c) is required to do so in connection with a technical and/or security issue; or (d) determines that you are in breach of these ToU and/or MSA and fail to cure such breach within seven (7) days of receiving written notice (email acceptable). Skillable will have no liability to you, any End User, or any third party for any termination of these ToU, or limiting access to the Skillable Templates. You will not be entitled to receive a refund of any lab developer license fees paid, in whole or part, if these ToU are terminated. The provisions of these ToU which are expressly or impliedly intended to survive the termination or expiration of the term of your MSA will survive such termination or expiration, including Sections 2 through 13.
> 10. **Assignment**. These ToU and any rights or obligations hereunder, including your access to and use of the Skillable Templates may not be assigned, sublicensed or otherwise transferred by you, whether by a change of control or by operation of law, without the prior written consent of Skillable, which will not be unreasonably withheld. Any assignment, attempted assignment, or transfer in violation of this Section will be void and of no force or effect. Skillable and its subsequent assignees may assign, delegate, sublicense, or otherwise transfer from time-to-time these ToU, or the rights or obligations hereunder, in whole or in part, to any person or entity.
> 11. **Enforceability of These ToU**. If any provision of these ToU is found by a court of competent jurisdiction to be invalid or unenforceable, or is otherwise invalid or enforceable, you and Skillable agree that the court, or you and Skillable, as applicable, should endeavor to give effect to you and Skillable's intentions as reflected in the provision, and if not given effect, will be deemed severable from these ToU and will not affect the validity and enforceability of any remaining provisions of these ToU, which remain in full force and effect.
> 12. **Miscellaneous**. These ToU may be amended from time-to-time in Skillable's sole discretion. Any changes to these ToU will be effective immediately upon the posting of the revised ToU on the Skillable Studio, or Skillable's website or application. These ToU, including any agreements and terms incorporated by reference herein, constitutes the entire agreement between the parties, and govern your use of the Skillable Templates, and supersedes any prior and/or contemporaneous written and/or oral agreements, discussions, communications, or representations between the parties relating to the Skillable Templates (including any additional, different, or conflicting terms on any of your forms, emails, purchase orders, or papers). Any suggestions, comments, improvements, ideas, enhancement requests or feedback provided by you and/or End Users with respect to or relating to the Skillable Templates, may be used by Skillable without compensation or attribution to you or End Users, and in connection therewith, you and/or End Users, as applicable, grant Skillable a perpetual, irrevocable, fully paid-up, unrestricted right and license to use any or all of the foregoing. Skillable retains all rights, title, and interests in the Skillable Templates, together with all derivative works, modifications, enhancements, and upgrades thereto, specifically excluding the custom labs you create with such Skillable Templates. Only a written instrument specifically waiving compliance that is executed by whichever party is entitled to waive such compliance may waive any term and/or condition of these ToU. No waiver by either party of any provision hereof will be deemed a waiver of any other breach of such provision or a waiver of the provision. Except for your lab developer license fees, neither party will have any liability under these ToU by reason of any failure or delay in the performance of the applicable party's obligations on account of strikes, shortages, riots, acts of terrorism, insurrection, fires, flood, storm, explosions, earthquakes, Internet, network and/or electrical outages, computer viruses, cyber-attacks, pandemics (including COVID-19), endemics, acts of God, war, governmental action, malicious acts of a third party, or any cause that is beyond the applicable party's reasonable control. The parties are independent contractors and nothing in these ToU will be construed to create, evidence, or imply any agency, employment, partnership, or joint venture between the parties. Except as expressly set forth herein, these ToU are not intended to benefit, nor will it be deemed to give rise to any rights in, any third party. Notwithstanding the foregoing, you acknowledge and agree that the Skillable Indemnitees and licensors are third-party beneficiaries to these ToU, and will be entitled to directly enforce, and rely upon, any provision herein which confers a benefit on, or rights in favor of, them. The headings in these ToU are for convenience only and have no legal or contractual effect. As used in these ToU, the words "**herein**" or "**hereof**" mean these ToU, "**including**" is a term of enlargement meaning "including without limitation" and does not denote exclusivity, and the words "**will**", "**shall**", and "**must**" are deemed to be equivalent and denote a mandatory obligation or prohibition, as applicable. All definitions herein apply both to their singular and plural forms, as the context may require.
> 13. **Electronic Signatures Effective**. By clicking on the "I Agree" box or a similarly named box, or otherwise expressly agreed to in these ToU, you create an electronic signature to these ToU, establishing a valid and binding agreement between the parties. Therefore, you agree to accept these ToU, and any other agreement contained or referenced herein. In addition, you agree that we may supply you a copy of these ToU in electronic form. Please print or save a copy of these ToU for your records. You also may choose to receive a copy of the ToU in non-electronic form at any time by sending a letter and self-addressed, stamped envelope to us at: Hands-On Learning Solutions LLC *d.b.a.* Skillable, located at 7143 State Road 54, \#153, New Port Richey, FL 34653.
> 
>     You may choose to withdraw your consent to receive these ToU in electronic form. Withdrawing your consent to receive the ToU in electronic form does not change your existing obligations to Skillable under the ToU. Instead, withdrawing your consent means that you wish to have your relationship with Skillable governed by a non-electronic form of these ToU. If you wish to withdraw your consent to receive these ToU in electronic form and to instead enter into a non-electronic form of the ToU, please send a letter and self-addressed, stamped envelope to us at: Hands-On Learning Solutions LLC *d.b.a.* Skillable, located at 7143 State Road 54, \#153, New Port Richey, FL 34653. Skillable then will send you a non-electronic form of the ToU. Your withdrawal of consent will become effective when Skillable mails you a copy of the non-electronic form of the ToU, at which point your relationship with Skillable will be governed by the terms of such ToU. In either instance, the obligations that you incur pursuant to the electronic form of these ToU, prior to the effective date of the withdrawal of your consent, will remain unchanged until they are fully satisfied by you.
> 
>     In order to access and retain the electronic ToU, you must have access to the Internet, either directly or through devices that access web-based and/or mobile content, and pay any charges associated with such access. In addition, you must use all equipment necessary to make such connection to the Internet (e.g., a computer, mobile phone, or other access device). Skillable will use commercially reasonable efforts to notify you of any material changes in the hardware or software requirements needed to access and/or retain these ToU that create a material risk that you will not be able to continue to access and/or retain the electronic ToU.

===

# Lab - Manage sensitive data using Microsoft Purview Information Protection in the age of AI

Alex Wilber, Contoso's Information Security Administrator, needs employees to recognize sensitive financial information as they work with Microsoft 365 Copilot. You'll help Alex create and publish a sensitivity label, configure automatic detection of credit card numbers, and label a sample document. This classification work sets up the DLP controls you'll configure in the next section.

> [!NOTE]
> Copilot respects users' existing access permissions. The Financial data label you'll create adds classification and a footer, not encryption or a Copilot restriction.

**Tasks**:

1. Create a label group and a financial data label
1. Publish sensitivity labels
1. Configure auto-apply labeling
1. Apply the Confidential/All Employees label to a document

## Task 1 - Create a label group and a financial data label

Create an Internal label group and a Financial data label. The label's footer will help employees recognize sensitive financial content intended for internal use.

1. In the **Microsoft Purview portal**, navigate to **Solutions** > **Information Protection**.

1. On the **Information Protection** page, select **Sensitivity labels** from the left navigation.

1. On the **Sensitivity labels** page, select **+ Create** > **Label group**.

1. On the **Provide basic details for this label group** page, enter:

   - **Name**: `Internal`
   - **Display name**: `Internal`
   - **Description for users**: `Use this label for internal Contoso content.`
   - **Description for admins**: `Label group for internal Contoso content, including financial data.`

1. Select **Next**.

1. On the **Review your settings and finish** page, select **Create label group**.

1. On the **Your label group was created successfully** page, select **Create a label in this group**, then select **Done**.

1. On the **Provide basic details for this label** page enter:

   - **Name**: `Financial data`
   - **Display name**: `Financial data`
   - **Description for users**: `Use this label for documents and emails that contain sensitive financial information, such as credit card numbers.`
   - **Description for admins**: `Classifies sensitive financial content with a visible footer and supports auto-labeling and label-based DLP policies.`

1. Select **Next**.

1. On the **Define the scope for this label** page, select **Files & other data assets** and **Emails**. Make sure **Meetings** is deselected, then select **Next**.

1. On the **Choose protection settings for labeled items** page, select **Apply content marking**, then select **Next**.

1. On the **Content marking** page, enable **Content marking**.

1. Select the checkbox for **Add a footer**, then select **Customize text**.

1. In the **Customize footer text** flyout, enter:

   - **Footer text**: `Contoso Financial Data - Internal Use Only`
   - **Font size**: `10`
   - **Font color**: Black
   - **Align text**: Left
   - Select **Save**.

1. Back on the **Content marking** page, select **Next**.

1. Keep the default settings on the remaining pages by selecting **Next** until you reach the **Review your settings and finish** page.

1. Select **Create label**.

1. On the **Your sensitivity label was created** page, select **Don't create a policy yet**, then select **Done**.

Your Financial data label is ready. Next, publish it so employees can apply it to their content.

## Task 2 - Publish sensitivity labels

Publish the Financial data label to make it available to users. You'll also select it in the auto-labeling policy in the next task.

1. In the Microsoft Purview portal, under **Information Protection**, expand **Policies** then select **Label publishing policies**.

1. On the **Label policies** page, select **Publish labels**.

1. On the **Choose sensitivity labels to publish** page, select **Choose sensitivity labels to publish**.

1. On the **Sensitivity labels to publish** flyout, select the checkbox for:

   - **Internal/Financial data**
   - Select **Add**

1. Back on the **Choose sensitivity labels to publish** page, select **Next** through the remaining pages until you reach the **Name your policy** page.

1. On the **Name your policy** page, enter:

   - **Name**: `Internal financial data`
   - **Description**: `Makes the Financial data label in the Internal label group available for users to apply to documents and emails.`

1. Select **Next**, then on the **Review and finish** page, select **Submit**.

1. On the **New policy created** page, select **Done**.

You've published Internal/Financial data. Next, configure a policy to apply it when credit card numbers are detected.

## Task 3 - Configure auto-apply labeling

Configure an auto-labeling policy using the built-in Credit card number sensitive information type (SIT). Start in simulation mode to evaluate matches before applying the Financial data label.

> [!NOTE]
> This rule detects credit card numbers, not all financial information. Simulation evaluates matches without applying labels. The policy is set to activate after seven days if it isn't modified.

1. In the Microsoft Purview portal, under **Information Protection**, expand **Policies** then select **Auto-labeling policies**.

1. On the **Auto-labeling policies** page, select **+ Create auto-labeling policy**.

1. On the **What type of auto-labeling policy do you want to create?** page, select **Automatically apply labels only**.

1. On the **Choose info you want this label applied to** page, select **Custom** as the category, then select **Custom policy** under regulations.

1. Select **Next**.

1. On the **Name your auto-labeling policy** page, enter:

   - **Name**: `Auto-apply financial data`
   - **Description**: `Automatically applies the Financial data sensitivity label when credit card numbers are detected.`

1. Select **Next**.

1. On the **Choose a label to auto-apply** page, select **+ Choose a label**.

1. On the **Choose a sensitivity label** flyout, select the checkbox for **Internal/Financial data**, then select **Add**.

1. Back on the **Choose a label to auto-apply** page, select **Next**.

1. On the **Assign admin units** page, select **Next**.

1. On the **Choose locations where you want to apply the label** page, select:

   - **Exchange email**
   - **SharePoint sites**
   - **OneDrive accounts**

1. Select **Next**.

1. On the **Set up common or advanced rules** page, select **Common rules**, then select **Next**.

1. On the **Define rules for content in all locations** page, select **+ New rule**.

1. In the **New rule** flyout, enter:

   - **Name**: `Credit card number rule`
   - **Description**: `Detects credit card numbers using the built-in Credit card number sensitive information type.`

1. Under **Conditions**, select **+ Add condition** > **Content contains**.

1. Under the **Content contains** section, select **+ Add** > **Sensitive info types**.

1. In the **Sensitive info types** list, search for and select `Credit card number`, then select **Add**.

1. Select **Save** to finish creating the rule.

1. Select **Next**.

1. On the **Additional label settings for email** page, select **Next**.

1. On the **Decide if you want to test out the policy now or later** page, select **Run policy in simulation mode**, and select the checkbox for **Automatically turn on policy if not modified after 7 days in simulation**.

1. Select **Next**.

1. On the **Review and finish** page, select **Create policy**.

1. On the confirmation page, select **Done**.

Your auto-labeling policy is configured in simulation mode. Next, apply a label manually to content that doesn't contain credit card numbers.

## Task 4 - Apply the Confidential/All Employees label to a document

Create a fictional budget summary in Word for the web and apply Confidential/All Employees. This gives you a labeled document for the next section's Copilot DLP policy.

> [!NOTE]
> New labels can take time to synchronize across Word and DLP. Use the preconfigured Confidential/All Employees label for this document and the following DLP exercise, even if Financial data is available.

> [!NOTE]
> If Sensitivity is unavailable, check your lab account and SharePoint/OneDrive labeling support. If Confidential/All Employees is missing, contact your instructor rather than selecting another label.

1. In the **Microsoft Purview portal**, select the **Microsoft 365 app launcher** (the nine-dot icon in the upper-left corner).

1. Select **Word**. If Word isn't listed, select **More apps**, then select **Word**.

1. In **Word for the web**, confirm that you're signed in with the lab account provided for **Alex Wilber**, then create a **Blank document**.

1. Select the document name at the top of the page and rename it to `Contoso financial planning summary`. The document is saved automatically to your lab account's OneDrive.

1. Enter the following fictional content:

    ```text
    Contoso financial planning summary
    Fictional information for training purposes only.

    Proposed quarterly budget: $125,000
    Forecast operating expenses: $98,000

    This draft contains internal financial planning information.
    Review and approve the figures before distributing the summary.
    ```

   Don't enter real payment details or other sensitive information. This document doesn't need credit card numbers because you'll apply the label manually.

1. On the **Ribbon** tab, click on the shield icon and select the right label **Confidential** > **All Employees**.

!IMAGE[3cwph4op.png](instructions359483/3cwph4op.png)

7. Notice the locker on the icon and confirm from the Sensitivity menu in the bar that Word for the web displays **Confidential/All Employees** as the document's sensitivity label. If only **All Employees** is displayed, open the **Sensitivity** menu and confirm that the selected label is under **Confidential**, not **General** or **Highly Confidential**.
!IMAGE[3pwprcyi.png](instructions359483/3pwprcyi.png) !IMAGE[0yev7oeu.png](instructions359483/0yev7oeu.png)

1. Wait until Word indicates that your changes are saved.

> [!TIP]
> Optional: If Internal/Financial data is available, try it on a separate document and check for the footer `Contoso Financial Data - Internal Use Only`. Keep Confidential/All Employees on your main sample document for the DLP exercise.

Your budget summary is labeled. Because its figures don't match the credit card number rule, this demonstrates where manual classification complements automatic detection.

## Section complete

You've created and published Financial data, configured auto-labeling in simulation, and manually applied Confidential/All Employees to a sample document. Alex now has a classification foundation for the next layer of controls.

Continue to data loss prevention to configure Copilot restrictions and controls for external AI websites.

===

# Lab - Prevent data exposure in Copilot and AI apps with Data Loss Prevention

Alex now needs controls for how sensitive content is used with AI. You'll enable a label-based Copilot restriction and prepare an endpoint DLP policy for banking information sent to AI websites. Keep the endpoint policy in simulation to evaluate matches without enforcing its blocking actions.

**Tasks**:

1. Create a DLP policy for Copilot
1. Create an endpoint DLP policy
1. Configure DLP alert settings
1. Configure DLP alert aggregation

## Task 1 - Create a DLP policy for Copilot

Create and enable a policy that restricts Copilot from processing content labeled Confidential/All Employees. Keep the default scope of all users and groups.

> [!NOTE]
> Select Confidential/All Employees, the label on your sample document. The policy will target all content with this label, not just that document.

You'll enable the policy directly for this lab exercise. In production, start in simulation mode and review policy matches before enabling enforcement.

1. Return to the **Microsoft Purview portal** browser tab. From the left sidebar, select **Solutions** > **Data Loss Prevention** > **Policies**.

1. On the **Policies** page, select **+ Create policy** .

1. On the **What info do you want to protect** page, select **Enterprise applications & devices**.

1. On the **Start with a template or create a custom policy** page, select **Custom** as the category, then select **Custom policy** under **Regulations**.

1. Select **Next**.

1. On the **Name your DLP policy** page, enter:

   - **Name**: `Copilot restrict confidential content`
   - **Description**: `Restricts Copilot from processing content labeled Confidential/All Employees.`

1. Select **Next**.

1. On the **Assign admin units** page select **Next**.

1. On the **Choose where to apply the policy** page, select the location for **Microsoft Copilot, Copilot Chat, and Copilot Cowork** only. If any other locations are selected, deselect them, then select **Next**.

1. On the **Define policy settings** page, leave the default **Create or customize advanced DLP rules** selected, then select **Next**.

1. On the **Customize advanced DLP rules** page, select **+ Create rule**.

1. In the **Create rule** flyout, in the **Name** field, enter `Restrict Copilot confidential content`.

1. Under **Conditions**, select **+ Add condition** > **Content contains**.

1. In the **Content contains** section, select **Add** > **Sensitivity labels**.

!IMAGE[414zmjzw.png](instructions359483/414zmjzw.png)

15. In the **Sensitivity labels** flyout, select the checkbox for **All Employees** with the label path **Confidential/All Employees**, then select **Add** at the bottom of the flyout.

1. Back on the **Create rule** flyout, under **Actions** select **+ Add an action** > **Restrict Copilot from processing content**.

1. Under **Restrict Copilot from processing content**, select **Accessing knowledge sources**. Ensure the dropdown is set to **Block**.

1. Select **Save** at the bottom of the **Create rule** flyout.

1. Back on the **Customize advanced DLP rules** page, select **Next**

1. On the **Policy mode** page select **Turn the policy on immediately**, then select **Next**.

1. On the **Review and finish** page, verify the settings, then select **Submit**.

1. On the **New policy created** page select **Done**.

Your Copilot policy is enabled for content labeled Confidential/All Employees. Next, configure a different control for banking information sent to AI websites.

> [!NOTE]
> Copilot policy changes can take up to four hours to take effect. Verify the policy configuration to complete this task; a live blocking demonstration isn't required.

## Task 2 - Create an endpoint DLP policy

The Copilot policy checks a document's label. Next, prepare an endpoint policy that detects banking information directly. Configure blocking actions for AI websites, but leave the policy in simulation for this exercise.

> [!NOTE]
> Endpoint enforcement requires supported, onboarded devices and browsers. Creating this policy doesn't onboard devices.

1. On the **Policies** page of the **Data Loss Prevention** solution of the Microsoft Purview portal, select **+ Create policy**.

1. On the **What info do you want to protect** page, select **Enterprise applications & devices**.

1. On the **Start with a template or create a custom policy** page, select **Custom** and **Custom policy**, then select **Next**.

1. On the **Name your DLP policy** page, enter:

    - **Name**: `Block AI website uploads of banking data`
    - **Description**: `Protects banking information from being uploaded or pasted to AI websites.`

1. Select **Next**.

1. On the **Assign admin units** page, select **Next**.

1. On the **Choose where to apply the policy** page, ensure only the **Devices** location is selected. If any other location is selected, ensure they're deselected, then select **Next**.

1. On the **Define policy settings** page, select **Create or customize advanced DLP rules** then select **Next**.

1. On the **Customize advanced DLP rules** page, select **+ Create rule**.

1. In the **Create rule** flyout, in the **Name** field, enter `Block banking data exposure to AI websites`.

1. Under **Conditions** select **+ Add condition** then select **Content contains**.

1. In the new **Content contains** section:

    - Select **Add** > **Sensitive info types**.
    - In the **Sensitive info types** flyout, search for these sensitive info types:
       - `Credit Card Number`
       - `ABA Routing Number`
       - `SWIFT Code`
       - `International Banking Account Number (IBAN)`
    - Select **Add** at the bottom of the flyout

1. Under **Actions**, select **+ Add an action** > **Audit or restrict activities on devices**.

1. In the **Service domain and browser activities** section:

   1. Select the checkbox for **Manage protected files access from unallowed browsers and uploads to restricted cloud service domains**.

   1. Next to this option, select **+ Choose different restrictions for sensitive service domains**.

   1. In the **Sensitive service domain restrictions** flyout:

      - Select **+ Add group**.
      - In the **Choose sensitive service domain groups** flyout, select the checkbox for **Generative AI Websites**, then select **Add**.
      - Back on the **Sensitive service domain restrictions** flyout, change the action in the dropdown from **Audit only** to **Block**.
      - Select **Save**.

   1. In the **Create rule** flyout, under **Upload to a restricted cloud service domain or access from an unallowed browser**, set the restriction to **Audit only**.

1. In the same **Service domain and browser activities** section:

   1. Select the checkbox for **Paste to supported browsers**.

   1. Next to this option, select **+ Choose different restrictions for sensitive service domains**.

   1. In the **Sensitive service domain restrictions** flyout:

      - Select **+ Add group**.
      - In the **Choose sensitive service domain groups** flyout, select the checkbox for **Generative AI Websites**, then select **Add**.
      - Back on the **Sensitive service domain restrictions** flyout, change the action in the dropdown from **Audit only** to **Block**.
      - Select **Save**.

   1. In the **Create rule** flyout, under **Paste to supported browsers**, set the restriction to **Audit only**.

1. Under **User notifications**:

    - Turn **On** the toggle for **Use notifications to inform your users and help educate them on the proper use of sensitive info.**
    - Select the checkbox to **Show users a policy tip notification when an activity is restricted...**.

1. Select **Save** at the bottom of the **Create rule** flyout.

1. Back on the **Customize advanced DLP rules**, select **Next**.

1. On the **Policy mode** page, select **Run the policy in simulation mode**. Leave automatic activation after fifteen days unchecked.

1. Select **Next**.

1. On the **Review and finish** page, review your policy settings then select **Submit** to create the policy.

1. Once the policy is created select **Done** on the **New policy created** page.

Your endpoint policy is saved in simulation and won't block activity. Next, configure alerts while keeping the policy in simulation.

## Task 3 - Configure DLP alert settings

Configure medium-severity email alerts for the endpoint rule so the MOD Administrator can review matching activity.

1. On the **Policies** page of the **Data Loss Prevention**, select the **Block AI website uploads of banking data** policy, then select **Edit policy** (pencil) icon !IMAGE[9icgyxg3.png](instructions359483/9icgyxg3.png).

1. Select **Next** until you reach the **Customize advanced DLP rules** page.

1. Select the pencil icon to the right of the **Block banking data exposure to AI websites** rule to edit the rule.!IMAGE[s2wct8be.png](instructions359483/s2wct8be.png)

1. In the **Edit rule** flyout, scroll down to the **Incident reports** section.

1. In the **Incident reports** section:

   - In **Use this severity level in admin alerts and reports**, set the dropdown to **Medium**.

   - Ensure the toggle is set to **On** for **Send an alert to admins when a rule match occurs**.

   - Under **Send email alerts to these people (optional)**, select **+ Add or remove users**.

      - In the **Add or remove users** flyout, search for, then select `MOD Administrator`

      - Select the checkbox to the left of the **MOD Administrator** account, then select **Add** at the bottom of the flyout.

   - Select **Send alert every time an activity matches the rule**.

1. Select **Save** at the bottom of the flyout.

1. Back on the **Customize advanced DLP rules** page, select **Next**.

1. On the **Policy mode** page, keep **Run the policy in simulation mode** selected and automatic activation unchecked, then select **Next**.

1. On the **Review and finish** page, review your policy settings then select **Submit** to create the policy.

1. Select **Done** on the **Policy updated** page.

You've configured medium-severity alerts for the MOD Administrator. Next, group repeated detections to make alerts easier to review.

## Task 4 - Configure DLP alert aggregation

Group repeated DLP detections from the same user into a 30-minute window to reduce alert volume.

1. In the Microsoft Purview portal, go to **Settings** > **Data Loss Prevention**.

1. On the **Event aggregation into alerts** option, select **User based** from the right panel under **Select aggregation type**.
!IMAGE[7fxjwcrs.png](instructions359483/7fxjwcrs.png)

1. Click the dropdown menu under **Alert aggregation window** to 30 minutes.
!IMAGE[hor2i9dj.png](instructions359483/hor2i9dj.png)

1. Select **Save**.

You've configured a 30-minute aggregation window to help administrators review repeated activity together.

## Section complete

You've enabled the Copilot restriction and prepared the banking-data endpoint policy and alerts. The endpoint policy remains in simulation so you can evaluate matches without blocking activity.

Continue to Insider Risk Management to configure detection of potentially risky AI activity.

===

# Lab - Detect risky AI usage with Insider Risk Management

Alex wants to understand potentially risky AI activity alongside the controls configured for financial information. You'll enable AI indicators, create an Insider Risk Management policy, and prepare a notice template for reviewer follow-up. The policy evaluates AI activity, not just financial content, and doesn't change DLP enforcement.

**Tasks**:

1. Assign insider risk management permissions
1. Configure analytics and AI risk indicators
1. Create a Risky AI usage policy
1. Create a notice template for AI usage guidance
<!-- Adaptive Protection tasks retained for future validation.
1. Connect the AI policy to Adaptive Protection
1. Add risk-based enforcement to the existing endpoint policy
-->

## Task 1 - Assign insider risk management permissions

Add Alex Wilber to the Insider Risk Management role group to access the features used in this section.

1. In your existing **Microsoft Purview portal** session, select **Settings** > **Roles and Scopes** > **Role groups**.

1. On the **Role groups for Microsoft Purview solutions** page, select **Insider Risk Management**.

1. On the **Insider Risk Management** flyout panel on the right, select the **Members** tab.

1. On the **Members** tab, select **+ Add member** > **Choose users**.

1. On the **Choose users** tab, select **Alex Wilber**, then select **Select**.

1. Back on the **Members** tab, select **Done**.

1. Select **Confirm** to confirm updating the role group.

Alex is now a member of the Insider Risk Management role group. Next, configure analytics and AI activity indicators.

## Task 2 - Configure analytics and AI risk indicators

Enable analytics and select the Copilot and other AI activity indicators that your risk policy will use.

1. In your existing **Microsoft Purview portal** session, select **Settings** > **Insider risk management**.

1. On the **Insider Risk Management settings** page, select **Analytics** from the left navigation.

1. On the **Analytics** page, under **Show insights at tenant level**, switch the toggle to **On**. This will also enable **Show insights at the user level**.

1. Select **Save** at the bottom of the page.

1. On the **Insider Risk Management settings** page, select the tab on the left for **Policy indicators**.

1. Expand each category and enable the following indicators:

   **Generative AI apps** > **Microsoft Copilot experiences**

   - Receiving sensitive response from Copilot
   - Entering risky prompt in Copilot

1. Select **Save** at the bottom of the page.

Your AI indicators are enabled. Next, select the users and activities to evaluate in a Risky AI usage policy.

## Task 3 - Create a Risky AI usage policy

Create an organization-wide AI risk policy using Microsoft's built-in thresholds. This adds activity-based detection alongside the content-based DLP policies you configured earlier.

1. In the Microsoft Purview portal, go to **Solutions** > **Insider Risk Management** > **Policies**.

1. On the **Policies** page, select **+ Create policy** > **Custom policy**.

1. On the **Choose a policy template** page, select **Risky AI usage**, then select **Next**.

1. On the **Name your policy** page, enter:

   - **Name**: `Risky AI usage - financial data protection`
   - **Description**: `Identifies potentially risky Copilot prompts and sensitive responses to support review of AI usage.`

1. Select **Next**.

1. On the **Choose users, groups, & adaptive scopes** page, choose the option to include all users and groups, then select **Next**.

1. On the **Exclude users and groups (optional)** page, leave exclusions empty, then select **Next**.

1. On the **Decide whether to prioritize content** page, select **I don't want to prioritize content right now**, then select **Next**.

1. On the **Choose triggering event for this policy** page, select **Risky or sensitive content in Microsoft Copilot experiences, Enterprise AI apps and web versions of other AI apps**.

1. Under **Select which activities will trigger this policy**, check the boxes for:

   - Entering risky prompt in Copilot
   - Receiving sensitive response from Copilot

    >[!Note] **Note:** If these triggers are already selected, confirm them and continue.

1. Select **Next**.

1. On the **Choose thresholds for triggering events** page, select **Apply built-in thresholds**, then select **Next**.

1. On the **Indicators** page, expand each category and confirm that the Copilot indicators enabled in Task 2 are selected, then select **Next**.

1. On the **Detection options** page, leave the defaults selected, then select **Next**.

1. On the **Choose threshold type for indicators** page, select **Apply thresholds provided by Microsoft**, then select **Next**.

1. On the **Review settings and finish** page, confirm that the policy uses the **Risky AI usage** template, includes all users and groups, and uses the selected AI indicators and Microsoft-provided thresholds. Select **Submit**.

1. On the **Your policy was created** page, select **Done**.

Your AI risk policy is configured to evaluate potentially risky Copilot activity. Next, prepare guidance that a reviewer can use during case follow-up. No live alert is required.

## Task 4 - Create a notice template for AI usage guidance

Prepare a reusable message about handling financial information with AI. Reviewers can use the template when following up with an employee during case review.
For this scenario we will switch from MOD admin to Alex Wilber user.

1. Click top right **End Session** button of the window and validate 
!IMAGE[81xumc3h.png](instructions359483/81xumc3h.png)!IMAGE[pe2w4fij.png](instructions359483/pe2w4fij.png)

2. Click on these credentials to login again

| Alex Wilber username | +++AlexW@@lab.CloudCredential(WWLM365E7).TenantName+++ |

| Alex Wilber password | +++@lab.CloudCredential(WWLM365E7).UserPassword+++ |

| Temporary Access Pass, when requested | +++@lab.CloudCredential(WWLM365E7).AlexWTAP+++ |

3. In the **Microsoft Purview portal**, go to **Solutions** > **Insider Risk Management** > **Users** > **Notice templates**.

1. Select **Create notice template**.

1. On the **Create a new notice template** page, enter:

   - **Template name**: `Financial information and AI usage guidance`
   - **Send from**: Enter the email address of Alex Wilber's lab account.
   - **Subject**: `Reminder: Handling financial information with AI`
   - **Message body**:

     ```text
     Please review how you use business information with Copilot and other AI tools.

     Check the sensitivity label before sharing financial documents, and use only AI tools approved by Contoso. Don't enter payment details or other sensitive information into unapproved AI services.

     If you're unsure how to handle information, contact your IT security team for guidance.

     Thank you,
     Contoso Security and Compliance Team
     ```

1. Select **Create** to save the template.

1. Confirm that **Financial information and AI usage guidance** appears in the template list.

You've prepared a consistent message for reviewer follow-up. Saving the template doesn't send an email or automatically notify users when the policy detects activity.

<!--
## Task 5 - Connect the AI policy to Adaptive Protection

Connect your AI policy to insider risk levels. Adaptive Protection uses configured activity and alert conditions to determine these levels.

1. In the Microsoft Purview portal, go to **Solutions** > **Insider Risk Management** > **Users** > **Adaptive Protection**.

1. From the left navigation, select **Adaptive Protection settings** and turn it on, then click **save**
!IMAGE[lz6z44tb.png](instructions359483/lz6z44tb.png)

2. From the left navigation, select **Insider risk levels**.

1. On the **Insider risk levels** page, in the **Insider risk policy** dropdown, select the **Risky AI usage - financial data protection** policy you created earlier.

1. Review the default conditions for **Elevated**, **Moderate**, and **Minor** risk. Note which conditions assign an **Elevated** risk level. You'll use this level in the endpoint DLP rule.

1. Leave the default risk level settings unchanged, then select **Save**.

Your AI policy is connected to insider risk levels. Next, use an elevated risk level as a DLP condition.

## Task 6 - Add risk-based enforcement to the existing endpoint policy

Update the endpoint policy you prepared earlier, rather than creating another DLP policy. Keep its banking information types and AI website actions, add the Elevated risk condition, and then enable Adaptive Protection and enforcement.

1. Go to **Settings** > **Data Loss Prevention** > **Endpoint DLP settings**. Enable **Advanced classification scanning and protection** if it isn't already enabled, and save any changes.

   > [!NOTE]
   > Microsoft requires advanced classification scanning and protection or a File type condition for Adaptive Protection on devices. This exercise uses the advanced classification setting, which sends supported file content to Microsoft's cloud classification service. See [Adaptive Protection for endpoint DLP](https://learn.microsoft.com/en-us/purview/dlp-adaptive-protection-learn#policy-values-for-devices-dlp-policy).

1. Go to **Solutions** > **Data Loss Prevention** > **Policies**.

1. Select **Block AI website uploads of banking data**, then select **Edit policy**.

1. Update the policy description to:

   `Blocks banking data uploads and pasting to configured AI websites only when the user's Adaptive Protection insider risk level is Elevated.`

1. Select **Next** until you reach **Customize advanced DLP rules**. Edit **Block banking data exposure to AI websites**.

1. Under **Conditions**, keep the existing **Content contains** condition and its banking sensitive information types.

1. Select **+ Add condition** > **User's insider risk level for Adaptive Protection is**, then select **Elevated risk**.

1. Confirm that the conditions use **AND** logic:

   - Content contains at least one of the banking information types selected earlier.
   - The user's insider risk level is **Elevated**.

   Don't use **OR**. Both conditions must match for this rule's blocking actions to apply.

1. Keep the existing **Generative AI Websites** group restrictions set to **Block** for uploads and pasting. Keep the default restrictions outside that group at **Audit only**, and leave the notifications and medium-severity alert settings unchanged.

1. Select **Save** to save the rule, then select **Next**.

1. On the **Policy mode** page, keep **Run the policy in simulation mode** selected and automatic activation unchecked, then select **Next**.

1. On **Review and finish**, confirm the banking content **AND Elevated risk** conditions and the existing AI website actions, then select **Submit**. Select **Done** on the confirmation page.

1. Return to **Solutions** > **Insider Risk Management** > **Adaptive Protection**.

1. On the **Adaptive Protection** page, select **Adaptive Protection settings** from the left navigation.

1. Set the toggle to **On** under **Adaptive Protection**, then select **Save** to enable Adaptive Protection.

1. Return to **Solutions** > **Data Loss Prevention** > **Policies**. Edit **Block AI website uploads of banking data** again.

1. Select **Next** to reach **Customize advanced DLP rules**. Confirm that the rule still includes both the banking content condition and **Elevated risk**, joined with **AND**, then select **Next**.

1. On **Policy mode**, select **Turn the policy on immediately**, then select **Next**.

1. On **Review and finish**, verify your settings, then select **Submit**. Select **Done** on the confirmation page.

Your existing endpoint policy now uses both banking content and Elevated risk to determine when to block AI website activity. Users without an Elevated risk assignment don't match this rule; other policies can still apply.

> [!NOTE]
> Risk assignments and endpoint policy updates take time to reach devices. Complete this task by verifying the saved AND conditions, enabled policy, risk-level settings, and Adaptive Protection toggle. No live block or risk-level change is required. The separate Copilot label-based policy remains unchanged.
-->

## Section complete

You've configured a policy to detect potentially risky AI activity and created a notice template for reviewer follow-up. These tools help Alex identify activity for review and prepare consistent guidance for employees.

Continue to Microsoft Agent 365 to generate activity with Analyst and explore how it appears in Purview and Agent 365.

===

# Lab - Explore agent activity in Microsoft Purview and Agent 365

You've helped Alex configure classification, DLP, and AI risk detection. Now, use Analyst to work with the financial document you created earlier, then review activity in Microsoft Purview and Microsoft Agent 365. This final section connects the employee's AI experience with the administrator's view of agent use.

**Tasks**:

1. Generate activity with Analyst
1. Review Copilot activity in Microsoft Purview
1. Review Analyst in Microsoft Agent 365

## Task 1 - Generate activity with Analyst

Ask Analyst to compare the budget and expenses in your fictional financial document. Keep its Confidential/All Employees label applied.

> [!NOTE]
> The Copilot DLP policy takes time to synchronize. This exercise focuses on generating and reviewing agent activity, not testing the restriction.

1. In the **Microsoft Purview portal**, select the **Microsoft 365 app launcher** (the nine-dot icon), then open **Copilot**. If it isn't listed, select **More apps** to find it.

1. In Copilot, select the **+** button in the prompt bar, then select **Add capabilities > Analyze data**.

1. Select **Attach cloud files**, then select **My files** on the left pane.

1. Select the **Contoso financial planning summary.docx** file created previously, then select **Select**.

1. In the prompt bar, enter the following prompt, then select **Send**.

   ```text
   Using this document, how much of the budget remains after forecast expenses, and what percentage of the budget do those expenses use?
   ```

6. Wait for Analyst to respond, then continue. 

You've used an agent with the same financial content from the earlier exercises. Next, look at the interaction from an administrator's perspective.

## Task 2 - Review Copilot activity in Microsoft Purview

Use Activity explorer to look for Copilot interactions. You're reviewing usage, not looking for a DLP block or a sensitive information match.

> [!NOTE]
> Activity records can take time to appear, and Copilot interaction logging requires auditing to be enabled. If your interaction isn't available yet, review an existing record if one is available, then continue. Don't wait for synchronization to complete during the session.

1. Return to the **Microsoft Purview portal** tab.

1. Go to **Solutions** > **Information Protection**, then expand **Explorers**.

1. Select **Activity explorer** and set the date range to include today's activity.

1. Set the **Activity** filter to **Copilot Interaction** and filter by your lab account.

1. Open a recent interaction, if available, and review the details shown:

   - Activity time and user
   - Application or workload
   - Agent information, if recorded
   - Referenced resources and prompt or response details, where available to your role

You've reviewed individual Copilot activity in Purview. Next, review Analyst's usage in Agent 365.

## Task 3 - Review Analyst in Microsoft Agent 365

Review Analyst's usage metrics and compare this summary with the individual activity records in Purview.

1. Open a new browser tab and go to `https://admin.microsoft.com`.

1. In the **Microsoft 365 admin center**, select **Agents** > **All Agents** > **Registry**.

1. Search for **Analyst**, then select the Microsoft-published agent to open its details.

1. Select the **Activity** tab and review the date range and last activity date.

1. Review the available **Usage** metrics:

   - Active users
   - Sessions
   - Exceptions
   - Agent run-time

1. Review the **Active users over time** chart. Look for recent usage without expecting a specific count.

1. Compare the two views:

   - **Purview Activity explorer** provides individual activity records and their available security and compliance details.
   - **Agent 365 Activity** summarizes usage and operational metrics for Analyst.

You've explored individual activity records in Purview and agent-level usage in Agent 365.

## Lab complete

You helped Alex classify financial information, configure DLP policies, and prepare AI risk detection and reviewer guidance. You then used Analyst with the sample document and reviewed activity in Purview and Agent 365. Together, these exercises show how to classify sensitive content, configure controls for AI use, and monitor agent activity.
