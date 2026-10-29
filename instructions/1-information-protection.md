# Lab – Manage sensitive data using Microsoft Purview Information Protection in the age of AI

Alex Wilber, Contoso's Information Security Administrator, needs employees to recognize sensitive financial information as they work with Microsoft 365 Copilot. You'll help Alex create and publish a sensitivity label, configure automatic detection of credit card numbers, and label a sample document. This classification work sets up the DLP controls you'll configure in the next section.

> [!NOTE]
> Copilot respects users' existing access permissions. The Financial data label you'll create adds classification and a footer, not encryption or a Copilot restriction.

**Tasks**:

1. Create a label group and a financial data label
1. Publish sensitivity labels
1. Configure auto-apply labeling
1. Apply the Confidential/All Employees label to a document

## Task 1 – Create a label group and a financial data label

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

1. On the **Define the scope for this label** page, select **Files & other data assets** and **Emails**. Make sure **Meetings** is deselected.

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

## Task 2 – Publish sensitivity labels

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

## Task 3 – Configure auto-apply labeling

Configure an auto-labeling policy using the built-in Credit card number sensitive information type (SIT). Start in simulation mode to evaluate matches before applying the Financial data label.

> [!NOTE]
> This rule detects credit card numbers, not all financial information. Simulation evaluates matches without applying labels. The policy is set to activate after seven days if it isn't modified.

1. In the Microsoft Purview portal, under **Information Protection**, expand **Policies** then select **Auto-labeling policies**.

1. On the **Auto-labeling policies** page, select **+ Create auto-labeling policy**.

1. On the **What type of auto-labeling policy do you want to create?** page, select **Automatically apply labels only**.

1. On the **Choose info you want this label applied to** page, create a policy in a **Custom** category for a **Custom policy** regulation.

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

1. On the **Additional settings for email** page, select **Next**.

1. On the **Decide if you want to test out the policy now or later** page, select **Run policy in simulation mode**, and select the checkbox for **Automatically turn on policy if not modified after 7 days in simulation**.

1. Select **Next**.

1. On the **Review and finish** page, select **Create policy**.

1. On the confirmation page, select **Done**.

Your auto-labeling policy is configured in simulation mode. Next, apply a label manually to content that doesn't contain credit card numbers.

## Task 4 – Apply the Confidential/All Employees label to a document

Create a fictional budget summary in Word for the web and apply Confidential/All Employees. This gives you a labeled document for the next section's Copilot DLP policy.

1. In the **Microsoft Purview portal**, select the **Microsoft 365 app launcher** (the nine-dot icon in the upper-left corner).

1. Select **Word**. If Word isn't listed, select **More apps**, then select **Word**.

1. In **Word for the web**, confirm that you're signed in with the lab account provided for **Alex Wilber**, then create a blank document.

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

1. On the **Home** tab, select **Sensitivity** > **Confidential** > **All Employees**.

1. Confirm that Word for the web displays **Confidential/All Employees** as the document's sensitivity label. If only **All Employees** is displayed, open the **Sensitivity** menu and confirm that the selected label is under **Confidential**, not **General** or **Highly Confidential**.

1. Wait until Word indicates that your changes are saved.

> [!TIP]
> Optional: If Internal/Financial data is available, try it on a separate document and check for the footer `Contoso Financial Data - Internal Use Only`. Keep Confidential/All Employees on your main sample document for the DLP exercise.

Your budget summary is labeled. Because its figures don't match the credit card number rule, this demonstrates where manual classification complements automatic detection.

## Section complete

You've created and published Financial data, configured auto-labeling in simulation, and manually applied Confidential/All Employees to a sample document. Alex now has a classification foundation for the next layer of controls.

Continue to [data loss prevention](./2-data-loss-prevention.md) to configure Copilot restrictions and controls for external AI websites.
