# Lab – Detect risky AI usage with Insider Risk Management

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

## Task 1 – Assign insider risk management permissions

Add Alex Wilber to the Insider Risk Management role group to access the features used in this section.

1. In your existing **Microsoft Purview portal** session, select **Settings** > **Roles and Scopes** > **Role groups**.

1. On the **Role groups for Microsoft Purview solutions** page, select **Insider Risk Management**.

1. On the **Insider Risk Management** flyout panel on the right, select the **Members** tab.

1. On the **Members** tab, select **+ Add member** > **Choose users**.

1. On the **Choose users** tab, select **Alex Wilber**, then select **Select**.

1. Back on the **Members** tab, select **Done**.

1. Select **Confirm** to confirm updating the role group.

Alex is now a member of the Insider Risk Management role group. Next, configure analytics and AI activity indicators.

## Task 2 – Configure analytics and AI risk indicators

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

## Task 3 – Create a Risky AI usage policy

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

## Task 4 – Create a notice template for AI usage guidance

Prepare a reusable message about handling financial information with AI. Reviewers can use the template when following up with an employee during case review.

1. In the **Microsoft Purview portal**, go to **Solutions** > **Insider Risk Management** > **Users** > **Notice templates**.

1. Select **Create notification template**.

1. On the **New email notification template** page, enter:

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

<!-- Adaptive Protection tasks retained for future validation.
## Task 3 – Connect the AI policy to Adaptive Protection

Connect your AI policy to insider risk levels. Adaptive Protection uses configured activity and alert conditions to determine these levels.

1. In the Microsoft Purview portal, go to **Solutions** > **Insider Risk Management** > **Users** > **Adaptive Protection**.

1. From the left navigation, select **Insider risk levels**.

1. On the **Insider risk levels** page, in the **Insider risk policy** dropdown, select the **Risky AI usage - financial data protection** policy you created earlier.

1. Review the default conditions for **Elevated**, **Moderate**, and **Minor** risk. Note which conditions assign an **Elevated** risk level. You'll use this level in the endpoint DLP rule.

1. Leave the default risk level settings unchanged, then select **Save**.

Your AI policy is connected to insider risk levels. Next, use an elevated risk level as a DLP condition.

## Task 4 – Add risk-based enforcement to the existing endpoint policy

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

Continue to [Microsoft Agent 365](./4-agent-365.md) to generate activity with Analyst and explore how it appears in Purview and Agent 365.
