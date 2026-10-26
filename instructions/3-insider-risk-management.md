# Lab – Detect and adapt to risky AI usage with Insider Risk Management

Alex wants to protect financial information without blocking every employee's AI activity. You'll configure AI risk detection, connect it to Adaptive Protection, and update the banking-data endpoint policy from the DLP section. Its blocking actions will require both matching banking content and an Elevated insider risk level.

> [!NOTE]
> This section focuses on configuration, not generating live alerts or risk levels. Results take time to populate. Risk signals support review; they aren't proof of misconduct.

> [!NOTE]
> AI detection requires appropriate licensing, permissions, and signal collection, including browser extensions on monitored devices. See the [Risky AI usage prerequisites](https://learn.microsoft.com/en-us/purview/insider-risk-management-policy-templates#risky-ai-usage). You won't install extensions or submit sensitive information to AI services in this exercise.

**Tasks**:

1. Configure analytics and AI risk indicators
1. Create a Risky AI usage policy
1. Configure insider risk levels
1. Add risk-based enforcement to the existing endpoint policy

## Task 1 – Configure analytics and AI risk indicators

Enable analytics and select the Copilot and other AI activity indicators that your risk policy will use.

1. In your existing **Microsoft Purview portal** session, select **Settings** > **Insider risk management**.

1. On the **Insider Risk Management settings** page, select **Analytics** from the left navigation.

1. On the **Analytics** page, under **Show insights at tenant level**, switch the toggle to **On**.

1. Select **Save** at the bottom of the page.

1. On the **Insider Risk Management settings** page, select the tab on the left for **Policy indicators**.

1. Expand each category and enable the following indicators:

   **Generative AI apps** > **Microsoft Copilot experiences**

   - Receiving sensitive response from Copilot
   - Entering risky prompt in Copilot

   **Generative AI apps** > **Other AI apps**

   - Entering risky prompt in other AI apps

1. Select **Save** at the bottom of the page.

Your AI indicators are enabled. Next, select the users and activities to evaluate in a Risky AI usage policy.

## Task 2 – Create a Risky AI usage policy

Create an organization-wide AI risk policy using Microsoft's built-in thresholds. Its signals will supply user risk context for the banking-data endpoint rule, rather than detecting financial content itself.

1. In the Microsoft Purview portal, go to **Solutions** > **Insider Risk Management** > **Policies**.

1. On the **Policies** page, select **+ Create policy** > **Custom policy**.

1. On the **Choose a policy template** page, select **Risky AI usage**, then select **Next**.

1. On the **Name your policy** page, enter:

   - **Name**: `Risky AI usage - financial data protection`
   - **Description**: `Evaluates potentially risky AI activity to inform Adaptive Protection for the banking-data endpoint DLP policy.`

1. Select **Next**.

1. On the **Choose users, groups, & adaptive scopes** page, choose the option to include all users and groups, then select **Next**.

1. On the **Exclude users and groups (optional)** page, leave exclusions empty, then select **Next**.

1. On the **Decide whether to prioritize content** page, choose not to prioritize specific content, then select **Next**.

1. On the **Choose triggering event for this policy** page, select **Risky or sensitive content in Microsoft Copilot experiences, Enterprise AI apps and web versions of other AI apps**.

1. Under **Select which activities will trigger this policy**, check the boxes for:

   - Entering risky prompt in Copilot
   - Receiving sensitive response from Copilot
   - Entering risky prompt in other AI apps

    >[!Note] **Note:** If these triggers are already selected, confirm them and continue.

1. Select **Next**.

1. On the **Choose thresholds for triggering events** page, select **Apply built-in thresholds**, then select **Next**.

1. On the **Indicators** page, expand each category and confirm that the Copilot and other AI apps indicators enabled in Task 1 are selected, then select **Next**.

1. On the **Detection options** page, leave the defaults selected, then select **Next**.

1. On the **Choose threshold type for indicators** page, select **Apply thresholds provided by Microsoft**, then select **Next**.

1. On the **Review settings and finish** page, confirm that the policy uses the **Risky AI usage** template, includes all users and groups, and uses the selected AI indicators and Microsoft-provided thresholds. Select **Submit**.

1. On the **Your policy was created** page, select **Done**.

Your AI risk policy is configured. Next, connect it to Adaptive Protection's risk levels.

## Task 3 – Configure insider risk levels

Connect your AI policy to insider risk levels. Adaptive Protection uses configured activity and alert conditions to determine these levels.

1. In the Microsoft Purview portal, go to **Solutions** > **Insider Risk Management** > **Users** > **Adaptive Protection**.

1. From the left navigation, select **Insider risk levels**.

1. On the **Insider risk levels** page:

   - In the **Insider risk policy** dropdown, select the **Risky AI usage - financial data protection** policy you created earlier.
   - Leave the default risk level settings unchanged.
   - Select **Save**.

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

## Lab complete

You've helped Alex connect classification, DLP, and user risk around financial information. The Copilot policy uses Confidential/All Employees to identify content. The existing endpoint policy blocks banking data at configured AI websites only when Adaptive Protection assigns the user an Elevated risk level.
