# Lab – Manage sensitive data using Microsoft Purview Information Protection in the age of AI

Alex Wilber, the Information Security Administrator at Contoso Ltd., is preparing the company's information for use with Microsoft 365 Copilot. Employees use Copilot to find information and summarize business documents, so Alex needs a consistent way to distinguish sensitive financial data from general internal content. In this lab, you'll help Alex create and publish sensitivity labels, configure an auto-labeling policy that detects credit card numbers using a built-in sensitive information type (SIT), and manually label a sample financial document.

The goal is to establish a classification foundation for responsible AI use. Microsoft 365 Copilot respects users' existing access permissions. The financial data label you create adds a visible footer; it doesn't encrypt content or prevent Copilot from using it. Classification can also support additional controls, such as the Copilot DLP policy in the [data loss prevention lab](./2-data-loss-prevention.md).

**Tasks**:

1. Create a label group and a financial data label
1. Publish sensitivity labels
1. Configure auto-apply labeling
1. Apply the Financial data label to a document

## Task 1 – Create a label group and a financial data label

Alex needs a consistent way to identify sensitive financial information as employees work with it, including through Microsoft 365 Copilot. In this task, you'll create an Internal label group and a Financial data label with a visible footer to help employees recognize content intended for internal use.

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

You created a Financial data label in the Internal label group. Its footer helps users recognize sensitive financial content when reading, sharing, or reusing it. The label provides classification, not an access restriction.

## Task 2 – Publish sensitivity labels

With the label created, you'll publish it so users and policies can apply it across Microsoft 365 workloads. Publishing makes the label available for manual and automated use.

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

You published the Internal/Financial data label so it can be applied manually or automatically. This makes the label available for use in your upcoming auto-labeling policy.

## Task 3 – Configure auto-apply labeling

You'll now configure an auto-labeling policy to apply the Financial data label when the built-in Credit card number SIT detects a match. This helps Alex classify sensitive payment information consistently, including content employees might reference in Copilot. You'll start the policy in simulation mode so its matches can be reviewed before labels are applied.

This rule detects credit card numbers, not all financial information. Users can apply the Financial data label manually to other sensitive financial content. No custom SIT is required.

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

You configured an auto-labeling policy in simulation mode, with automatic activation after seven days if the policy isn't modified. Simulation doesn't apply labels. Once active, the policy can label matching content to support consistent classification and label-based controls; it doesn't by itself restrict sharing or Copilot access.

## Task 4 – Apply the Financial data label to a document

Alex also needs employees to recognize financial information that isn't detected by the credit card number rule. In this task, you'll create a fictional budget summary in Word for the web, apply the Financial data label manually, and verify its footer. This lets you see the label in use without waiting for the auto-labeling simulation to finish.

> [!NOTE]
> Use your lab account, which must be included in the label publishing policy from Task 2. Newly published labels can take time to appear. If Financial data isn't available, confirm that you're signed in with the correct account and included in the policy, then allow time for the policy to reach Word for the web before refreshing the page. If the Sensitivity option is unavailable, also confirm that sensitivity labels are enabled for files in SharePoint and OneDrive. Don't select a different label to complete this task.

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

1. On the **Home** tab, select **Sensitivity** > **Internal** > **Financial data**.

1. Confirm that Word for the web displays **Financial data** as the document's sensitivity label.

1. Scroll to the bottom of the page and confirm that the footer contains:

   `Contoso Financial Data - Internal Use Only`

1. Wait until Word indicates that your changes are saved.

You manually classified a financial document and verified its label and visible footer. The budget figures don't match the credit card number rule, which demonstrates why manual classification still matters. The label doesn't restrict access or block Copilot by itself; the next lab adds a label-based DLP control.

## Lab complete

You helped Alex Wilber establish a classification foundation for Contoso's use of Microsoft 365 Copilot. You created and published a financial data label, configured an auto-labeling policy in simulation mode to detect credit card numbers, and manually labeled a sample financial document. These changes help distinguish sensitive financial information from general internal content without changing who can access it.

Continue to the [data loss prevention lab](./2-data-loss-prevention.md) to add a DLP safeguard that controls how Copilot handles labeled financial data.
