# CIS AWS Foundations Benchmark v1\.4\.0<a name="securityhub-cis-controls-1.4.0"></a>

For CIS AWS Foundations Benchmark v1\.4\.0, Security Hub supports the following controls\. Note the severity, underlying AWS Config rule, schedule type, and remediation steps for each control\.

**Note**  
We recommend upgrading to CIS AWS Foundations Benchmark v1\.4\.0 to stay current on security best practices, but you may have both v1\.4\.0 and v1\.2\.0 enabled at the same time\. For more information, see [Disabling or enabling a security standard](securityhub-standards-enable-disable.md)\. If you want to upgrade to v1\.4\.0, it's best to enable v1\.4\.0 first before disabling v1\.2\.0\. If you use the Security Hub integration with AWS Organizations to centrally manage multiple accounts and wish to batch enable v1\.4\.0 across all accounts \(and disable v1\.2\.0 if you wish\), you can use a [Security Hub multi\-account script](https://github.com/awslabs/aws-securityhub-multiaccount-scripts)\. 

## 1\.4 – Ensure no root user account access key exists<a name="securityhub-cis1.4-controls-1.4"></a>

**Severity:** Critical

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-root-access-key-check.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-root-access-key-check.html)

**Schedule type:** Periodic

The root user has complete access to all services and resources in an AWS account\.Access keys provide programmatic access to a given account\.

CIS recommends that all access keys be associated with the root user be removed\. Removing access keys associated with the root user limits vectors that the account can be compromised by\. Removing the root user access keys also encourages the creation and use of role\-based accounts that are least privileged\.

**Note**  
This control is not supported in the Asia Pacific \(Osaka\) Region\.

### Remediation<a name="cis1.4-1.4-remediation"></a>

**To delete access keys**

1. Sign in to the AWS Management Console and open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

   Use the credentials of the root user\.

1. Choose the account name near the top\-right corner of the page and then choose **Security Credentials**\.

1. Choose **Access keys \(access key ID and secret access key\)**\.

1. To permanently delete the key, choose **Delete** and then choose **Yes**\. You cannot recover deleted keys\.

1. If there is more than one root user access key, then repeat steps 4 and 5 for each key\.

## 1\.5 – Ensure MFA is enabled for the root user account<a name="securityhub-cis1.4-controls-1.5"></a>

**Severity:** Critical

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/root-account-mfa-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/root-account-mfa-enabled.html)

**Schedule type:** Periodic

The root user has complete access to all the services and resources in an AWS account\. MFA adds an extra layer of protection on top of a user name and password\. With MFA enabled, when a user signs in to the AWS Management Console, they're prompted for their user name and password and for an authentication code from their AWS MFA device\.

When you use virtual MFA for the root user, CIS recommends that the device used is *not* a personal device\. Instead, use a dedicated mobile device \(tablet or phone\) that you manage to keep charged and secured independent of any individual personal devices\. This lessens the risks of losing access to the MFA due to device loss, device trade\-in, or if the individual owning the device is no longer employed at the company\.

**Note**  
This control is not supported in the following Regions\.  
China \(Beijing\)
China \(Ningxia\)
 AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="cis1.4-1.5-remediation"></a>

**To enable MFA for the root user**

1. Log in to your account using the root user credentials\.

1. Choose the account name near the top\-right corner of the page and then choose **My Security Credentials**\.

1. In the pop\-up warning, choose **Continue to Security Credentials**\.

1. Choose **Multi\-factor authentication \(MFA\)**\.

1. Choose **Activate MFA**\.

1. Choose the type of device to use for MFA and then choose **Continue**\.

1. Complete the steps to configure the device type appropriate to your selection\.

   Choose a hardware\-based authentication mechanism for best results in passing the check [1\.6 – Ensure hardware MFA is enabled for the root user account](#securityhub-cis1.4-controls-1.6)\.

## 1\.6 – Ensure hardware MFA is enabled for the root user account<a name="securityhub-cis1.4-controls-1.6"></a>

**Severity:** Critical

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/root-account-hardware-mfa-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/root-account-hardware-mfa-enabled.html)

**Schedule type:** Periodic

The root user has complete access to all services and resources in an AWS account\. MFA adds an extra layer of protection on top of a user name and password\. With MFA enabled, when a user signs in to an AWS website, they're prompted for their user name and password and for an authentication code from their registered MFA device\.

For the highest level of security \(Level 2\), CIS recommends that you protect root user credentials with a hardware MFA\. A hardware MFA has a smaller attack surface than a virtual MFA\. For example, a hardware MFA doesn't suffer the attack surface introduced by the mobile smartphone that a virtual MFA resides on\.

That said, using hardware MFA for many accounts might create a logistical device management issue\. If this occurs, consider implementing this Level 2 recommendation selectively to the highest security accounts\. You can then apply virtual MFA \(Level 1\) to the remaining accounts\.

Both time\-based one\-time password \(TOTP\) and Universal 2nd Factor \(U2F\) tokens are viable as hardware MFA options\.

**Note**  
This control is not supported in the following Regions\.  
China \(Beijing\)
China \(Ningxia\)
 AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="cis1.4-1.6-remediation"></a>

**To enable hardware MFA for the root user**

1. Sign in to the AWS Management Console using the root user credentials\.

1. Choose the account name near the top\-right corner of the page and then choose **My Security Credentials**\.

1. In the pop\-up warning, choose **Continue to Security Credentials**\.

1. Choose **Multi\-factor authentication \(MFA\)**\.

1. Choose **Activate MFA**\.

1. Choose a hardware\-based \(not virtual\) device to use for MFA and then choose **Continue**\.

1. Complete the steps to configure the device type appropriate to your selection\.

## 1\.7 – Eliminate use of the 'root user for administrative and daily tasks<a name="securityhub-cis1.4-controls-1.7"></a>

**Severity:** Low

**AWS Config rule:** None

**Schedule type:** Periodic

The root user has unrestricted access to all services and resources in an AWS account\. We highly recommend that you avoid using the root user for daily tasks\. Minimizing the use of the root user and adopting the principle of least privilege for access management reduce the risk of accidental changes and unintended disclosure of highly privileged credentials\.

As a best practice, use your root user credentials only when required to [ perform account and service management tasks](https://docs.aws.amazon.com/general/latest/gr/aws_tasks-that-require-root.html)\. Apply IAM policies directly to groups and roles but not users\. For a tutorial on how to set up an administrator for daily use, see [ Creating your first IAM admin user and group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the *IAM User Guide*

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 1\.7 in the [CIS AWS Foundations Benchmark v1\.4\.0](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:2e5fec5c-5e99-4fb5-b08d-bb46b14754c1#pageNum=1)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cis1.4-1.7-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [3\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis1.4-controls-3.1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {$.userIdentity.type="Root" && $.userIdentity.invokedBy NOT EXISTS && $.eventType !="AwsServiceEvent"}
      ```

   1. Choose **Next**\.

1. Under **Assign Metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric Namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric Name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. In the navigation pane, choose **Alarms** and then **All alarms**\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Choose **Select metric**\.

   1. On the **Select metric** panel, scroll down to **Metrics**\. Choose the **LogMetrics** namespace\. You can also use the search bar to search for it\.

   1. Choose **Metrics with no dimensions**\.

   1. Select the check box for the metric that you created\. Then choose **Select metric**\.

   1. Under **Metric**, leave the default values\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm, such as **CIS\-1\.7\-RootAccountUsage**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## 1\.8 – Ensure IAM password policy requires minimum length of 14 or greater<a name="securityhub-cis1.4-controls-1.8"></a>

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html)

**Schedule type:** Periodic

Password policies, in part, enforce password complexity requirements\. Use IAM password policies to ensure that passwords are at least a given length\.

CIS recommends that the password policy require a minimum password length of 14 characters\. Setting a password complexity policy increases account resiliency against brute force login attempts\.

### Remediation<a name="cis1.4-1.8-remediation"></a>

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Account settings**\.

1. In the **Minimum password length** field, enter **14**, then choose **Apply password policy**\.

## 1\.9 – Ensure IAM password policy prevents password reuse<a name="securityhub-cis1.4-controls-1.9"></a>

**Severity:** Low

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-password-policy.html)

**Schedule type:** Periodic

This control checks whether the number of passwords to remember is set to 24\. The control fails if the value is not 24\.

IAM password policies can prevent the reuse of a given password by the same user\.

CIS recommends that the password policy prevent the reuse of passwords\. Preventing password reuse increases account resiliency against brute force login attempts\.

### Remediation<a name="cis1.4-1.9-remediation"></a>

**To modify the password policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Account settings**\.

1. Select **Prevent password reuse** and then enter **24** for **Number of passwords to remember**\.

1. Choose **Apply password policy**\.

## 1\.10 – Ensure multi\-factor authentication \(MFA\) is enabled for all IAM users that have a console password<a name="securityhub-cis1.4-controls-1.10"></a>

**Severity:** Medium

**AWS Config rule: **[https://docs.aws.amazon.com/config/latest/developerguide/mfa-enabled-for-iam-console-access.html](https://docs.aws.amazon.com/config/latest/developerguide/mfa-enabled-for-iam-console-access.html)

**Schedule type:** Periodic

Multi\-factor authentication \(MFA\) adds an extra layer of protection on top of a user name and password\. With MFA enabled, when a user signs in to an AWS website, they're prompted for their user name and password as well as for an authentication code from their AWS MFA device\.

CIS recommends that you enable MFA for all accounts that have a console password\. MFA provides increased security for console access\. It requires the authenticating principal to possess a device that emits a time\-sensitive key and to have knowledge of a credential\.

**Important**  
The AWS Config rule used for this check may take up to 4 hours to accurately report results for MFA\. Any findings that are generated within the first 4 hours after you enable the CIS security checks might not be accurate\. It may also take up to 4 hours after you remediate this issue for the check to pass\.

### Remediation<a name="cis1.4-1.10-remediation"></a>

**To configure MFA for a user**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Users**\.

1. Choose the **User name** of the user to configure MFA for\.

1. Choose **Security credentials** and then choose **Manage** next to **Assigned MFA device**\.

1. Follow the **Manage MFA Device** wizard to assign the type of device appropriate for your environment\.

To learn how to delegate MFA setup to users, see [How to Delegate Management of Multi\-Factor Authentication to AWS IAM Users](http://aws.amazon.com/blogs/security/how-to-delegate-management-of-multi-factor-authentication-to-aws-iam-users/) on the AWS Security Blog\.

## 1\.12 – Ensure credentials unused for 45 days or greater are disabled<a name="securityhub-cis1.4-controls-1.12"></a>

**Severity:** Medium

**AWS Config rule: **[https://docs.aws.amazon.com/config/latest/developerguide/iam-user-unused-credentials-check.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-user-unused-credentials-check.html)

**Schedule type:** Periodic

This control checks whether your IAM users have passwords or active access keys that have not been used for 45 days or more\. To do so, it checks whether the `maxCredentialUsageAge` parameter of the AWS Config rule is equal to 45 or more\.

IAM users can access AWS resources using different types of credentials, such as passwords or access keys\.

CIS recommends that you remove or deactivate all credentials that have been unused for 45 days or more\. Disabling or removing unnecessary credentials reduces the window of opportunity for credentials associated with a compromised or abandoned account to be used\.

The AWS Config rule for this control uses the [https://docs.aws.amazon.com/IAM/latest/APIReference/API_GetCredentialReport.html](https://docs.aws.amazon.com/IAM/latest/APIReference/API_GetCredentialReport.html) and [https://docs.aws.amazon.com/IAM/latest/APIReference/API_GenerateCredentialReport.html](https://docs.aws.amazon.com/IAM/latest/APIReference/API_GenerateCredentialReport.html) API operations, which are only updated every four hours\. Changes to IAM users can take up to four hours to be visible to this control\.

**Note**  
AWS Config should be enabled in all Regions in which you use Security Hub\. However, you can enable recording of global resources in a single Region\. If you only record global resources in a single Region, then you can disable this control in all Regions except the Region where you record global resources\. 

### Remediation<a name="cis1.4-1.12-remediation"></a>

To get some of the information that you need to monitor accounts for dated credentials, use the IAM console\. For example, when you view users in your account, there is a column for **Access key age**, **Password age**, and **Last activity**\. If the value in any of these columns is greater than 45 days, make the credentials for those users inactive\.

You can also use credential reports to monitor user accounts and identify those with no activity for 45 or more days\. You can download credential reports in \.csv format from the IAM console\. For more information about credential reports, see [Getting credential reports for your AWS account](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_getting-report.html#getting-credential-reports-console) in the *IAM User Guide*\.

After you identify the inactive accounts or unused credentials, use the following steps to disable them\.

**To disable credentials for inactive accounts**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Users**\.

1. Choose the name of the user that has credentials over 45 days old\.

1. Choose **Security credentials**\.

1. For each sign\-in credential and access key that hasn't been used in at least 45 days, choose **Make inactive**\.

## 1\.14 – Ensure access keys are rotated every 90 days or less<a name="securityhub-cis1.4-controls-1.14"></a>

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/access-keys-rotated.html](https://docs.aws.amazon.com/config/latest/developerguide/access-keys-rotated.html)

**Schedule type:** Periodic

Access keys consist of an access key ID and secret access key, which are used to sign programmatic requests that you make to AWS\. AWS users need their own access keys to make programmatic calls to AWS from the AWS Command Line Interface \(AWS CLI\), Tools for Windows PowerShell, the AWS SDKs, or direct HTTP calls using the APIs for individual AWS services\.

When you rotate access keys regularly, you reduce the chance that an access key is used that is associated with a compromised or terminated account\. Rotate access keys to ensure that data can't be accessed with an old key that might have been lost, cracked, or stolen\. 

**Note**  
This control is not supported in the Africa \(Cape Town\) or Europe \(Milan\) Regions\.

### Remediation<a name="cis1.4-1.14-remediation"></a>

**To ensure that access keys aren't more than 90 days old**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Users**\.

1. For each user that shows an **Access key age** that is greater than 90 days, choose the **User name** to open the settings for that user\.

1. Choose **Security credentials**\.

1. To create a new key for the user:

   1. Choose **Create access key**\.

   1. To save the key content, either download the secret access key, or choose **Show** and then copy it from the page\.

   1. Store the key in a secure location to provide to the user\.

   1. Choose **Close**\.

1. Update all applications that were using the previous key to use the new key\.

1. For the previous key, choose **Make inactive** to make the access key inactive\. Now the user can't make requests using that key\.

1. Confirm that all applications work as expected with the new key\.

1. After confirming that all applications work with the new key, delete the previous key\. After you delete the access key, you can't recover it\.

   To delete the previous key, choose the **X** at the end of the row and then choose **Delete**\.

## 1\.16 – Ensure IAM policies that allow full "\*:\*" administrative privileges are not attached<a name="securityhub-cis1.4-controls-1.16"></a>

**Severity:** High

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-no-statements-with-admin-access.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-no-statements-with-admin-access.html)

**Schedule type:** Change triggered

This control checks whether the default version of IAM policies \(also known as customer managed policies\) has administrator access by including a statement with `"Effect": "Allow"` with `"Action": "*"` over `"Resource": "*"`\. This control also has the `excludePermissionBoundaryPolicy` parameter set to `true` to exclude permission boundary policies\. The control fails if you have IAM policies with such a statement\.

The control only checks the customer managed policies that you create\. It does not check inline and AWS managed policies\.

IAM policies define a set of privileges granted to users, groups, or roles\. It's recommended and considered a standard security advice to grant least privilege—that is, granting only the permissions required to perform a task\. Determine what users need to do and then craft policies that let the users perform only those tasks, instead of allowing full administrative privileges\.

It's more secure to start with a minimum set of permissions and grant additional permissions as necessary, rather than starting with permissions that are too lenient and then trying to tighten them later\. Providing full administrative privileges instead of restricting to the minimum set of permissions that the user is required to do exposes the resources to potentially unwanted actions\.

**Note**  
AWS Config should be enabled in all Regions in which you use Security Hub\. However, you can enable recording of global resources in a single Region\. If you only record global resources in a single Region, then you can disable this control in all Regions except the Region where you record global resources\.

### Remediation<a name="cis1.4-1.16-remediation"></a>

**To modify an IAM policy**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. Choose **Policies**\.

1. Select the radio button next to the policy to remove\.

1. From the **Policy actions** drop\-down menu, choose **Detach**\.

1. On the **Detach policy** page, select the radio button next to each user to detach the policy from and then choose **Detach policy**\.

Confirm that the user that you detached the policy from can still access AWS services and resources as expected\.

## 1\.17 \- Ensure a support role has been created to manage incidents with AWS Support<a name="securityhub-cis1.4-controls-1.17"></a>

**Severity:** Low

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-in-use.html](https://docs.aws.amazon.com/config/latest/developerguide/iam-policy-in-use.html)

**Schedule type:** Periodic

AWS provides a support center that can be used for incident notification and response, as well as technical support and customer services\.

Create an IAM role to allow authorized users to manage incidents with AWS Support\. By implementing least privilege for access control, an IAM role will require an appropriate IAM policy to allow support center access in order to manage incidents with AWS Support\.

**Note**  
This control is not supported in the following Regions\.  
Africa \(Cape Town\)
Asia Pacific \(Osaka\)
 Europe \(Milan\)

### Remediation<a name="cis1.4-1.17-remediation"></a>

To remediate this issue, create a role to allow authorized users to manage AWS Support incidents\.

**To create the role to use for AWS Support access**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the IAM navigation pane, choose **Roles**, then choose **Create role**\.

1. For **Role type**, choose the **Another AWS account**\.

1. For **Account ID**, enter the AWS account ID of the AWS account to which you want to grant access to your resources\.

   If the users or groups that will assume this role are in the same account, then enter the local account number\.
**Note**  
The administrator of the specified account can grant permission to assume this role to any IAM user in that account\. To do this, the administrator attaches a policy to the user or a group that grants permission for the `sts:AssumeRole` action\. In that policy, the resource must be the role ARN\.

1. Choose **Next: Permissions**\.

1. Search for the managed policy `AWSSupportAccess`\.

1. Select the check box for the `AWSSupportAccess` managed policy\.

1. Choose **Next: Tags**\.

1. \(Optional\) To add metadata to the role, attach tags as key–value pairs\.

   For more information about using tags in IAM, see [Tagging IAM users and roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_tags.html) in the *IAM User Guide*\.

1. Choose **Next: Review**\.

1. For **Role name**, enter a name for your role\.

   Role names must be unique within your AWS account\. They are not case sensitive\.

1. \(Optional\) For **Role description**, enter a description for the new role\.

1. Review the role, then choose **Create role**\.

## 2\.1\.1 – Ensure all S3 buckets employ encryption\-at\-rest<a name="securityhub-cis1.4-controls-2.1.1"></a>

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-server-side-encryption-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-server-side-encryption-enabled.html)

**Schedule type:** Change triggered

This control checks that your S3 bucket either has Amazon S3 default encryption enabled or that the S3 bucket policy explicitly denies put\-object requests without server\-side encryption\.

For an added layer of security for your sensitive data in S3 buckets, you should configure your buckets with server\-side encryption to protect your data at rest\. Amazon S3 encrypts each object with a unique key\. As an additional safeguard, Amazon S3 encrypts the key itself with a root key that it rotates regularly\. Amazon S3 server\-side encryption uses one of the strongest block ciphers available to encrypt your data, 256\-bit Advanced Encryption Standard \(AES\-256\)\.

To learn more, see [Protecting data using server\-side encryption with Amazon S3\-managed encryption keys \(SSE\-S3\)](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html) in the *Amazon Simple Storage Service User Guide*\.

### Remediation<a name="cis1.4-2.1.1-remediation"></a>

To remediate this issue, update your S3 bucket to enable default encryption\.

**To enable default encryption on an S3 bucket**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. In the left navigation pane, choose **Buckets**\.

1. Choose the S3 bucket from the list\.

1. Choose **Properties**\.

1. Choose **Default encryption**\.

1. For the encryption, choose either **AES\-256** or **AWS\-KMS**\.
   + Choose **AES\-256** to use keys that are managed by Amazon S3 for default encryption\. For more information about using Amazon S3 server\-side encryption to encrypt your data, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingServerSideEncryption.html)\.
   + Choose **AWS\-KMS** to use keys that are managed by AWS KMS for default encryption\. Then choose a root key from the list of the AWS KMS root keys that you have created\.

     Enter the Amazon Resource Name \(ARN\) of the AWS KMS key to use\. You can find the ARN for your KMS key in the IAM console, under **Encryption keys**\. Or, you can choose a key name from the drop\-down list\.
**Important**  
If you use the AWS KMS option for your default encryption configuration, you are subject to the RPS \(requests per second\) quotas of AWS KMS\. For more information about AWS KMS quotas and how to request a quota increase, see the [https://docs.aws.amazon.com/kms/latest/developerguide/limits.html](https://docs.aws.amazon.com/kms/latest/developerguide/limits.html)\.

     For more information about creating an KMS key, see the [https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html](https://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html)\.

     For more information about using AWS KMS with Amazon S3, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingKMSEncryption.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingKMSEncryption.html)\.

   When enabling default encryption, you might need to update your bucket policy\. For more information about moving from bucket policies to default encryption, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html#bucket-encryption-update-bucket-policy](https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html#bucket-encryption-update-bucket-policy)\.

1. Choose **Save**\.

For more information about default S3 bucket encryption, see the [https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html](https://docs.aws.amazon.com/AmazonS3/latest/dev/bucket-encryption.html)\.

## 2\.1\.2 – Ensure S3 Bucket Policy is set to deny HTTP requests<a name="securityhub-cis1.4-controls-2.1.2"></a>

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-ssl-requests-only.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-ssl-requests-only.html)

**Schedule type:** Change triggered

This control checks whether S3 buckets have policies that require requests to use Secure Socket Layer \(SSL\)\.

S3 buckets should have policies that require all requests \(`Action: S3:*`\) to only accept transmission of data over HTTPS in the S3 resource policy, indicated by the condition key `aws:SecureTransport`\.

### Remediation<a name="cis1.4-2.1.2-remediation"></a>

To remediate this issue, update the permissions policy of the S3 bucket\.

**To configure an S3 bucket to deny nonsecure transport**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Navigate to the noncompliant bucket, then choose the bucket name\.

1. Choose **Permissions**, and then choose **Bucket Policy**\.

1. Add a similar policy statement to that in the policy below\. Replace `awsexamplebucket` with the name of the bucket you are modifying\.

   ```
   {
       "Id": "ExamplePolicy",
       "Version": "2012-10-17",
       "Statement": [
           {
               "Sid": "AllowSSLRequestsOnly",
               "Action": "s3:*",
               "Effect": "Deny",
               "Resource": [
                   "arn:aws:s3:::awsexamplebucket",
                   "arn:aws:s3:::awsexamplebucket/*"
               ],
               "Condition": {
                   "Bool": {
                        "aws:SecureTransport": "false"
                   }
               },
              "Principal": "*"
           }
       ]
   }
   ```

1. Choose **Save**\.

For more information, see the knowledge center article [What S3 bucket policy should I use to comply with the AWS Config rule s3\-bucket\-ssl\-requests\-only?](http://aws.amazon.com/premiumsupport/knowledge-center/s3-bucket-policy-for-config-rule/)\.

## 2\.1\.5\.1 – S3 Block Public Access setting should be enabled<a name="securityhub-cis1.4-controls-2.1.5.1"></a>

**Important**  
You must pass controls 2\.1\.5\.1 and 2\.1\.5\.2 to satisfy CIS AWS Foundations Benchmark requirement ** 2\.1\.5 – Ensure that S3 Buckets are configured with 'Block public access \(bucket settings\)\.'**

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-account-level-public-access-blocks-periodic.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-account-level-public-access-blocks-periodic.html) 

**Schedule type:** Periodic

**Parameters:** 
+ `ignorePublicAcls`: `true`
+ `blockPublicPolicy`: `true`
+ `blockPublicAcls`: `true`
+ `restrictPublicBuckets`: `true`

This control checks whether the following Amazon S3 public access block settings are configured at the account level:
+ `ignorePublicAcls`: `true`
+ `blockPublicPolicy`: `true`
+ `blockPublicAcls`: `true`
+ `restrictPublicBuckets`: `true`

The control passes if all of the public access block settings are set to `true`\.

The control fails if any of the settings are set to `false`, or if any of the settings are not configured\.

Amazon S3 public access block is designed to provide controls across an entire AWS account or at the individual S3 bucket level to ensure that objects never have public access\. Public access is granted to buckets and objects through access control lists \(ACLs\), bucket policies, or both\.

Unless you intend to have your S3 buckets be publicly accessible, you should configure the account level Amazon S3 Block Public Access feature\.

To learn more, see [Using Amazon S3 Block Public Access](https://docs.aws.amazon.com/AmazonS3/latest/dev/access-control-block-public-access.html) in the *Amazon Simple Storage Service User Guide*\.

**Note**  
This control is not supported in the following Regions:  
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="cis1.4-2.1.5.1-remediation"></a>

To remediate this issue, enable Amazon S3 Block Public Access\.

**To enable Amazon S3 Block Public Access**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose **Block public access \(account settings\)**\.

1. Choose **Edit**\.

1. Select **Block *all* public access**\.

1. Choose **Save changes**\.

For more information, see [Using Amazon S3 block public access](https://docs.aws.amazon.com/AmazonS3/latest/dev/access-control-block-public-access.html) in the *Amazon Simple Storage Service User Guide*\.

## 2\.1\.5\.2 – S3 Block Public Access setting should be enabled at the bucket level<a name="securityhub-cis1.4-controls-2.1.5.2"></a>

**Important**  
You must pass controls 2\.1\.5\.1 and 2\.1\.5\.2 to satisfy CIS AWS Foundations Benchmark requirement **2\.1\.5 – Ensure that S3 Buckets are configured with 'Block public access \(bucket settings\)\.'**

**Severity:** High

**Resource type:** `AWS::S3::Bucket`

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-level-public-access-prohibited.html](https://docs.aws.amazon.com/config/latest/developerguide/s3-bucket-level-public-access-prohibited.html)

**Schedule type:** Change triggered

**Parameters:**
+ `excludedPublicBuckets` \(Optional\) – A comma\-separated list of known allowed public S3 bucket names\.

This control checks whether S3 buckets have bucket\-level public access blocks applied\. This control fails is if any of the following settings are set to `false`:
+ `ignorePublicAcls`
+ `blockPublicPolicy`
+ `blockPublicAcls`
+ `restrictPublicBuckets`

Block Public Access at the S3 bucket level provides controls to ensure that objects never have public access\. Public access is granted to buckets and objects through access control lists \(ACLs\), bucket policies, or both\.

Unless you intend to have your S3 buckets publicly accessible, you should configure the bucket level Amazon S3 Block Public Access feature\.

**Note**  
This control is not supported in the following Regions:  
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="cis1.4-2.1.5.2-remediation"></a>

For information on how to remove public access at a bucket level, see [Blocking public access to your Amazon S3 storage](https://docs.aws.amazon.com/AmazonS3/latest/dev/access-control-block-public-access.html) in the *Amazon S3 User Guide*\.

## 2\.2\.1 – Ensure EBS volume encryption is enabled<a name="securityhub-cis1.4-controls-2.2.1"></a>

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/ec2-ebs-encryption-by-default.html](https://docs.aws.amazon.com/config/latest/developerguide/ec2-ebs-encryption-by-default.html)

**Schedule type:** Periodic

This control checks whether account\-level encryption is enabled by default for Amazon Elastic Block Store\(Amazon EBS\)\. The control fails if the account level encryption is not enabled\. 

When encryption is enabled for your account, Amazon EBS volumes and snapshot copies are encrypted at rest\. This adds an additional layer of protection for your data\. For more information, see [Encryption by default](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSEncryption.html#encryption-by-default) in the *Amazon EC2 User Guide for Linux Instances*\.

Note that following instance types do not support encryption: R1, C1, and M1\.

**Note**  
This control is not supported in the Asia Pacific \(Jakarta\) or Asia Pacific \(Osaka\) Regions\.

### Remediation<a name="cis1.4-2.2.1-remediation"></a>

You can use the Amazon EC2 console to enable default encryption for Amazon EBS volumes\.

**To configure the default encryption for Amazon EBS encryption for a Region**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. From the navigation pane, select **EC2 Dashboard**\.

1. In the upper\-right corner of the page, choose **Account Attributes, EBS encryption**\.

1. Choose **Manage**\.

1. Select **Enable**\. You can keep the AWS managed key with the alias `alias/aws/ebs` created on your behalf as the default encryption key, or choose a symmetric customer managed key\.

1. Choose **Update EBS encryption**\.

## 2\.3\.1 – Ensure that encryption is enabled for RDS instances<a name="securityhub-cis1.4-controls-2.3.1"></a>

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/rds-storage-encrypted.html](https://docs.aws.amazon.com/config/latest/developerguide/rds-storage-encrypted.html)

**Schedule type:** Change triggered

This control checks whether storage encryption is enabled for your Amazon RDS DB instances\.

This control is intended for RDS DB instances\. However, it can also generate findings for Aurora DB instances, Neptune DB instances, and Amazon DocumentDB clusters\. If these findings are not useful, then you can suppress them\.

For an added layer of security for your sensitive data in RDS DB instances, you should configure your RDS DB instances to be encrypted at rest\. To encrypt your RDS DB instances and snapshots at rest, enable the encryption option for your RDS DB instances\. Data that is encrypted at rest includes the underlying storage for DB instances, its automated backups, read replicas, and snapshots\. 

RDS encrypted DB instances use the open standard AES\-256 encryption algorithm to encrypt your data on the server that hosts your RDS DB instances\. After your data is encrypted, Amazon RDS handles authentication of access and decryption of your data transparently with a minimal impact on performance\. You do not need to modify your database client applications to use encryption\. 

Amazon RDS encryption is currently available for all database engines and storage types\. Amazon RDS encryption is available for most DB instance classes\. To learn about DB instance classes that do not support Amazon RDS encryption, see [Encrypting Amazon RDS resources](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.Encryption.html) in the *Amazon RDS User Guide*\.

### Remediation<a name="cis1.4-2.3.1-remediation"></a>

For information about encrypting DB instances in Amazon RDS, see [Encrypting Amazon RDS resources](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.Encryption.html) in the *Amazon RDS User Guide*\.

## 3\.1 – Ensure CloudTrail is enabled in all Regions<a name="securityhub-cis1.4-controls-3.1"></a>

**Severity:** High

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/multi-region-cloudtrail-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/multi-region-cloudtrail-enabled.html)

**Schedule type:** Periodic

This control checks that there is at least one multi\-Region CloudTrail trail\. It also checks that the `ExcludeManagementEventSources` parameter is empty for at least one of those trails\.

CloudTrail is a service that records AWS API calls for your account and delivers log files to you\. The recorded information includes the identity of the API caller, the time of the API call, the source IP address of the API caller, the request parameters, and the response elements returned by the AWS service\. CloudTrail provides a history of AWS API calls for an account, including API calls made via the AWS Management Console, AWS SDKs, command\-line tools, and higher\-level AWS services \(such as AWS CloudFormation\)\.

The AWS API call history produced by CloudTrail enables security analysis, resource change tracking, and compliance auditing\. Additionally:
+ Ensuring that a multi\-Region trail exists ensures that unexpected activity occurring in otherwise unused Regions is detected
+ Ensuring that a multi\-Region trail exists ensures that Global Service Logging is enabled for a trail by default to capture recording of events generated on AWS global services
+ For a multi\-Region trail, ensuring that management events configured for all type of Read/Writes ensures recording of management operations that are performed on all resources in an AWS account

By default, CloudTrail trails that are created using the AWS Management Console are multi\-Region trails\.

**Note**  
If you use the Security Hub integration with AWS Organizations, and a member account does not own any CloudTrail trails that match the conditions described in this control, Security Hub will not generate findings for the member account for CIS v1\.4\.0 4\.x controls and [1\.7 – Eliminate use of the 'root user for administrative and daily tasks](#securityhub-cis1.4-controls-1.7)\.

### Remediation<a name="cis1.4-3.1-remediation"></a>

**To create a new trail in CloudTrail**

1. Sign in to the AWS Management Console and open the CloudTrail console at [https://console\.aws\.amazon\.com/cloudtrail/](https://console.aws.amazon.com/cloudtrail/)\.

1. If you haven't used CloudTrail before, choose **Get Started Now**\.

1. Choose **Trails** and then choose **Create trail**\.

1. Enter a name for the trail\.

1. Under **Storage location**, do one of the following:
   + To create a new S3 bucket for CloudTrail logs, choose **Create new S3 bucket** and then enter a name for the bucket\.
   + Choose **Use existing S3 bucket** and then select the bucket to use\.

1. Choose **Additional settings** and, for **Log file validation**, choose **Enabled** to pass [3\.2\. – Ensure CloudTrail log file validation is enabled ](#securityhub-cis1.4-controls-3.2) \.

1. To pass [3\.4 – Ensure CloudTrail trails are integrated with CloudWatch logs](#securityhub-cis1.4-controls-3.4), you must enable CloudWatch Logs\.

   1. Under CloudWatch Logs, select the **Enabled** check box\.

   1. For **Log group**, do one of the following:
      + To use an existing log group, choose **Existing** and then enter the name of the log group to use\.
      + To create a new log group, choose **New** and then enter a name for the log group to create\.

   1. For **IAM role**, do one of the following:
      + To use an existing role, choose **Existing** and then choose the role from the drop\-down list\.
      + To create a new role, choose **New** and then enter a name for the role to create\. The new role is assigned a policy that grants the necessary permissions\.

        To view the permissions granted to the role, expand the **Policy document**\.

1. Choose **Create**\.

**To update an existing trail in CloudTrail**

1. Sign in to the AWS Management Console and open the CloudTrail console at [https://console\.aws\.amazon\.com/cloudtrail/](https://console.aws.amazon.com/cloudtrail/)\.

1. Choose **Trails**\.

1. Choose the name of the trail in the **Name** column\.

1. Update the trail configuration as needed\.

   To update the configuration in a particular section, do the following:

   1. Choose **Edit** for that section\.

   1. Make the required updates to the configuration\.

   1. Choose **Save changes**\.

## 3\.2\. – Ensure CloudTrail log file validation is enabled<a name="securityhub-cis1.4-controls-3.2"></a>

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-log-file-validation-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-log-file-validation-enabled.html)

**Schedule type:** Periodic

CloudTrail log file validation creates a digitally signed digest file containing a hash of each log that CloudTrail writes to S3\. You can use these digest files to determine whether a log file was changed, deleted, or unchanged after CloudTrail delivered the log\.

CIS recommends that you enable file validation on all trails\. Enabling log file validation provides additional integrity checking of CloudTrail logs\.

### Remediation<a name="cis1.4-3.2-remediation"></a>

**To enable CloudTrail log file validation**

1. Open the CloudTrail console at [https://console\.aws\.amazon\.com/cloudtrail/](https://console.aws.amazon.com/cloudtrail/)\.

1. Choose **Trails**\.

1. Choose the name of a trail to edit in the **Name** column\.

1. Under **General details**, choose **Edit**\.

1. Under **Additional settings**, for **Log file validation**, select **Enabled**\.

1. Choose **Save**\.

## 3\.3 – Ensure the S3 bucket used to store CloudTrail logs is not publicly accessible<a name="securityhub-cis1.4-controls-3.3"></a>

**Severity:** Critical

**AWS Config rule:** None

**Schedule type:** Periodic and change triggered

CloudTrail logs a record of every API call made in your account\. These log files are stored in an S3 bucket\. CIS recommends that the S3 bucket policy, or access control list \(ACL\), applied to the S3 bucket that CloudTrail logs to prevents public access to the CloudTrail logs\. Allowing public access to CloudTrail log content might aid an adversary in identifying weaknesses in the affected account's use or configuration\.

To run this check, Security Hub first uses custom logic to look for the S3 bucket where your CloudTrail logs are stored\. It then uses the AWS Config managed rules to check that bucket is publicly accessible\.

If you aggregate your logs into a single centralized S3 bucket, then Security Hub only runs the check against the account and Region where the centralized S3 bucket is located\. For other accounts and Regions, the control status is **No data**\.

If the bucket is publicly accessible, the check generates a failed finding\.

### Remediation<a name="cis1.4-3.3-remediation"></a>

**To remove public access for an Amazon S3 bucket**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose the name of the bucket where your CloudTrail are stored\.

1. Choose **Permissions** and then choose **Public access settings**\.

1. Choose **Edit**, select all four options, and then choose **Save**\.

1. If prompted, enter **confirm** and then choose **Confirm**\.

## 3\.4 – Ensure CloudTrail trails are integrated with CloudWatch logs<a name="securityhub-cis1.4-controls-3.4"></a>

**Severity:** Low

**AWS Config rule: **[https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-cloud-watch-logs-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-cloud-watch-logs-enabled.html)

**Schedule type:** Periodic

CloudTrail is a web service that records AWS API calls made in a given account\. The recorded information includes the identity of the API caller, the time of the API call, the source IP address of the API caller, the request parameters, and the response elements returned by the AWS service\.

CloudTrail uses Amazon S3 for log file storage and delivery, so log files are stored durably\. In addition to capturing CloudTrail logs in a specified Amazon S3 bucket for long\-term analysis, you can perform real\-time analysis by configuring CloudTrail to send logs to CloudWatch Logs\.

For a trail that is enabled in all Regions in an account, CloudTrail sends log files from all those Regions to a CloudWatch Logs log group\.

CIS recommends that you send CloudTrail logs to CloudWatch Logs\.

**Note**  
 The intent of this recommendation is to ensure that account activity is being captured, monitored, and appropriately alarmed on\. CloudWatch Logs is a native way to accomplish this using AWS services but doesn't preclude the use of an alternate solution\.

Sending CloudTrail logs to CloudWatch Logs facilitates real\-time and historic activity logging based on user, API, resource, and IP address\. It provides the opportunity to establish alarms and notifications for anomalous or sensitivity account activity\.

### Remediation<a name="cis1.4-3.4-remediation"></a>

**To ensure that CloudTrail trails are integrated with CloudWatch Logs**

1. Open the CloudTrail console at [https://console\.aws\.amazon\.com/cloudtrail/](https://console.aws.amazon.com/cloudtrail/)\.

1. Choose **Trails**\.

1. Choose a trail that there is no value for in the **CloudWatch Logs Log group** column\.

1. Scroll down to the **CloudWatch Logs** section and then choose **Edit**\.

1. Select the **Enabled** check box\.

1. For **Log group**, do one of the following:
   + To use an existing log group, choose **Existing** and then enter the name of the log group to use\.
   + To create a new log group, choose **New** and then enter a name for the log group to create\.

1. For **IAM role**, do one of the following:
   + To use an existing role, choose **Existing** and then choose the role from the drop\-down list\.
   + To create a new role, choose **New** and then enter a name for the role to create\. The new role is assigned a policy that grants the necessary permissions\.

     To view the permissions granted to the role, expand the **Policy document**\.

1. Choose **Save changes**\.

For more information, see [Configuring CloudWatch Logs monitoring with the console](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/send-cloudtrail-events-to-cloudwatch-logs.html#send-cloudtrail-events-to-cloudwatch-logs-console) in the *AWS CloudTrail User Guide*\.

## 3\.5 – Ensure AWS Config is enabled in all Regions<a name="securityhub-cis1.4-controls-3.5"></a>

**Severity:** Medium

**AWS Config rule:** None

**Schedule type:** Periodic

AWS Config is a web service that performs configuration management of supported AWS resources in your account and delivers log files to you\. The recorded information includes the configuration item \(AWS resource\), relationships between configuration items \(AWS resources\), and any configuration changes between resources\.

CIS recommends that you enable AWS Config in all Regions\. The AWS configuration item history that AWS Config captures enables security analysis, resource change tracking, and compliance auditing\.

**Note**  
CIS 2\.5 requires that AWS Config is enabled in all Regions in which you use Security Hub\.  
Because Security Hub is a regional service, the check performed for this control checks only the current Region for the account\. It does not check all Regions\.  
You also must record global resources so that security checks against global resources can be checked in each Region\. If you only record global resources in a single Region, then you can disable this control in all Regions except the Region where you record global resources\.

To run this check, Security Hub performs custom logic to perform the audit steps prescribed for it in the [CIS AWS Foundations Benchmark v1\.4\.0](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:2e5fec5c-5e99-4fb5-b08d-bb46b14754c1#pageNum=1)\. Security Hub also requires that global resources are recorded in each Region, because Security Hub is a regional service and performs its security checks on a Region\-by\-Region basis\.

### Remediation<a name="cis1.4-3.5-remediation"></a>

**To configure AWS Config settings**

1. Open the AWS Config console at [https://console\.aws\.amazon\.com/config/](https://console.aws.amazon.com/config/)\.

1. Select the Region to configure AWS Config in\.

1. If you haven't used AWS Config before, see [Getting Started](https://docs.aws.amazon.com/config/latest/developerguide/getting-started.html) in the *AWS Config Developer Guide*\.

1. Navigate to the Settings page from the menu, and do the following:
   + Choose **Edit**\.
   + Under **Resource types to record**, select **Record all resources supported in this region** and **Include global resources \(e\.g\., AWS IAM resources\)**\.
   + Under **Data retention period**, choose the default retention period for AWS Config data, or specify a custom retention period\.
   + Under **AWS Config role**, either choose **Create AWS Config service\-linked role** or choose **Choose a role from your account** and then select the role to use\.
   + Under **Amazon S3 bucket**, specify the bucket to use or create a bucket and optionally include a prefix\.
   + Under **Amazon SNS topic**, select an Amazon SNS topic from your account or create one\. For more information about Amazon SNS, see the [https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html)\.

1. Choose **Save**\.

For more information about using AWS Config from the AWS Command Line Interface, see [Turning on AWS Config](https://docs.aws.amazon.com/config/latest/developerguide/gs-cli-subscribe.html) in the *AWS Config Developer Guide*\.

You can also use an AWS CloudFormation template to automate this process\. For more information, see the [AWS CloudFormation StackSets sample template](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/stacksets-sampletemplates.html) in the *AWS CloudFormation User Guide*\.

## 3\.6 – Ensure S3 bucket access logging is enabled on the CloudTrail S3 bucket<a name="securityhub-cis1.4-controls-3.6"></a>

**Severity:** Low

**AWS Config rule:** None

**Schedule type:** Periodic

S3 bucket access logging generates a log that contains access records for each request made to your S3 bucket\. An access log record contains details about the request, such as the request type, the resources specified in the request worked, and the time and date the request was processed\.

CIS recommends that you enable bucket access logging on the CloudTrail S3 bucket\.

By enabling S3 bucket logging on target S3 buckets, you can capture all events that might affect objects in a target bucket\. Configuring logs to be placed in a separate bucket enables access to log information, which can be useful in security and incident response workflows\.

To run this check, Security Hub first uses custom logic to look for the bucket where your CloudTrail logs are stored and then uses the AWS Config managed rule to check if logging is enabled\.

If you aggregate your logs into a single centralized S3 bucket, then Security Hub only runs the check against the account and Region where the centralized S3 bucket is located\. For other accounts and Regions, the control status is **No data**\.

If the bucket is publicly accessible, the check generates a failed finding\.

### Remediation<a name="cis1.4-3.6-remediation"></a>

**To enable S3 bucket access logging**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose the bucket used for CloudTrail\.

1. Choose **Properties**\.

1. Choose **Server access logging**, then choose **Enable logging**\.

1. Select a bucket from the **Target bucket** list, and optionally enter a prefix\.

1. Choose **Save**\.

## 3\.7 – Ensure CloudTrail logs are encrypted at rest using AWS KMS keys<a name="securityhub-cis1.4-controls-3.7"></a>

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-encryption-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cloud-trail-encryption-enabled.html)

**Schedule type:** Periodic

CloudTrail is a web service that records AWS API calls for an account and makes those logs available to users and resources in accordance with IAM policies\. AWS Key Management Service \(AWS KMS\) is a managed service that helps create and control the encryption keys used to encrypt account data, and uses hardware security modules \(HSMs\) to protect the security of encryption keys\.

You can configure CloudTrail logs to leverage server\-side encryption \(SSE\) and KMS keys to further protect CloudTrail logs\.

CIS recommends that you configure CloudTrail to use SSE\-KMS\.

Configuring CloudTrail to use SSE\-KMS provides additional confidentiality controls on log data because a given user must have S3 read permission on the corresponding log bucket and must be granted decrypt permission by the KMS key policy\.

### Remediation<a name="cis1.4-3.7-remediation"></a>

**To enable encryption for CloudTrail logs**

1. Open the CloudTrail console at [https://console\.aws\.amazon\.com/cloudtrail/](https://console.aws.amazon.com/cloudtrail/)\.

1. Choose **Trails**\.

1. Choose the trail to update\.

1. Under **Storage location**, choose the pencil icon to edit the settings\.

1. For **Encrypt log files with SSE\-KMS**, choose **Yes**\.

1. For **Create a new KMS key**, do one of the following:
   + To create a key, choose **Yes** and then enter an alias for the key in the **KMS key** field\. The key is created in the same Region as the bucket\.
   + To use an existing key, choose **No** and then select the key from the **KMS key** list\.
**Note**  
The KMS key and S3 bucket must be in the same Region\.

1. Choose **Save**\.

You might need to modify the policy for CloudTrail to successfully interact with your KMS key\. For more information, see [Encrypting CloudTrail log files with AWS KMS–Managed Keys \(SSE\-KMS\)](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/encrypting-cloudtrail-log-files-with-aws-kms.html?icmpid=docs_cloudtrail_console) in the *AWS CloudTrail User Guide*\.

## 3\.8 – Ensure rotation for customer\-created KMS keys is enabled<a name="securityhub-cis1.4-controls-3.8"></a>

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/cmk-backing-key-rotation-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/cmk-backing-key-rotation-enabled.html)

**Schedule type:** Periodic

AWS KMS enables customers to rotate the backing key, which is key material stored in AWS KMS and is tied to the key ID of the KMS key\. It's the backing key that is used to perform cryptographic operations such as encryption and decryption\. Automated key rotation currently retains all previous backing keys so that decryption of encrypted data can take place transparently\.

CIS recommends that you enable KMS key rotation\. Rotating encryption keys helps reduce the potential impact of a compromised key because data encrypted with a new key can't be accessed with a previous key that might have been exposed\.

### Remediation<a name="cis1.4-3.8-remediation"></a>

**To enable KMS key rotation**

1. Open the AWS KMS console at [https://console\.aws\.amazon\.com/kms](https://console.aws.amazon.com/kms)\.

1. To change the AWS Region, use the Region selector in the upper\-right corner of the page\.

1. Choose **Customer managed keys**\.

1. Choose the alias of the key to update in the **Alias** column\.

1. Choose **Key rotation**\.

1. Select **Automatically rotate this KMS key every year** and then choose **Save**\.

## 3\.9 – Ensure VPC flow logging is enabled in all VPCs<a name="securityhub-cis1.4-controls-3.9"></a>

**Severity:** Medium

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/vpc-flow-logs-enabled.html](https://docs.aws.amazon.com/config/latest/developerguide/vpc-flow-logs-enabled.html)

**Schedule type:** Periodic

VPC flow logs is a feature of Amazon Virtual Private Cloud \(Amazon VPC\) that enables you to capture information about the IP traffic going to and from network interfaces in your VPC\. After you have created a flow log, you can view and retrieve its data in CloudWatch Logs\.

CIS recommends that you enable flow logging for packet rejects for VPCs\. Flow logs provide visibility into network traffic that traverses the VPC and can detect anomalous traffic or insight during security workflows\. 

### Remediation<a name="cis1.4-3.9-remediation"></a>

**To enable VPC flow logging**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. Choose **Your VPCs**\.

1. Select a VPC to update\.

1. Choose the **Flow Logs** tab in the bottom section of the page\.

1. Choose **Create flow log**\.

1. For **Filter**, choose **Reject**\.

1. For **Destination log group**, select the log group to use\.

1. For **IAM role**, select the IAM role to use\.

1. Choose **Create**\.

## 4\.4 – Ensure a log metric filter and alarm exist for IAM policy changes<a name="securityhub-cis1.4-controls-4.4"></a>

**Severity:** Low

**AWS Config rule:** None

**Schedule type:** Periodic

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\.

CIS recommends that you create a metric filter and alarm for changes made to IAM policies\. Monitoring these changes helps ensure that authentication and authorization controls remain intact\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 4\.4 in the [CIS AWS Foundations Benchmark v1\.4\.0](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:2e5fec5c-5e99-4fb5-b08d-bb46b14754c1#pageNum=1)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cis1.4-4.4-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

Note that the alarm checks for specific API operations by name\. One of these operations is `DeletePolicy`\. The alarm does not check that the call was issued from IAM\. Because of this, the alarm also is triggered when Auto Scaling calls `DeletePolicy`\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [3\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis1.4-controls-3.1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {($.eventName=DeleteGroupPolicy) || ($.eventName=DeleteRolePolicy) || ($.eventName=DeleteUserPolicy) || ($.eventName=PutGroupPolicy) || ($.eventName=PutRolePolicy) || ($.eventName=PutUserPolicy) || ($.eventName=CreatePolicy) || ($.eventName=DeletePolicy) || ($.eventName=CreatePolicyVersion) || ($.eventName=DeletePolicyVersion) || ($.eventName=AttachRolePolicy) || ($.eventName=DetachRolePolicy) || ($.eventName=AttachUserPolicy) || ($.eventName=DetachUserPolicy) || ($.eventName=AttachGroupPolicy) || ($.eventName=DetachGroupPolicy)}
      ```

   1. Choose **Next**\.

1. Under **Assign metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. Choose the **Metric filters** tab, then choose the metric filter that you just created\.

   To choose the metric filter, select the check box at the upper right\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Under **Metric**, for **Statistic**, choose **Average**\. For more information about the available statistics, see [Statistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Statistic) in the *Amazon CloudWatch User Guide*\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm\. For example, **CIS\-4\.4\-IAMPolicyChanges**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## 4\.5 – Ensure a log metric filter and alarm exist for CloudTrail configuration changes<a name="securityhub-cis1.4-controls-4.5"></a>

**Severity:** Low

**AWS Config rule:** None

**Schedule type:** Periodic

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\.

CIS recommends that you create a metric filter and alarm for changes to CloudTrail configuration settings\. Monitoring these changes helps ensure sustained visibility to activities in the account\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 4\.5 in the [CIS AWS Foundations Benchmark v1\.4\.0](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:2e5fec5c-5e99-4fb5-b08d-bb46b14754c1#pageNum=1)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cis1.4-4.5-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [3\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis1.4-controls-3.1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {($.eventName=CreateTrail) || ($.eventName=UpdateTrail) || ($.eventName=DeleteTrail) || ($.eventName=StartLogging) || ($.eventName=StopLogging)}
      ```

   1. Choose **Next**\.

1. Under **Assign metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. Choose the **Metric filters** tab, then choose the metric filter that you just created\.

   To choose the metric filter, select the check box at the upper right\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Under **Metric**, leave the default values\. For more information about the available statistics, see [Statistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Statistic) in the *Amazon CloudWatch User Guide*\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm\. For example, **CIS\-4\.5\-CloudTrailChanges**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## 4\.6 – Ensure a log metric filter and alarm exist for AWS Management Console authentication failures<a name="securityhub-cis1.4-controls-4.6"></a>

**Severity:** Low

**AWS Config rule:** None

**Schedule type:** Periodic

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\.

CIS recommends that you create a metric filter and alarm for failed console authentication attempts\. Monitoring failed console logins might decrease lead time to detect an attempt to brute\-force a credential, which might provide an indicator, such as source IP, that you can use in other event correlations\. 

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 4\.6 in the [CIS AWS Foundations Benchmark v1\.4\.0](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:2e5fec5c-5e99-4fb5-b08d-bb46b14754c1#pageNum=1)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cis1.4-4.6-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [3\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis1.4-controls-3.1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {($.eventName=ConsoleLogin) && ($.errorMessage="Failed authentication")}
      ```

   1. Choose **Next**\.

1. Under **Assign metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. Choose the **Metric filters** tab, then choose the metric filter that you just created\.

   To choose the metric filter, select the check box at the upper right\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Under **Metric**, leave the default values\. For more information about the available statistics, see [Statistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Statistic) in the *Amazon CloudWatch User Guide*\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm\. For example, **CIS\-4\.6\-ConsoleAuthenticationFailure**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## 4\.7 – Ensure a log metric filter and alarm exist for disabling or scheduled deletion of customer managed keys<a name="securityhub-cis1.4-controls-4.7"></a>

**Severity:** Low

**AWS Config rule:** None

**Schedule type:** Periodic

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\.

CIS recommends that you create a metric filter and alarm for customer managed keys that have changed state to disabled or scheduled deletion\. Data encrypted with disabled or deleted keys is no longer accessible\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 4\.7 in the [CIS AWS Foundations Benchmark v1\.4\.0](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:2e5fec5c-5e99-4fb5-b08d-bb46b14754c1#pageNum=1)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\. The control also fails if `ExcludeManagementEventSources` contains `kms.amazonaws.com`\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cis1.4-4.7-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [3\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis1.4-controls-3.1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {($.eventSource=kms.amazonaws.com) && (($.eventName=DisableKey) || ($.eventName=ScheduleKeyDeletion))}
      ```

   1. Choose **Next**\.

1. Under **Assign metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. Choose the **Metric filters** tab, then choose the metric filter that you just created\.

   To choose the metric filter, select the check box at the upper right\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Under **Metric**, leave the default values\. For more information about the available statistics, see [Statistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Statistic) in the *Amazon CloudWatch User Guide*\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm\. For example, **CIS\-4\.7\-DisableOrDeleteCMK**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## 4\.8 – Ensure a log metric filter and alarm exist for S3 bucket policy changes<a name="securityhub-cis1.4-controls-4.8"></a>

**Severity:** Low

**AWS Config rule:** None

**Schedule type:** Periodic

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\.

CIS recommends that you create a metric filter and alarm for changes to S3 bucket policies\. Monitoring these changes might reduce time to detect and correct permissive policies on sensitive S3 buckets\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 4\.8 in the [CIS AWS Foundations Benchmark v1\.4\.0](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:2e5fec5c-5e99-4fb5-b08d-bb46b14754c1#pageNum=1)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cis1.4-4.8-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [3\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis1.4-controls-3.1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {($.eventSource=s3.amazonaws.com) && (($.eventName=PutBucketAcl) || ($.eventName=PutBucketPolicy) || ($.eventName=PutBucketCors) || ($.eventName=PutBucketLifecycle) || ($.eventName=PutBucketReplication) || ($.eventName=DeleteBucketPolicy) || ($.eventName=DeleteBucketCors) || ($.eventName=DeleteBucketLifecycle) || ($.eventName=DeleteBucketReplication))}
      ```

   1. Choose **Next**\.

1. Under **Assign metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. Choose the **Metric filters** tab, then choose the metric filter that you just created\.

   To choose the metric filter, select the check box at the upper right\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Under **Metric**, for **Statistic**, choose **Average**\. For more information about the available statistics, see [Statistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Statistic) in the *Amazon CloudWatch User Guide*\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm\. For example, **CIS\-4\.8\-S3BucketPolicyChanges**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## 4\.9 – Ensure a log metric filter and alarm exist for AWS Config configuration changes<a name="securityhub-cis1.4-controls-4.9"></a>

**Severity:** Low

**AWS Config rule:** None

**Schedule type:** Periodic

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\.

CIS recommends that you create a metric filter and alarm for changes to AWS Config configuration settings\. Monitoring these changes helps ensure sustained visibility of configuration items in the account\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 4\.9 in the [CIS AWS Foundations Benchmark v1\.4\.0](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:2e5fec5c-5e99-4fb5-b08d-bb46b14754c1#pageNum=1)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cis1.4-4.9-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [3\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis1.4-controls-3.1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {($.eventSource=config.amazonaws.com) && (($.eventName=StopConfigurationRecorder) || ($.eventName=DeleteDeliveryChannel) || ($.eventName=PutDeliveryChannel) || ($.eventName=PutConfigurationRecorder))}
      ```

   1. Choose **Next**\.

1. Under **Assign metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. Choose the **Metric filters** tab, then choose the metric filter that you just created\.

   To choose the metric filter, select the check box at the upper right\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Under **Metric**, leave the default values\. For more information about the available statistics, see [Statistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Statistic) in the *Amazon CloudWatch User Guide*\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm\. For example, **CIS\-4\.9\-AWSConfigChanges**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## 4\.10 – Ensure a log metric filter and alarm exist for security group changes<a name="securityhub-cis1.4-controls-4.10"></a>

**Severity:** Low

**AWS Config rule:** None

**Schedule type:** Periodic

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. Security groups are a stateful packet filter that controls ingress and egress traffic in a VPC\.

CIS recommends that you create a metric filter and alarm for changes to security groups\. Monitoring these changes helps ensure that resources and services aren't unintentionally exposed\. 

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 4\.10 in the [CIS AWS Foundations Benchmark v1\.4\.0](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:2e5fec5c-5e99-4fb5-b08d-bb46b14754c1#pageNum=1)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cis1.4-4.10-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [3\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis1.4-controls-3.1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {($.eventName=AuthorizeSecurityGroupIngress) || ($.eventName=AuthorizeSecurityGroupEgress) || ($.eventName=RevokeSecurityGroupIngress) || ($.eventName=RevokeSecurityGroupEgress) || ($.eventName=CreateSecurityGroup) || ($.eventName=DeleteSecurityGroup)}
      ```

   1. Choose **Next**\.

1. Under **Assign metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. Choose the **Metric filters** tab, then choose the metric filter that you just created\.

   To choose the metric filter, select the check box at the upper right\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Under **Metric**, leave the default values\. For more information about the available statistics, see [Statistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Statistic) in the *Amazon CloudWatch User Guide*\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm\. For example, **CIS\-4\.10\-SecurityGroupChanges**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## 4\.11 – Ensure a log metric filter and alarm exist for changes to Network Access Control Lists \(NACL\)<a name="securityhub-cis1.4-controls-4.11"></a>

**Severity:** Low

**AWS Config rule:** None

**Schedule type:** Periodic

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. NACLs are used as a stateless packet filter to control ingress and egress traffic for subnets in a VPC\.

CIS recommends that you create a metric filter and alarm for changes to NACLs\. Monitoring these changes helps ensure that AWS resources and services aren't unintentionally exposed\. 

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 4\.11 in the [CIS AWS Foundations Benchmark v1\.4\.0](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:2e5fec5c-5e99-4fb5-b08d-bb46b14754c1#pageNum=1)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cis1.4-4.11-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [3\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis1.4-controls-3.1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {($.eventName=CreateNetworkAcl) || ($.eventName=CreateNetworkAclEntry) || ($.eventName=DeleteNetworkAcl) || ($.eventName=DeleteNetworkAclEntry) || ($.eventName=ReplaceNetworkAclEntry) || ($.eventName=ReplaceNetworkAclAssociation)}
      ```

   1. Choose **Next**\.

1. Under **Assign metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. Choose the **Metric filters** tab, then choose the metric filter that you just created\.

   To choose the metric filter, select the check box at the upper right\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Under **Metric**, leave the default values\. For more information about the available statistics, see [Statistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Statistic) in the *Amazon CloudWatch User Guide*\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm\. For example, **CIS\-4\.11\-NetworkACLChanges**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## 4\.12 – Ensure a log metric filter and alarm exist for changes to network gateways<a name="securityhub-cis1.4-controls-4.12"></a>

**Severity:** Low

**AWS Config rule:** None

**Schedule type:** Periodic

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. Network gateways are required to send and receive traffic to a destination outside a VPC\.

CIS recommends that you create a metric filter and alarm for changes to network gateways\. Monitoring these changes helps ensure that all ingress and egress traffic traverses the VPC border via a controlled path\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 4\.12 in the [CIS AWS Foundations Benchmark v1\.2](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:2e5fec5c-5e99-4fb5-b08d-bb46b14754c1#pageNum=1)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cis1.4-4.12-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [3\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis1.4-controls-3.1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {($.eventName=CreateCustomerGateway) || ($.eventName=DeleteCustomerGateway) || ($.eventName=AttachInternetGateway) || ($.eventName=CreateInternetGateway) || ($.eventName=DeleteInternetGateway) || ($.eventName=DetachInternetGateway)}
      ```

   1. Choose **Next**\.

1. Under **Assign metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. Choose the **Metric filters** tab, then choose the metric filter that you just created\.

   To choose the metric filter, select the check box at the upper right\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Under **Metric**, leave the default values\. For more information about the available statistics, see [Statistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Statistic) in the *Amazon CloudWatch User Guide*\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm\. For example, **CIS\-4\.12\-NetworkGatewayChanges**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## 4\.13 – Ensure a log metric filter and alarm exist for route table changes<a name="securityhub-cis1.4-controls-4.13"></a>

**Severity:** Low

**AWS Config rule:** None

**Schedule type:** Periodic

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. Routing tables route network traffic between subnets and to network gateways\.

CIS recommends that you create a metric filter and alarm for changes to route tables\. Monitoring these changes helps ensure that all VPC traffic flows through an expected path\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 4\.13 in the [CIS AWS Foundations Benchmark v1\.4\.0](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:2e5fec5c-5e99-4fb5-b08d-bb46b14754c1#pageNum=1)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cis1.4-4.13-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [3\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis1.4-controls-3.1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {($.eventName=CreateRoute) || ($.eventName=CreateRouteTable) || ($.eventName=ReplaceRoute) || ($.eventName=ReplaceRouteTableAssociation) || ($.eventName=DeleteRouteTable) || ($.eventName=DeleteRoute) || ($.eventName=DisassociateRouteTable)}
      ```

   1. Choose **Next**\.

1. Under **Assign metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. Choose the **Metric filters** tab, then choose the metric filter that you just created\.

   To choose the metric filter, select the check box at the upper right\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Under **Metric**, for **Statistic**, choose **Average**\. For more information about the available statistics, see [Statistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Statistic) in the *Amazon CloudWatch User Guide*\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm\. For example, **CIS\-4\.13\-RouteTableChanges**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## 4\.14 – Ensure a log metric filter and alarm exist for VPC changes<a name="securityhub-cis1.4-controls-4.14"></a>

**Severity:** Low

**AWS Config rule:** None

**Schedule type:** Periodic

You can do real\-time monitoring of API calls by directing CloudTrail logs to CloudWatch Logs and establishing corresponding metric filters and alarms\. You can have more than one VPC in an account, and you can create a peer connection between two VPCs, enabling network traffic to route between VPCs\.

CIS recommends that you create a metric filter and alarm for changes to VPCs\. Monitoring these changes helps ensure that authentication and authorization controls remain intact\.

To run this check, Security Hub uses custom logic to perform the exact audit steps prescribed for control 4\.14 in the [CIS AWS Foundations Benchmark v1\.4\.0](https://acrobat.adobe.com/link/track?uri=urn:aaid:scds:US:2e5fec5c-5e99-4fb5-b08d-bb46b14754c1#pageNum=1)\. This control fails if the exact metric filters prescribed by CIS are not used\. Additional fields or terms cannot be added to the metric filters\.

**Note**  
When Security Hub performs the check for this control, it looks for CloudTrail trails that the current account uses\. These trails might be organization trails that belong to another account\. Multi\-Region trails also might be based in a different Region\.  
The check results in `FAILED` findings in the following cases:  
No trail is configured\.
The available trails that are in the current Region and that are owned by current account do not meet the control requirements\.
The check results in a control status of `NO_DATA` in the following cases:  
The multi\-Region trail is based in a different Region\. Security Hub can only generate findings in the Region where the trail is based\.
The multi\-Region trail belongs to a different account\. Security Hub can only generate findings for the account that owns the trail\.
For the alarm, the current account must either own the referenced Amazon SNS topic, or must get access to the Amazon SNS topic by calling `ListSubscriptionsByTopic`\. Otherwise Security Hub generates `WARNING` findings for the control\.

### Remediation<a name="cis1.4-4.14-remediation"></a>

The steps to remediate this issue include setting up an Amazon SNS topic, a CloudTrail trail, a metric filter, and an alarm for the metric filter\.

**To create an Amazon SNS topic**

1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v3/home](https://console.aws.amazon.com/sns/v3/home)\.

1. Create an Amazon SNS topic that receives all CIS alarms\.

   Create at least one subscriber to the topic\. For more information, see [Getting started with Amazon SNS](https://docs.aws.amazon.com/sns/latest/dg/sns-getting-started.html#CreateTopic) in the *Amazon Simple Notification Service Developer Guide*\.

Next, set up an active CloudTrail that applies to all Regions\. To do so, follow the remediation steps in [3\.1 – Ensure CloudTrail is enabled in all Regions](#securityhub-cis1.4-controls-3.1)\.

Make a note of the name of the CloudWatch Logs log group that you associate with the CloudTrail trail\. You create the metric filter for that log group\.

Finally, create the metric filter and alarm\.

**To create a metric filter and alarm**

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1. In the navigation pane, choose **Log groups**\.

1. Select the check box for the CloudWatch Logs log group that is associated with the CloudTrail trail that you created\.

1. From **Actions**, choose **Create Metric Filter**\.

1. Under **Define pattern**, do the following:

   1. Copy the following pattern and then paste it into the **Filter Pattern** field\.

      ```
      {($.eventName=CreateVpc) || ($.eventName=DeleteVpc) || ($.eventName=ModifyVpcAttribute) || ($.eventName=AcceptVpcPeeringConnection) || ($.eventName=CreateVpcPeeringConnection) || ($.eventName=DeleteVpcPeeringConnection) || ($.eventName=RejectVpcPeeringConnection) || ($.eventName=AttachClassicLinkVpc) || ($.eventName=DetachClassicLinkVpc) || ($.eventName=DisableVpcClassicLink) || ($.eventName=EnableVpcClassicLink)}
      ```

   1. Choose **Next**\.

1. Under **Assign metric**, do the following:

   1. In **Filter name**, enter a name for your metric filter\.

   1. For **Metric namespace**, enter **LogMetrics**\.

      If you use the same namespace for all of your CIS log metric filters, then all CIS Benchmark metrics are grouped together\.

   1. For **Metric name**, enter a name for the metric\. Remember the name of the metric\. You will need to select the metric when you create the alarm\.

   1. For **Metric value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Review and create**, verify the information that you provided for the new metric filter\. Then choose **Create metric filter**\.

1. Choose the **Metric filters** tab, then choose the metric filter that you just created\.

   To choose the metric filter, select the check box at the upper right\.

1. Choose **Create Alarm**\.

1. Under **Specify metric and conditions**, do the following:

   1. Under **Metric**, for **Statistic**, choose **Average**\. For more information about the available statistics, see [Statistics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/cloudwatch_concepts.html#Statistic) in the *Amazon CloudWatch User Guide*\.

   1. Under **Conditions**, for **Threshold**, choose **Static**\.

   1. For **Define the alarm condition**, choose **Greater/Equal**\.

   1. For **Define the threshold value**, enter **1**\.

   1. Choose **Next**\.

1. Under **Configure actions**, do the following:

   1. Under **Alarm state trigger**, choose **In alarm**\.

   1. Under **Select an SNS topic**, choose **Select an existing SNS topic**\.

   1. For **Send a notification to**, enter the name of the SNS topic that you created in the previous procedure\.

   1. Choose **Next**\.

1. Under **Add name and description**, enter a **Name** and **Description** for the alarm\. For example, **CIS\-4\.14\-VPCChanges**\. Then choose **Next**\.

1. Under **Preview and create**, review the alarm configuration\. Then choose **Create alarm**\.

## 5\.1 – Ensure no Network ACLs allow ingress from 0\.0\.0\.0/0 to remote server administration ports<a name="securityhub-cis1.4-controls-5.1"></a>

**Severity:** Medium 

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/nacl-no-unrestricted-ssh-rdp.html](https://docs.aws.amazon.com/config/latest/developerguide/nacl-no-unrestricted-ssh-rdp.html)

**Schedule type:** Change triggered

**Parameters:** None

This control checks whether a network access control list \(NACL\) allows unrestricted access to the default ports for SSH/RDP ingress traffic\. The rule fails if a NACL inbound entry allows a source CIDR block of '0\.0\.0\.0/0' or '::/0' for ports 22 or 3389\.

Access to remote server administration ports, such as port 22 \(SSH\) and port 3389 \(RDP\), should not be publicly accessible, as this may allow unintended access to resources within your VPC\.

**Note**  
This control is not supported in the following Regions:  
China \(Beijing\)
China \(Ningxia\)
AWS GovCloud \(US\-East\)
AWS GovCloud \(US\-West\)

### Remediation<a name="cis1.4-5.1-remediation"></a>

For more information about NACLs, see [Network ACLs](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html) in the VPC User Guide\.

## 5\.3 – Ensure the default security group of every VPC restricts all traffic<a name="securityhub-cis1.4-controls-5.3"></a>

**Severity:** High

**AWS Config rule:** [https://docs.aws.amazon.com/config/latest/developerguide/vpc-default-security-group-closed.html](https://docs.aws.amazon.com/config/latest/developerguide/vpc-default-security-group-closed.html)

**Schedule type:** Change triggered

A VPC comes with a default security group with initial settings that deny all inbound traffic, allow all outbound traffic, and allow all traffic between instances assigned to the security group\. If you don't specify a security group when you launch an instance, the instance is automatically assigned to this default security group\. Security groups provide stateful filtering of ingress and egress network traffic to AWS resources\.

CIS recommends that the default security group restrict all traffic\.

Update the default security group for the default VPC in every Region to comply\. Any new VPCs automatically contain a default security group that you need to remediate to comply with this recommendation\.

**Note**  
When implementing this recommendation, you can use VPC flow logging, enabled for [3\.9 – Ensure VPC flow logging is enabled in all VPCs ](#securityhub-cis1.4-controls-3.9), to determine the least\-privilege port access that systems require to work properly\. VPC flow logging can log all packet acceptances and rejections that occur under the current security groups\.

Configuring all VPC default security groups to restrict all traffic encourages least\-privilege security group development and mindful placement of AWS resources into security groups\. This in turn reduces the exposure of those resources\.

### Remediation<a name="cis1.4-5.3-remediation"></a>

**To update the default security group to restrict all access**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. View the default security groups details to see the resources that are assigned to them\.

1. Create a set of least\-privilege security groups for the resources\.

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. On the Amazon EC2 console, change the security group for the resources that use the default security groups to the least\-privilege security group you created\.

1. For each default security group, choose the **Inbound** tab and delete all inbound rules\.

1. For each default security group, choose the **Outbound** tab and delete all outbound rules\.

For more information, see [Working with Security Groups](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html#WorkingWithSecurityGroups) in the *Amazon VPC User Guide*\.