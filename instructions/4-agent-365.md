# Lab – Explore agent activity in Microsoft Purview and Agent 365

You've helped Alex configure classification, DLP, and AI risk detection. Now, use Analyst to work with the financial document you created earlier, then review activity in Microsoft Purview and Microsoft Agent 365. This final section connects the employee's AI experience with the administrator's view of agent use.

**Tasks**:

1. Generate activity with Analyst
1. Review Copilot activity in Microsoft Purview
1. Review Analyst in Microsoft Agent 365

## Task 1 – Generate activity with Analyst

Ask Analyst to compare the budget and expenses in your fictional financial document. Keep its Confidential/All Employees label applied.

> [!NOTE]
> The Copilot DLP policy takes time to synchronize. This exercise focuses on generating and reviewing agent activity, not testing the restriction.

1. In the **Microsoft Purview portal**, select the **Microsoft 365 app launcher** (the nine-dot icon), then open **Microsoft 365 Copilot**. If it isn't listed, select **More apps** to find it.

1. In Copilot, select the **+** button in the prompt bar, then select **Analyze data**.

1. Select **Attach cloud files**, then select **My files** on the left pane.

1. Select the **Contoso financial planning summary.docx** file created previously, then select **Select**.

1. In the prompt bar, enter the following prompt, then select **Send**.

   ```text
   Using this document, how much of the budget remains after forecast expenses, and what percentage of the budget do those expenses use?
   ```

1. Wait for Analyst to respond, then continue.

You've used an agent with the same financial content from the earlier exercises. Next, look at the interaction from an administrator's perspective.

## Task 2 – Review Copilot activity in Microsoft Purview

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

## Task 3 – Review Analyst in Microsoft Agent 365

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

You helped Alex classify financial information, configure Copilot and endpoint DLP policies, and set up AI risk detection. You then used Analyst with the sample document and explored activity visibility in Purview and Agent 365. These views support ongoing review as policy changes and new activity finish processing.
