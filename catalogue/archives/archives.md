# Archive configuration

> Back to the [Catalogue Page](../catalogue.md)

## Background

**Archives** are defined as FarEarth's method of managing a *datastore* with the capability to store input data as well as processed product data and any intermediary metadata files, etc. As an order progresses through each of its defined jobs as part of processing, published files are ingested into this *Archive* datastore.

> FarEarth currently supports four types of *Archive* **Protocols**, and these are defined as:
* **[filesystem](archive-filesystem.md)**: This protocol is used by any locally run zipped version of the FarEarth application components such as *datapoint*, *director-bundled*, *catalogue*, *gateway-bundled*, etc. In the case of Archives, the *Catalogue* is the most relevant application for *filesystem* use.
* **[azure](archive-azure.md)**: This protocol is used when interfacing with Microsoft Azure, leveraging their blob storage as an archive.
* **[amazon-s3](archive-s3.md)**: This protocol is used when interfacing with Amazon S3, leveraging their bucket storage for an archive.
* **[gdrive](archive-gdrive.md)**: This protocol is used when interfacing with Google Drive, leveraging their cloud storage as an archive.
* **[pyxis](archive-pyxis.md)**: FarEarth's own blob storage protocol, called Pyxis.


## Configuration

Creating an **Archive** occurs on the **ARCHIVES** page under the **CATALOGUE CONFIG** section of any subscription.
You do, however, need to be an **administrator** or **root admin** with an **Archive** resource shared to said subscription to have the necessary permissions for creating, editing, or deleting an archive.

* Take note that if the archive is being created under a *bundled* application such as FarEarth's **Gateway-Bundled** or **Director-Bundled**, an *Archive* is part of the overall bundled installation, which does not require specific sharing of the said resource to the **farearth** subscription.

* To create a new *archive*, click on the **CREATE ARCHIVE** button, and the **New Archive** modal will be displayed. Within this modal, a few key fields are displayed that should be filled in by the admin user.

> Defining the contents of the modal:

| Field       | Description        | Details                                                                     |
|-------------|--------------------|-----------------------------------------------------------------------------|
| App         | Parent Application  | The application under which the archive is being created, i.e., *gateway-bundled*, *catalogue* etc. |
| Subscription| Parent subscription | The subscription under which the archive is being created such as the *farearth* subscription |
| ID          | Archive ID          | The ID value that the admin chooses for the archive to be created under      |
| File Name   | JSON file name      | The actual file name of the archive json file generated. This is prepopulated when entering the *ID*, with the *subscription*.*ID*.*archive*.*json*, however the admin is free to choose what the file name should be, within formatting rules |
| Protocol    | Datastore protocol  | Dropdown list of the four available protocols, which defines what datastore is to be used, and which configuration requirements should be entered |

* After filling out the form with the archive details and clicking the **CREATE** button, a new archive will be generated on the **ARCHIVES** page, with a default JSON blob contained within it. This requires further configuration explained below.
* For each of the above default archive json blobs, specific configuration parameters are required on a per protocol basis.

* To explain the content of the archive json files in more detail the table below.

> Archive json file contents with definitions:

| Field | Example Value | Description | Details |
|-------|---------------|-------------|---------|
| id | farearth.azure-archive-101, farearth.fs-archive-101 etc. | Archive ID | This field is the archive's physical ID which includes the subscriptionID under which it has been created. This is used as part of the audit and authorization trail for the archive itself |
| protocol | azure, gdrive, filesystem, amazon-s3 | Datastore Protocol | This defines what type of datastore is being used, and what parameters and properties are applicable to it |
| prefix | FarEarth-Testing/{subscription}/{year}/{doy}/{uuid} | Flat folder structure | This string effectively creates a faux folder structure wherein data is published for storing. More on the available variables for folder structures below |
| shareable | true, false | Shareable Resource | Sets the archive as shareable or not as a resources for other subscriptions than the one it was created on. The flag is set to *false* by default if omitted from the config file |
| accessModes | PUSH, PULL | Access mode supported for data requests | Specify the type of data requests the archive support out of the perspective of the recipient. It can be PUSH/PULL or both |
| dataStoreLimits | "capacity", "warnOnRemaining", "errorOnRemaining"  | Data Storage Limit Management | Setting up the *dataStoreLimits* allows for customized insurance on the availability of allocated storage space of the archive. Using fields such as:
|                 |                                                    |                               | - capacity: Setting the maximum available storage for the datastore (see **Rolling Archive** section for more information)
|                 |                                                    |                               | - warnOnRemaining: Receive a warning when less than the set minimum storage space is available for the datastore
|                 |                                                    |                               | - errorOnRemaining: Receive an error when less than the set minimum storage space is available for the datastore |
| properties | "containerName", "baseUrl", "connectionString", credFileB64, etc.  | Protocol Dependent Datastore Properties | Each of the properties that can be seen in the json examples are *required* for the startup of the relevant individual protocol datastore, meaning if any of the properties are missing the archivenot work. The required fields for example the *baseUrl*, *accessKey*, *connectionString*, etc. is generated during the creation of the datastore on the service provider's (read protocol host) web based client, and can be extracted from there for configuration on the FarEarth platform |

* As mentioned the **prefix** field creates the semblance of a *folder structure* within the protocol relevant datastore. This is to make it more easily distinguishable between datasets and their unique identifying characteristics on a heuristic basis.

* It is important to note, apart from being an administrator with access rights to the relevant datastore provider interface, you'll likely never see the prefixed folder structure. This is because the actual front-end view of the input and/or product data is done via the *Catalogue* itself rather than the datastore provider's interfaces.

#### Rolling Archive

The Rolling Archive mechanism is triggered when the capacity property, under dataStoreLimits, is set in the configuration. This feature monitors the archive's current usage (during startup or after each product is published) by checking the data recorded in the Catalogue. If the defined capacity is exceeded, it will begin deleting complete products from the archive, starting with the oldest orders based on their processed date. Refer to the JSON example for Azure above, which demonstrates enabling Rolling Archive with a 64GB capacity* limit for that archive configuration.

Please note, the capacity calculation is based on what is registered in the Catalogue and linked to each archive configuration, not the actual size of the binary files in storage. Therefore, if there are external files or other archive configurations pointing to the same bucket/container/folder, it won’t impact the system's calculated capacity.

 **Values that can be specified are in MB/GB/TB, ie 1000000MB=1000GB=1TB*

#### Prefix templates

The following table shows template variables that can be used to customize sub-directory placement of archived products.

```text
storeDataId  |  The store data id, e.g. '628'
dataStoreId  |  The current data store, e.g. 'filesystem-metop-archive'
subscription |  The current subscription, e.g. 'farearth'
spacecraft   |  The spacecraft used for the imagery,, e.g. 'METOP-C'
uuid or guid |  Generated randomly, e.g. f567252a-77b9-11ee-b962-0242ac120002
year         |  Year of day number e.g. 2023 (derived from the 'datetime' product property)
doy          |  Day of year number 01 .. 365/6 (derived from the 'datetime' product property)
month        |  Month of year number 01 .. 12 (derived from the 'datetime' product property)
day          |  Day of month number 01 .. 31 (derived from the 'datetime' product property)
woy          |  Week of year number 01 .. 52 (derived from the 'datetime' product property)
hours        |  Hour of day number 00 .. 23 (derived from the 'datetime' product property)
minutes      |  Minutes of hour number 00 .. 59 (derived from the 'datetime' product property)
seconds      |  Seconds of minute number 00 to 59 (derived from the 'datetime' product property)
productId    |  Synonym for 'id', e.g. 'metopa_68198_20191211T015827'
userId       |  A sanitized representation of the user ID (e.g. 'test-at-gmail-com' for email 'test@gmail.com')
```

* As mentioned the variables can either be static or taken from the product being archive (e.g., *spacecraft*, *datetime*, or *instruments*), and are described by two curly braces "{}". An example of this can be seen in the above *Azure* or *Google Drive* protocol json blobs.

> Back to the [Catalogue Page](../catalogue.md)