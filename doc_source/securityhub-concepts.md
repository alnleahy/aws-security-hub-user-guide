# Terminology and concepts<a name="securityhub-concepts"></a>

This topic describes the key concepts in AWS Security Hub to help you get started\.

**Account**  
A standard Amazon Web Services \(AWS\) account that contains your AWS resources\. You can sign in to AWS with your account and enable Security Hub\.  
An account can invite other accounts to enable Security Hub and become associated with that account in Security Hub\. Accepting a membership invitation is optional\. If the invitations are accepted, the account becomes an administrator account, and the added accounts are member accounts\. Administrator accounts can view findings in their member accounts\.  
If you are enrolled in AWS Organizations, then your organization designates a Security Hub administrator account for the organization\. The Security Hub administrator account can enable other organization accounts as member accounts\.  
An account cannot be both an administrator account and a member account at the same time\. An account can only have one administrator account\.  
For more information, see [Managing administrator and member accounts](securityhub-accounts.md)\.

**Administrator account**  
An account in Security Hub that is granted access to view findings for associated member accounts\.  
An account becomes an administrator account in one of the following ways:  
+ The account invites other accounts to become associated with it in Security Hub\. When those accounts accept the invitation, they become member accounts, and the inviting account becomes their administrator account\.
+ The account is designated by an organization management account as the Security Hub administrator account\. The Security Hub administrator account can enable any organization account as a member account, and can also invite other accounts to be member accounts\.
An account can only have one administrator account\. An account cannot be both an administrator account and a member account at the same time\.

**Aggregation Region**  
Setting an aggregation Region allows you to view security findings from multiple Regions in a single pane of glass\.   
The aggregation Region is the Region from which you view and manage findings\. Findings are aggregated to the aggregation Region from linked Regions\. Updates to findings are replicated across Regions\.  
In the aggregation Region, the **Security standards**, **Insights**, and **Findings** pages include data from all linked Regions\.  
See [Cross\-Region aggregation](finding-aggregation.md)\.

**Archived finding**  
A finding that has a `RecordState` set to `ARCHIVED`\. Archiving a finding indicates that the finding provider believes that the finding is no longer relevant\. The record state is separate from the workflow status, which tracks the status of an investigation into a finding\.  
Finding providers can use the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchImportFindings.html) operation of the Security Hub API to archive findings that they created\. Security Hub automatically archives findings for controls if the control is disabled or the associated resource is deleted, based on one of the following criteria\.  
+ The finding is not updated in three to five days \(note that this is best effort and not guaranteed\)\.
+ The associated AWS Config evaluation returns `NOT_APPLICABLE`\.
By default, archived findings are excluded from findings lists in the Security Hub console\. You can update the filter to include archived findings\.  
The [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetFindings.html) operation of the Security Hub API returns both active and archived findings\. You can include a filter for the record state\.  

```
"RecordState": [ 
    { 
        "Comparison": "EQUALS",
        "Value": "ARCHIVED"
    }
],
```

**AWS Security Finding Format \(ASFF\)**  
A standardized format for the contents of findings that Security Hub aggregates or generates\. The AWS Security Finding Format enables you to use Security Hub to view and analyze findings that are generated by AWS security services, third\-party solutions, or Security Hub itself from running security checks\. For more information, see [AWS Security Finding Format \(ASFF\)](securityhub-findings-format.md)\.

**Control**  
A safeguard or countermeasure prescribed for an information system or an organization designed to protect the confidentiality, integrity, and availability of its information and to meet a set of defined security requirements\. A security standard consists of controls\.

**Custom action**  
A Security Hub mechanism for sending selected findings to EventBridge\. A custom action is created in Security Hub\. It is then linked to an EventBridge rule\. The rule defines a specific action to take when a finding is received that is associated with the custom action ID\. Custom actions can be used, for example, to send a specific finding, or a small set of findings, to a response or remediation workflow\. For more information, see [Creating a custom action \(console\)](securityhub-cwe-custom-actions.md#securityhub-cwe-configure)\.

**Delegated administrator account \(Organizations\)**  
In Organizations, the delegated administrator account for a service is able to manage the use of a service for the organization\.  
In Security Hub, the Security Hub administrator account is also the delegated administrator account for Security Hub\. When the organization management account first designates a Security Hub administrator account, Security Hub calls Organizations to make that account the delegated administrator account\.  
The organization management account must then choose the delegated administrator account as the Security Hub administrator account in all Regions\.

**Finding**  
The observable record of a security check or security\-related detection\.  
For more information about findings in Security Hub, see [Findings in AWS Security Hub](securityhub-findings.md)\.  
Findings are deleted 90 days after the most recent update or 90 days after the creation date if no update occurs\. To store findings for longer than 90 days, you can configure a rule in EventBridge that routes findings to your Amazon S3 bucket\.

**Cross\-Region aggregation**  
The aggregation of findings, insights, control compliance statuses, and security scores from linked Regions to an aggregation Region\. You can then view all of your data from the aggregation Region and update findings and insights from the aggregation Region\.  
See [Cross\-Region aggregation](finding-aggregation.md)\.

**Finding ingestion**  
The import of findings into Security Hub from other AWS services and from third\-party partner providers\.  
Finding ingestion events include both new findings and updates to existing findings\.

**Insight**  
A collection of related findings defined by an aggregation statement and optional filters\. An insight identifies a security area that requires attention and intervention\. Security Hub offers several managed \(default\) insights that you can't modify\. You can also create custom Security Hub insights to track security issues that are unique to your AWS environment and usage\. For more information, see [Insights in AWS Security Hub](securityhub-insights.md)\.

**Linked Region**  
When you enable cross\-Region aggregation, a linked Region is a region that aggregates findings, insights, control compliance statuses, and security scores to the aggregation Region\.  
In a linked Region, the **Findings** and **Insights** pages contain findings only from that Region\.  
See [Cross\-Region aggregation](finding-aggregation.md)\.

**Member account**  
An account that has granted permission to an administrator account to view and take action on their findings\.  
An account becomes a member account in one of the following ways:  
+ The account accepts an invitation from another account\.
+ For an organization account, the Security Hub administrator account enables the account as a member account\.

**Related requirements**  
A set of industry or regulatory requirements that are mapped to a control\.

**Rule**  
A set of automated criteria that is used to assess whether a control is being adhered to\. When a rule is evaluated, it can pass or fail\. If the evaluation cannot determine whether rule passes or fails, then the rule is in a warning state\. If the rule cannot be evaluated, then it is in a not available state\.

**Security check**  
A specific point\-in\-time evaluation of a rule against a single resource resulting in a passed, failed, warning, or not available state\. Running a security check produces a finding\.

**Security Hub administrator account**  
An organization account that manages Security Hub membership for an organization\.  
The organization management account designates the Security Hub administrator account in each Region\. The organization management account must choose the same Security Hub administrator account in all Regions\.  
The Security Hub administrator account is also the delegated administrator account for Security Hub in Organizations\.  
The Security Hub administrator account can enable any organization account as a member account\. The Security Hub administrator account can also invite other accounts to be member accounts\.

**Security standard**  
A published statement on a topic specifying the characteristics, usually measurable and in the form of controls, that must be satisfied or achieved for compliance\. Security standards can be based on regulatory frameworks, best practices, or internal company policies\. To learn more about security standards in Security Hub, see [Security standards and controls in AWS Security Hub](securityhub-standards.md)\.

**Severity**  
The severity assigned to a Security Hub control identifies the importance of the control\. The severity of a control can be **Critical**, **High**, **Medium**, **Low**, or **Informational**\. The severity assigned to control findings is equal to the severity of the control itself\. To learn about how Security Hub assigns severity to a control, see [Assigning severity to control findings](controls-findings-create-update.md#control-findings-severity)\.

**Workflow status**  
The status of an investigation into a finding\. Tracked using the `Workflow.Status` attribute\.  
The workflow status is initially `NEW`\. If you notified the resource owner to take action on the finding, you can set the workflow status to `NOTIFIED`\. If the finding is not an issue, and does not require any action, set the workflow status to `SUPPRESSED`\. After you review and remediate a finding, set the workflow status to `RESOLVED`\.  
By default, most finding lists only include findings with a workflow status of `NEW` or `NOTIFIED`\. Finding lists for controls also include `RESOLVED` findings\.  
For the [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_GetFindings.html) operation, you can include a filter for the workflow status\.  

```
"WorkflowStatus": [ 
    { 
        "Comparison": "EQUALS",
        "Value": "RESOLVED"
    }
],
```
The Security Hub console provides an option to set the workflow status for findings\. Customers \(or SIEM, ticketing, incident management, or SOAR tools working on behalf of a customer to update findings from finding providers\) can also use [https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html](https://docs.aws.amazon.com/securityhub/1.0/APIReference/API_BatchUpdateFindings.html) to update the workflow status\.