---

copyright:
  years: 2017, 2019
lastupdated: "2019-10-25"

keywords: schematics limitations, schematics variables.tf, schematics local variables file, schematics local variable, schematics output.tf, schematics terraform.tfstate

subcollection: schematics

---
{:new_window: target="_blank"} 
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}
{:faq: data-hd-content-type='faq'}
{:external: target="_blank" .external}

# Limitations
{: #schematics-limitations}

Review the following limitations for {{site.data.keyword.bplong_notm}}.
{: shortdesc}

## Differences to native Terraform
{: #terraform-vs-schematics}

If you used native Terraform before and plan to migrate your Terraform templates to {{site.data.keyword.bplong_notm}}, make sure that you understand the differences between the services to adjust your template.  
{: shortdesc}

### Do I need to provide an {{site.data.keyword.cloud_notm}} API key in the `provider` block?
{: #provider-block}

The {{site.data.keyword.cloud_notm}} API key is essential to authenticate with the {{site.data.keyword.cloud_notm}} platform, receive the IAM token and IAM refresh token that {{site.data.keyword.bpshort}} requires to work with the resource's API, and to determine the permissions that you were granted. When you use native Terraform, you must provide the {{site.data.keyword.cloud_notm}} API key at all times. In {{site.data.keyword.bpshort}}, the API key is automatically retrieved for all IAM-enabled resources, including {{site.data.keyword.containerlong_notm}}, and VPC infrastructure resources. However, the API key is not retrieved for Cloud Foundry and classic infrastructure resources and must be provided in the `provider` block.
{: shortdesc}

For more information about how to configure the `provider` block, see [Configuring the `provider` block](/docs/schematics?topic=schematics-create-tf-config#configure-provider). 

### Can I use my local `terraform.tfvars` file?
{: #terraformtfvars}

The `terraform.tfvars` file is a local variables file that you use to store sensitive information, such as your {{site.data.keyword.cloud_notm}} API key or classic infrastructure user name when you use native Terraform. This file must be present on your local machine so that Terraform can load the values for your credentials when you initialize the Terraform CLI. 
{: shortdesc}

With {{site.data.keyword.bplong_notm}}, you do not use a local `terraform.tfvars` file. Instead, you [declare your variables](/docs/schematics?topic=schematics-create-tf-config#configure-variables) in the Terraform configuration files, and enter the values for your variables when you create a workspace. You can later change the values of your variables by updating the variables from your workspace details page. 

### Can I import an existing `terraform.tfstate` file?
{: #terraformtfstate}

If you used native Terraform before to provision and manage {{site.data.keyword.cloud_notm}} resources, you might have a `terraform.tfstate` file in your GitHub repository that stores the current state of your Terraform-deployed {{site.data.keyword.cloud_notm}} resources. 
{: shortdesc}

These `terraform.tfstate` files are not imported when you create a {{site.data.keyword.bpshort}} workspace. Because the `terraform.tfstate` file is not available to {{site.data.keyword.bplong_notm}}, you cannot use the service to manage {{site.data.keyword.cloud_notm}} resources that you already provisioned and started managing with native Terraform. 

### Can I use an `output.tf` file? 
{: #terraform-output}

In a `output.tf` file, you can include the information that you want to retrieve about your resources after the Terraform template is applied in your {{site.data.keyword.cloud_notm}} environment. 
{: shortdesc}

In native Terraform, you can access the information that you defined in the `output.tf` file by using the `terraform output` command. This command is not supported in {{site.data.keyword.bpshort}}. 

## Data storage and residency
{: #limitation-data-residency}

Before you start using {{site.data.keyword.bpshort}}, make sure to understand the data storage limitations. 
{: shortdesc}

### Where is my personal data stored?
{: #data-storage}

By default, all [information that {{site.data.keyword.bpshort}} retrieves](/docs/schematics?topic=schematics-faqs#data-residency) is encrypted in transit and at rest. To make your data highly available, all data is stored in the US South region and replicated to the US East region. You cannot choose the region where your data is stored. 
{: shortdesc}

When you select a zone that is located outside your country, keep in mind that you might require legal authorization before data can be physically stored in a foreign country.
{: important}

### How can I access {{site.data.keyword.bpshort}} events?
{: #at-events}

Events that are generated by {{site.data.keyword.bpshort}} are automatically forwarded to the {{site.data.keyword.at_full_notm}} service that is located in US South. To view your events, you must have an instance of {{site.data.keyword.cloudaccesstrailshort}} in the US South region.
{: shortdesc}

For more information about the events that are generated by {{site.data.keyword.bpshort}}, see [{{site.data.keyword.at_full_notm}} events](/docs/schematics?topic=schematics-at_events). 