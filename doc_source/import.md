# Step 2: Import Your LDIF File<a name="import"></a>

You can extend your schema by importing an LDIF file from either the AWS Directory Service console or by using the API\. For more information about how to do this with the schema extension APIs, see the [http://docs.aws.amazon.com/directoryservice/latest/devguide/](http://docs.aws.amazon.com/directoryservice/latest/devguide/)\. At this time, AWS does not support external applications, such as Microsoft Exchange, to perform schema updates directly\. 

**Important**  
When you make an update to your AWS Managed Microsoft AD directory schema, the operation is not reversible\. In other words, once you create a new class or attribute, Active Directory doesn’t allow you to remove it\. However, you can disable it\.   
If you must delete the schema changes, one option is to restore the directory from a previous snapshot\. Restoring a snapshot rolls both the schema and the directory data back to a previous point, not just the schema\.

Before the update process begins, AWS Managed Microsoft AD takes a snapshot to preserve the current state of your directory\.

**To import your LDIF file**

1. In the [AWS Directory Service console](https://console.aws.amazon.com/directoryservice/) navigation pane, select **Directories**\.

1. In the **Directory ID** column, choose the link for your directory\.

1. Under the **Schema extensions** tab, choose **Upload and update schema**\.

1. In the dialog box, click **Browse**, select a valid LDIF file, type a description, and then choose **Update Schema**\.
**Important**  
Extending the schema is a critical operation\. Don’t apply any schema update in production environment without first testing it with your application in a development or test environment\.

## How is the LDIF File Applied<a name="howapplied"></a>

After your LDIF file has been uploaded, AWS Managed Microsoft AD takes steps to protect your directory against errors as it applies the changes in the following order\. 

1. **Validates the LDIF file\.** Since LDIF scripts can manipulate any object in the domain, AWS Managed Microsoft AD runs checks right after you upload to help ensure that the import operation will not fail\. These include checks to ensure the following:
   + The objects to be updated are only held in the schema container
   + The DC \(domain controllers\) part matches the name of the domain where the LDIF script is running

1. **Takes a snapshot of your directory\.** You can use the snapshot to restore your directory in case you encounter any problems with your application after updating the schema\. 

1. **Applies the changes to a single DC\.** AWS Managed Microsoft AD isolates one of your DCs and applies the updates in the LDIF file to the isolated DC\. It then selects one of your DCs to be the schema master, removes that DC from directory replication, and applies your LDIF file using `Ldifde.exe`\.

1. **Replication occurs to all DCs\.** AWS Managed Microsoft AD adds the isolated DC back in to replication to complete the update\. While this is all happening, your directory continues to provide the Active Directory service to your applications without disruption\.

**Next Step**

[Step 3: Verify If The Schema Extension Was Successful](verify.md)