# PCI DSS controls that you might want to disable<a name="securityhub-standards-pcidss-to-disable"></a>

To save on the cost of AWS Config, you can disable recording of global resources in all but one Region\. When do you this, Security Hub will still run security checks in all Regions where controls are enabled and will charge you based on the number of checks per account per Region\. Accordingly, to save on the cost of Security Hub, disable these controls that deal with global resources in all Regions except the Region that records global resources\.
+ [\[PCI\.CW\.1\] A log metric filter and alarm should exist for usage of the "root" user](securityhub-pci-controls.md#pcidss-cw-1)
+ [\[PCI\.IAM\.1\] IAM root user access key should not exist](securityhub-pci-controls.md#pcidss-iam-1)
+ [\[PCI\.IAM\.2\] IAM users should not have IAM policies attached](securityhub-pci-controls.md#pcidss-iam-2)
+ [\[PCI\.IAM\.3\] IAM policies should not allow full "\*" administrative privileges](securityhub-pci-controls.md#pcidss-iam-3)
+ [\[PCI\.IAM\.4\] Hardware MFA should be enabled for the root user](securityhub-pci-controls.md#pcidss-iam-4)
+ [\[PCI\.IAM\.5\] Virtual MFA should be enabled for the root user](securityhub-pci-controls.md#pcidss-iam-5)
+ [\[PCI\.IAM\.6\] MFA should be enabled for all IAM users](securityhub-pci-controls.md#pcidss-iam-6)

If you disable these controls and disable recording of global resources in a particular Region, you should also disable[ \[PCI\.Config\.1\] AWS Config should be enabled](securityhub-pci-controls.md#pcidss-config-1)\. This is because [ \[PCI\.Config\.1\] AWS Config should be enabled](securityhub-pci-controls.md#pcidss-config-1) requires recording of global resources in order to pass\.