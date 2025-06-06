# Catalogue 

##### [Home](../README.md) > Catalogue
---

*FarEarth*'s Catalogue is the component that securely and reliably manages all data. The Catalogue has support for the most popular cloud storage providers, through the [Archive](archives/archives.md) subsystem.

All products in *FarEarth* are STAC compliant. The Catalogue also supports integrating external STAC catalogues transparently.

![Catalogue diagram](catalogue.png "FarEarth Catalogue Diagram")

We have extended the STAC concept of [Collections](collections/collections.md) for improved organising and searching capabilities.

## Terms and definitions

In *FarEarth* we use the terms below to mean specific things.

| Term | Description |
|------|-------------|
| [Archive](archives/archives.md) | *FarEarth*'s datastore where all data is stored. |
| Catalogue | *FarEarth* application responsible for configuring the archives, as well as providing a web-based interface to query the data in the various datastores. |
| Catalog | STAC concept to group a set of collections together. |
| [Collection](collections/collections.md) | STAC definition to group items (products) together within a Catalog. *FarEarth* extends this concept to allow for dynamic products grouping based on filters. |

