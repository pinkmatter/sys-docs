# Datapoint

##### [Home](../README.md) > Datapoint
---

In *FarEarth*, a Datapoint is a data management component. A [Pickup](pickup/pickups.md) is a specific configuration of a Datapoint that is responsible for ingesting data from a specific location.

*FarEarth* currently support these methods and protocols for ingesting data:
* Directly from your own storage
* Microsoft Azure blob storage
* Amazon's AWS S3 buckets
* Google Drive
* *FarEarth*'s Pyxis

For more information on the above, refer to the [Pickups](pickup/pickups.md) documentation.

In addition, you can also ingest data for processing from within *FarEarth*:
* From the Archive, using the [Catalogue](../catalogue/catalogue.md)
* Using the [APIs](../developer/api/api.md)
* Manually, through a web browser, in the *FarEarth* portal
