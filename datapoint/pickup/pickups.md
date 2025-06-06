# Pickup configuration

> Back to the [Datapoint Page](../datapoint.md)

## Background

**Pickups** are defined as FarEarth's method of managing a *datastore* with the capability to copy/ingest/push input data of a user or client into the FarEarth processing chain. Input data consumed by these datastores are flagged for processing, and if configured correctly is a very powerful tool in easing the burden of input data management.

> FarEarth currently support four types of *Pickup* **Protocols** and these are defined as:
* **[filesystem](pickup-filesystem.md)**: This protocol is used by any locally run zipped version of the FarEarth application components such as the, *datapoint*, *director-bundled*, *catalogue*, *gateway-bundled* etc. In the case of Pickups, the *Datapoint* is the most relevant application for *filesytem* use.
* **[azure](pickup-azure.md)**: This protocol is used when interfacing with Microsoft Azure, and leveraging their blob storage as a pickup point.
* **[amazon-s3](pickup-s3.md)**: This protocol is used when interfacing with Amazon S3, and leveraging their buckets storage for a pickup point.
* **[gdrive](pickup-gdrive.md)**: This protocol is used when interfacing with Google Drive, and leveraging their cloud storage as a pickup point.
* **[pyxis](pickup-pyxis.md)**: This protocol is used when interfacing with Google Drive, and leveraging their cloud storage as a pickup point.

## Configuration

Creating a **Pickup** occurs on the **PICKUPS** page under the **DATAPOINT CONFIG** section of any subscription. 
You do however need to be an **administrator** or **root admin** with a **Datapoint** resource shared to said subscription to have the necessary permissions for creating, editing or deleting a pickup. 

* Take note however that if the pickup is being created under a *bundled* application such as FarEarth's **Gateway-Bundled** or **Director-Bundled**, a *Datapoint* is part of the overall bundled installation, which does not require specific sharing of said resource to the **farearth** subscription.

* To create a new *pickup*, click on the **CREATE PICKUP** button, for the **New Pickup** modal to be displayed. Within this modal a few key fields are displayed that should be filled in by the admin user.

> Defining the contents of the modal:

| Field | Description | Details |
|-------|-------------|---------|
| App | Parent Application | The application under which the pickup is being created i.e., *gateway-bundled*, *datapoint* etc. |
| Subscription | Parent subscription | The subscription under which the pickup is being created such as the *farearth* subscription |
| ID | Pickup ID | The ID value that the admin chooses for the pickup to be created under |
| File Name | JSON file name | The actual file name of the pickup json file generated. This is prepopulated when entering the *ID*, with the *subscription*.*ID*.*pickup*.*json*, however the admin is free to choose what the file name should be, within formatting rules |
| Protocol | Datastore protocol | Dropdown list of the four available protocols, which defines what datastore is to be used, and which configuration requirements should be entered |

* After filling out the form with the pickup details, and clicking the **CREATE** button a new pickup will be generated on the **PICKUPS** page, with a default json blob contained within it. This requires further configuration explained below.
* To explain the content of the pickup json files in more detail the table below.

> Pickup json file contents with definitions:

| Field | Example Value | Description | Details |
|-------|---------------|-------------|---------|
| id | farearth.azure-pickup-101, farearth.fs-pickup-101 etc. | Pickup ID | This field is the pickup's physical ID which includes the subscriptionID under which it has been created. This is used as part of the audit and authorization trail for the pickup itself |
| protocol | azure, gdrive, filesystem, amazon-s3 | Datastore Protocol | This defines what type of datastore is being used, and what parameters and properties are applicable to it |
| dataRetentionWindow | "12 hours" | Data Retention Period | This parameter defines how long lingering data is retained in the pickup before the cleanup functionality removes it |
| shareable | true, false | Shareable Resource | Sets the pickup as shareable or not as a resources for other subscriptions than the one it was created on. The flag is set to *false* by default if omitted from the config file |
| attachParameters | "workflowId", "sendNotification" | Adding Useful Parameters | Attaching Parameters adds optional extras in tailoring a pickup's automation capabilities such as:
|                  |                                  |                          | - *workflowId*: specifies which workflow to run on ingested input data |
|                  |                                  |                          | - *sendNotifications*: sends an email upon processing completion for the ingested input data |
| dataStoreLimits | "capacity", "warnOnRemaining", "errorOnRemaining"  | Data Storage Limit Management | Setting up the *dataStoreLimits* allows for customized insurance on the availability of allocated storage space of the pickup point. Using fields such as: 
|                 |                                                    |                               | - capacity: Setting the maximum available storage for the datastore
|                 |                                                    |                               | - warnOnRemaining: Receive a warning when less than the set minimum storage space is available for the datastore
|                 |                                                    |                               | - errorOnRemaining: Receive an error when less than the set minimum storage space is available for the datastore |
| properties | "containerName", "baseUrl", "connectionString", credFileB64, etc.  | Protocol Dependent Datastore Properties | Each of the properties that can be seen in the json examples are *required* for the startup of the relevant individual protocol datastore, meaning if any of the properties are missing the pickup will not work. The required fields for example the *baseUrl*, *accessKey*, *connectionString*, etc. is generated during the creation of the datastore on the service provider's (read protocol host) web based client, and can be extracted from there for configuration on the FarEarth platform |
| triggers | "READY_FILE", "NO_CHANGE", "FILE_MANIFEST", "MD5_FILE", etc. | Data Ingestion Triggers | Triggers are various ways of accepting the input data and kicking off processing. More on this topic below |

* As mentioned **triggers** is FarEarth's way of "realizing" input data has been made available for processing, but it is also a way of filtering out data or garbage that might find it's way into a pickup point. In that case we would rather not want to start processing and waste valuable resources on junk or incomplete data. 
* It is also important to note that all input datasets that are ingested via a browser based interface such as Google Drive should be placed into a folder and uploaded in that folder. 
* There are currently seven triggers available explained in the below table.

> Table of Triggers:

| Trigger | Additional Parameters | Details |
|---------|-----------------------|---------|
| "ACCEPT_ALL" | "delay": "5m" | Triggers off of any file, however you'll need to add the *delay* parameter as to prevent ingestion of the input data before the copy operation into the pickup point has completed |
| "NO_CHANGE" | "delay": "60s", "minimumFileCount": 3 | Triggers off of no changes occurring to the input data in this example's case, for 60 seconds. Additionally it requires a minimum input file count of 3 files before triggering |
| "FOLDER_SUFFIX" | "busySuffix": "_busy", "doneSuffix": "_completed" | Triggers based off of the suffix used within the name of the folder, meaning creating a folder name i.e, *data_busy*, will not start processing, only after the folder name has been updated to *data_completed*, will the dataset be ingested. This trigger is usually used if the data is copied by an Acquisition Controller, that modifies the folder suffixes during and after copy the input data into it |
| "FILE_MANIFEST" | "suffix": "_manifest.txt" | Triggers based off of the contents of a manifest file that describes the input dataset, and is in the same folder as the input data. An example of the manifest file contents below |
| "READY_FILE" | N/A | Triggers off a sidecarred file with file extension of *.READY*. An example of the file contents below |
| "PRODUCT_FILE" | "suffix": "_product.json" | Triggers based off of the presence of a json product file that is contained within the folder of the input dataset. An example of the file contents below |
| "MD5_FILE" | "suffix": ".MD5" | Triggers based off of the presence of a MD5 file containing the checksum(s) of the input dataset. The file should be contained within the input data folder |

> Formatted json example of Triggers:

```json
    "triggers": [
        {
            "id": "ACCEPT_ALL",
            "delay": "5m"
        },
        {
            "id": "NO_CHANGE",
            "delay": "60s",
            "minimumFileCount": 3
        },
        {
            "id": "FOLDER_SUFFIX",
            "busySuffix": "_busy",
            "doneSuffix": "_completed"
        },
        {
            "id": "FILE_MANIFEST",
            "suffix": "_manifest.txt"
        },
        {
            "id": "READY_FILE"
        },
        {
            "id": "PRODUCT_FILE",
            "suffix": "_product.json"
        },
        {
            "id": "MD5_FILE",
            "suffix": ".MD5"
        },
    ]
```

* Also take note that for any of the above **triggers** that have a *suffix* parameter the default of said suffix could be omitted from the *json* file. This means for example when looking at the **FOLDER_SUFFIX**, the *"busySuffix": "_busy"* is its default setting, and can be omitted from the config file. Only when you want to change the default from *"_busy"* to something like *"_inProgress"* do you need explicitly define it in the config file.

> File manifest example:

```text
5815_5_20231019132435_TRUBIT-1_PA51_QDRA_2023-Oct-19-13-25-17107_5_20231019132435_TRUBIT-1_PA51_QDRA_2023-Oct-19-13-25-17.cadu_bbframe_merged_1697671170.raw 13779941880
6839_5_20231019124755_TRUBIT-1_SG184_QDRA_2023-Oct-19-12-48-37271_5_20231019124755_TRUBIT-1_SG184_QDRA_2023-Oct-19-12-48-37.cadu_bbframe_merged_1697671170.raw 15774919584
```

* The manifest file contents described as: *File Name* *File Size*. In addition you also only have to list all *File Names* within the manifest each on a new line.

> READY file example:

```json
{
  "workflowId" : "farearth.archive",
  "properties" : {
    "id" : "1-TRUBIT-1-20220120-KANSAS-5",
    "gsd" : [ 5.0, -5.0 ],
    "productType" : "imagery",
    "dataset" : "geni-benchmarks",
    "datetime" : "2022-01-20T21:15:30Z",
    "spacecraft" : "TRUBIT-1",
    "instruments" : [ "MS-100" ],
    "bbox" : [ ],
    "eoBands" : [ {
      "name" : "B01",
      "commonName" : "Blue",
      "centerWavelengthNanoMeter" : 490.0,
      "fullWidthHalfMaxNanoMeter" : 65.0
    }, {
      "name" : "B02",
      "commonName" : "Green",
      "centerWavelengthNanoMeter" : 560.0,
      "fullWidthHalfMaxNanoMeter" : 35.0
    }, {
      "name" : "B03",
      "commonName" : "Red",
      "centerWavelengthNanoMeter" : 665.0,
      "fullWidthHalfMaxNanoMeter" : 30.0
    }, {
      "name" : "B04",
      "commonName" : "Red-Edge1",
      "centerWavelengthNanoMeter" : 705.0,
      "fullWidthHalfMaxNanoMeter" : 15.0
    }, {
      "name" : "B05",
      "commonName" : "Red-Edge2",
      "centerWavelengthNanoMeter" : 740.0,
      "fullWidthHalfMaxNanoMeter" : 15.0
    }, {
      "name" : "B06",
      "commonName" : "Red-Edge3",
      "centerWavelengthNanoMeter" : 783.0,
      "fullWidthHalfMaxNanoMeter" : 20.0
    }, {
      "name" : "B07",
      "commonName" : "NIR",
      "centerWavelengthNanoMeter" : 842.0,
      "fullWidthHalfMaxNanoMeter" : 115.0
    } ],
    "geometry" : {
      "type" : "Point",
      "coordinates" : [ -101.40862, 39.18863 ]
    }
  },
  "inputFiles" : {
    "1-TRUBIT-1-20220120-KANSAS-5.TIF" : {
      "id" : "IMAGE",
      "title" : "Unprojected image",
      "roles" : [ "data" ],
      "type" : "image/tiff"
    }
  }
}
```

* Regarding the **READY** file it is important to note that the *required fields* for i.e., ingesting a dataset into the *Archive*, as part of *STAC* compliance, are the following:
    * **workflowId**: The worfklow ID of the workflow to be used or kicked off by the Pickup upon data ingestion.
    * **productType**: The STAC standard product type to be assigned to the input dataset.
    * **datetime**: The date and time of the data acquisition, with a format of: *yyyy-mm-ddThh:mm:ssZ*.
    * **inputFiles**: This section defines what input files are to be ingested, it could be one file or multiple. The *required fields* for the inputFiles section are:
        * **inputName**: The actual file name on disk.
        * **id**: The STAC standard id for the file as part of a collection.
        * **title**: A descriptive title for the input file.

> Product file example contents:

```json
{
  "type" : "Feature",
  "id" : "1694394734_small",
  "assets" : {
    "RAW" : {
      "title" : "RAW ses file",
      "href" : "sample_500MB.raw",
      "size" : 524288000
    }
  },
  "bbox" : null,
  "geometry" : null,
  "properties" : {
    "spacecraft" : "TRUBIT-1",
    "datetime" : "2023-05-18T07:33:56Z",
    "id" : "1694394734_small",
    "productType" : "RAW"
  },
  "links" : [ ],
  "stac_version" : "0.9.0"
}
```

* Regarding the **PRODUCT** file it is important to note the *required fields* for i.e., describing a file for ingestion into the *Archive*. Fields that are *required* are very similar to the **READY** file requirements as it also pertains to STAC compliance.

> MD5 file example contents:

```text
9B68D20CD048E31017207ED91817DC7C sample_500MB.raw
```

* Regarding the **MD5** file it is important to note that the some datastore providers are able to calculate the *checksums* automatically, and that is the reason for MD5 support. Note that it is an expensive operation to calculate checksums manually for every ingestion operation. If you look at the actual file you'll see that it is merely the *checksum* of the input file separated by a space followed by the actual file name in this case *sample_500MB.raw*. Where multiple files exist within the folder each would be displayed in a new line with a similar format.

* One last note regarding the **"shareable": true,** flag, if this is set to *true* (default it is set to *false*), and the **pickup** has been correctly configured, the newly added pickup will be shareable from the **Subscriptions** page under any of the available *group* and/or *default* subscriptions by a *root admin*, effectively making the pickup a shareable resource.

> Back to the [Datapoint Page](../datapoint.md)