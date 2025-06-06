# Hosting configuration

> Back to the [Processing Page](../processing.md)

## Background

**Hosting** is defined as FarEarth's method of managing the transient processing cache (hosted processing data), that is to be shared between *executor nodes* during processing. It is simply put, another *datastore* such as a *pickup* from where FarEarth is able to share the hosted processing data, which is necessary as executor nodes are spun up and shut down rapidly in between jobs, and FarEarth needs some method of retaining the necessary data in between processing jobs of i.e., one order in progress.

* Another name for **hosting** would be to call it a **dataHost**, as this is its functional use as well.

> FarEarth currently support three types of *Hosting* **Protocols** and these are defined as:
* **[filesystem](hosting-filesystem.md)**: This protocol is used by any locally run zipped version of the FarEarth application components such as the, *Processor*, *director-bundled*, *catalogue*, *gateway-bundled* etc. In the case of Hosting, the *Processor* is the most relevant application for *filesytem* use.
* **[azure](hosting-azure.md)**: This protocol is used when interfacing with Microsoft Azure, and leveraging their blob storage as a dataHost.
* **[amazon-s3](hosting-s3.md)**: This protocol is used when interfacing with Amazon S3, and leveraging their buckets storage for a dataHost.

## Configuration

Creating a **Hosting** occurs on the **HOSTING** page under the **PROCESSOR CONFIG** section of any subscription. 
You do however need to be an **administrator** or **root admin** with a **Processor** resource shared to said subscription to have the necessary permissions for creating, editing or deleting a dataHost. 

* Take note however that if the dataHost is being created under a *bundled* application such as FarEarth's **Gateway-Bundled** or **Director-Bundled**, a *Processor* is part of the overall bundled installation, which does not require specific sharing of said resource to the **farearth** subscription.

* To create a new *dataHost*, click on the **CREATE HOSTING** button, for the **New Hosting** modal to be displayed. Within this modal a few key fields are displayed that should be filled in by the admin user.

| Field | Description | Details |
|-------|-------------|---------|
| App | Parent Application | The application under which the dataHost is being created i.e., *gateway-bundled*, *processor* etc. |
| Subscription | Parent subscription | The subscription under which the dataHost is being created such as the *farearth* subscription |
| ID | Hosting ID | The ID value that the admin chooses for the dataHost to be created under |
| File Name | JSON file name | The actual file name of the dataHost json file generated. This is prepopulated when entering the *ID*, with the *subscription*.*ID*.*dataHost*.*json*, however the admin is free to choose what the file name should be, within formatting rules |
| Protocol | Datastore protocol | Dropdown list of the four available protocols, which defines what datastore is to be used, and which configuration requirements should be entered |

* After filling out the form with the pickup details, and clicking the **CREATE** button a new pickup will be generated on the **HOSTINGS** page, with a default json blob contained within it. This requires further configuration explained below.

* To explain the content of the hosting json files in more detail the table below.

> Hosting json file contents with definitions:

| Field | Example Value | Description | Details |
|-------|---------------|-------------|---------|
| id | farearth.azure-host-101, farearth.fs-host-101 etc. | Hosting ID | This field is the dataHost's physical ID which includes the subscriptionID under which it has been created. This is used as part of the audit and authorization trail for the dataHost itself |
| protocol | azure, filesystem, amazon-s3 | Datastore Protocol | This defines what type of datastore is being used, and what parameters and properties are applicable to it |
| dataRetentionWindow | "12 hours" | Data Retention Period | This parameter defines how long lingering data is retained in the dataHost before the cleanup functionality removes it |
| shareable | true, false | Shareable Resource | Sets the dataHost as shareable or not as a resources for other subscriptions than the one it was created on. The flag is set to *false* by default if omitted from the config file |
| properties | "containerName", "baseUrl", "connectionString", accessKey, secretKey, etc.  | Protocol Dependent Datastore Properties | Each of the properties that can be seen in the json examples are *required* for the startup of the relevant individual protocol datastore, meaning if any of the properties are missing the dataHost will not work. The required fields for example the *baseUrl*, *accessKey*, *connectionString*, etc. is generated during the creation of the datastore on the service provider's (read protocol host) web based client, and can be extracted from there for configuration on the FarEarth platform |

> Back to the [Processing Page](../processing.md)