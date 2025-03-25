# Collection configuration

> Back to the [Catalogue Page](../catalogue.md)

## Background

**Collections** are defined as FarEarth's method of searching for ingested data, be it input or product, in FarEarth's *Catalogue* as a viewing and inspection tool named a Catalog. The database format of all ingested data is STAC compliant, and therefore any queries directed at the Catalogue via *collections* should be created with that in mind.

* Apart from querying FarEarth's own internal Catalogue storage it is also possible to query outside STAC compliant databases two examples of this would be *element84's* *Copernicus DEM GLO-30* references or the *USGS's* *Landsat Collection 2 L1* products, however there are many more out there . It should be noted that some of these STAC compliant databases do require payment, and are not always free.

* Additionally just a brief overview of FarEarth's storage and searching concepts, all  inter-related to each other and how FarEarth handles data:
    * **Archive**: FarEarth's physical datastore and main storage for all inputs and related product files that are published during processing.
    * **Catalogue**: The application wherein the Archive lives, as well as the front-end GUI from where all data can be queried for and viewed.
    * **Catalog**: A method of grouping collections together, usually by subcription ID or proxied provider.
    * **Collection**: A json blob that queries a STAC compliant database and returns with the search results specified.

## Configuration

Creating a **Collection** occurs on the **COLLECTIONS** page under the **CATALOGUE CONFIG** section of any subscription. 
You do however need to be an **administrator** or **root admin** with a **Catalogue** resource shared to said subscription to have the necessary permissions for creating, editing or deleting a collection. 

* Take note however that if the collection is being created under a *bundled* application such as FarEarth's **Gateway-Bundled** or **Director-Bundled**, a *Catalogue* is part of the overall bundled installation, which does not require specific sharing of said resource to the **farearth** subscription.

* To create a new *collection*, click on the **CREATE COLLECTION** button, for the **New Collection** modal to be displayed. Within this modal a few key fields are displayed that should be filled in by the admin user.

> Defining the contents of the modal:

| Field | Description | Details |
|-------|-------------|---------|
| App | Parent Application | The application under which the collection is being created i.e., *gateway-bundled*, *catalogue* etc. |
| Subscription | Parent subscription | The subscription under which the collection is being created such as the *farearth* subscription |
| ID | Collection ID | The ID value that the admin chooses for the collection to be created under |
| File Name | JSON file name | The actual file name of the collection json file generated. This is prepopulated when entering the *ID*, with the *subscription*.*ID*.*collection*.*json*, however the admin is free to choose what the file name should be, within formatting rules |
| Title | Name of the collection | The actual name of the collection displayed within the Catalogue, under the Catalog section  |
| Description | Collection description | A description of the search results that would be garnered by running the collection |

* After filling out the form with the collection details, and clicking the **CREATE** button a new collection will be generated on the **COLLECTIONS** page, with a default json blob contained within it. This requires further configuration explained below.

> Example of default generated collection json config:

```json
{
    "details": {
        "id": "farearth.test",
        "title": "Test",
        "description": "test description"
    },
    "filter": {
    }
}
```

* There are quite a lot of queryable parameters when searching through FarEarth's Catalogue or from outside sources, via the usage of collections. See below a few examples of collections and their relative format with an explanation to follow.

> Example collections:

```json
{
    "details": {
        "id": "farearth.geni",
        "title": "Geni benchmark datasets",
        "description": "Geni benchmark datasets"
    },
    "filter": {
        "query": {
            "dataset": {
                "eq": "geni-benchmarks"
            }
        }
    }
}
```

```json
{
    "details": {
        "id": "farearth.trubit-1-l1a",
        "title": "TRUBIT-1-l1a",
        "description": "",
        "shareable": true        
    },
    "filter": {
        "query": {
            "productType": {
                "eq": "L1A"
            },
            "spacecraft": {
                "eq": "TRUBIT-1"
            },
            "subscriptionId": {
                "eq": "trueorbit"
            }
        }
    }
}
```

```json
{
    "details": {
        "id": "farearth.cop-dem-glo-30",
        "title": "Copernicus DEM GLO-30",
        "description": "The Copernicus DEM is a Digital Surface Model (DSM) which represents the surface of the Earth including buildings, infrastructure and vegetation"
    },
    "proxy": {
        "sourceId": "e84-aws-v1",
        "sourceTitle": "AWS Earth Search API (v1)",
        "baseUrl": "https://earth-search.aws.element84.com/v1"
    }
}
```

```json
{
    "details": {
        "id": "farearth.landsat-c2l1",
        "title": "Landsat Collection 2 L1 products",
        "description": "Landsat Collection 2 L1 products"
    },
    "proxy": {
        "sourceId": "usgs.landsat-c2l1",
        "sourceTitle": "USGS STAC Server",
        "baseUrl": "https://landsatlook.usgs.gov/stac-server"
    }
}
```

> Collection json file contents with definitions:

| Field | Example Value | Description | Details |
|-------|---------------|-------------|---------|
| filter | query | Search by using | There are multiple available query parameters, that a creator can also link together to create more in depth limited scope searches with. Examples of such query parameters are: |
|        |       |                 | - *productType*: Searching via a specific product type such as *RAW*, *L0*, *L1A*, *L1C*, etc. |
|        |       |                 | - *spacecraft*: Searching via a specific spacecraft ID such as *TRUBIT-1* etc. |
|        |       |                 | - *subscriptionId*: Searching within the constraints of a specific subscription such as *farearth*, *trueorbit* etc. |
| proxy | sourceId, sourceTitle, baseUrl | Proxy search by | Using external data source providers, there are a few required parameters to access their STAC compliant servers namely: |
|  |  |  | - sourceId: This field represents the unique identifier assigned to the particular data source within the STAC Catalog |
|  |  |  | - sourceTitle: This field represents the name associated with the data source |
|  |  |  | - baseUrl: This field represents the endpoint of the STAC API for the particular source |

* As mentioned it is possible to taper the possible search results by adding additional query parameters in a chained fashion, as can be seen in the *TRUBIT-1-l1a*, collection. In this example collection you can see that the query filters via three specific fields, namely: *productType*, *spacecraft*, and *subscriptionId*, which effectively means that all three fields need to be *true* for the relevant results to be displayed within the Catalogue to the user/subscription utilizing the collection.

> Back to the [Catalogue Page](../catalogue.md)