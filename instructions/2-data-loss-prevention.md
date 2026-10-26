---
lab:
    title: 'Prevent data exposure in Copilot and AI apps with Data Loss Prevention'
    module: 'Prevent data exposure in Copilot and AI apps with Data Loss Prevention'
---

# Lab – Prevent data exposure in Copilot and AI apps with Data Loss Prevention

Alex now needs controls for how sensitive content is used with AI. You'll enable a label-based Copilot restriction and prepare an endpoint DLP policy for banking information sent to AI websites. Keep the endpoint policy in simulation until you add an insider risk condition in the next section.

**Tasks**:

1. Create a DLP policy for Copilot
1. Create an endpoint DLP policy
1. Configure DLP alert settings
1. Configure DLP alert aggregation

## Task 1 – Create a DLP policy for Copilot

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

1. On the **Choose locations to apply the policy** page, select the location for **Microsoft Copilot and Copilot Chat** only. If any other locations are selected, deselect them.

1. Keep the default **All users & groups** scope for Microsoft 365 Copilot, then select **Next**.

1. On the **Define policy settings** page, leave the default **Create or customize advanced DLP rules** selected, then select **Next**.

1. On the **Customize advanced DLP rules** page, select **+ Create rule**.

1. In the **Create rule** flyout, in the **Name** field, enter `Restrict Copilot confidential content`.

1. Under **Conditions**, select **+ Add condition** > **Content contains**.

1. In the **Content contains** section, select **Add** > **Sensitivity labels**.

   ![Screenshot of the Conditions pane in Microsoft Purview with Content contains selected and the Add menu showing Sensitivity labels.](./media/dlp-condition-sensitivity-label.png)

1. In the **Sensitivity labels** flyout, select the checkbox for **All Employees** with the label path **Confidential/All Employees**, then select **Add** at the bottom of the flyout.

1. Back on the **Create rule** flyout, under **Actions** select **+ Add an action** > **Restrict Copilot from processing content**.

1. Select **Save** at the bottom of the **Create rule** flyout.

1. Back on the **Customize advanced DLP rules** page, select **Next**

1. On the **Policy mode** page select **Turn the policy on immediately**, then select **Next**.

1. On the **Review and finish** page, verify the following settings, then select **Submit**:

   - **Location**: Microsoft Copilot and Copilot Chat only
   - **Scope**: All users & groups
   - **Sensitivity label**: Confidential/All Employees
   - **Action**: Restrict Copilot from processing content
   - **Policy mode**: Turn the policy on immediately

1. On the **New policy created** page select **Done**.

Your Copilot policy is enabled for content labeled Confidential/All Employees. Next, configure a different control for banking information sent to AI websites.

> [!NOTE]
> Copilot policy changes can take up to four hours to take effect. Verify the policy configuration to complete this task; a live blocking demonstration isn't required.

## Task 2 – Create an endpoint DLP policy

The Copilot policy checks a document's label. Next, prepare an endpoint policy that detects banking information directly. Configure blocking actions for AI websites, but leave the policy in simulation until you add the Elevated risk condition in the IRM section.

> [!NOTE]
> Endpoint enforcement requires supported, onboarded devices and browsers. Creating this policy doesn't onboard devices.

1. On the **Policies** page of the **Data Loss Prevention** solution of the Microsoft Purview portal, select **+ Create policy**.

1. On the **Choose what type of data to protect** page, select **Data stored in connected sources**, then select **Next**.

1. On the **Start with a template or create a custom policy** page, select **Custom** and **Custom policy**, then select **Next**.

1. On the **Name your DLP policy** page, enter:

    - **Name**: `Block AI website uploads of banking data`
    - **Description**: `Prepared in simulation for risk-based blocking of banking data uploads and pasting to AI websites. Add the Elevated risk condition before enabling enforcement.`

1. Select **Next**.

1. On the **Assign admin units** page, select **Next**.

1. On the **Choose locations to apply the policy** page, ensure only the **Devices** location is selected. If any other location is selected, ensure they're deselected, then select **Next**.

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

   1. Select the checkbox for **Upload to a restricted cloud service domain or access from an unallowed browser**.

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

    - Turn **On** the toggle for **Use notifications to inform your users and help educate them on the proper use of sensitive info.**.
    - Select the checkbox to **Show users a policy tip notification when an activity is restricted**.

1. Select **Save** at the bottom of the **Create rule** flyout.

1. Back on the **Customize advanced DLP rules**, select **Next**.

1. On the **Policy mode** page, select **Run the policy in simulation mode**. Leave automatic activation after fifteen days unchecked.

1. Select **Next**.

1. On the **Review and finish** page, review your policy settings then select **Submit** to create the policy.

1. Once the policy is created select **Done** on the **New policy created** page.

Your endpoint policy is saved in simulation and won't block activity yet. Next, configure alerts; keep it in simulation until the risk condition is added.

## Task 3 – Configure DLP alert settings

Configure medium-severity email alerts for the endpoint rule so the MOD Administrator can review matching activity.

1. On the **Policies** page of the **Data Loss Prevention**, select the **Block AI website uploads of banking data** policy, then select **Edit policy** (pencil) icon (![Icon of a pencil.](./media/edit-pencil-icon.png)).

1. Select **Next** until you reach the **Customize advanced DLP rules** page.

1. Select the pencil icon (![Icon of a pencil.](./media/edit-pencil-icon.png)) to the right of the **Block banking data exposure to AI websites** rule to edit the rule.

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

## Task 4 – Configure DLP alert aggregation

Group repeated DLP detections from the same user into a 30-minute window to reduce alert volume.

1. In the Microsoft Purview portal, go to **Settings** > **Data Loss Prevention**.

1. On the **Data Loss Prevention settings** page, select **Aggregate DLP alerts by user** from the left panel of the settings options.

1. On the **Aggregate DLP alerts by user** page, turn the toggle on.

1. In the **Alert aggregation window (in minutes)** dropdown, select **30**.

1. Select **Save**.

You've configured a 30-minute aggregation window to help administrators review repeated activity together.

## Section complete

You've enabled the Copilot restriction and prepared the banking-data endpoint policy and alerts. The endpoint policy is still in simulation. Next, add an Elevated risk condition so its blocking actions apply only when both content and user risk match.

Continue to [Insider Risk Management](./3-insider-risk-management.md) to configure AI risk detection and Adaptive Protection.
