# API configuration and use

> Back to the [Developer Page](../developer.md)

## Obtaining an API key

1. Navigate to the USERS menu.
2. Click on your user's email address
3. Click on the create button to generate an API key
4. If you would like to remove access for an API key, click the remove button

## Testing access

Perform the following curl call to verify the API key works:

```bash
curl -H "Content-Type: application/json" \
  -H "X-API-Key: O5t...qm0" \
  -X GET https://gateway.farearth.space/api/ext/v1/test/hello
```

## API documentation

Using the FarEarth side menu, navigate to DEVELOPER -> API. This page provides an interface to explore the available end-points and options available. The page also allows a user to enter his/her API key to test the calls inline.

## OpenAPI schemas

A OpenAPI JSON schema file is available at https://gateway.farearth.space/api/public/api-schema/subscription to allow an end-user to generate his/her own API integration code.

## STAC access

A user can also directly interact with the FarEarth Catalogue by using [PySTAC](https://github.com/stac-utils/pystac)

```python
import os
import urllib

FE3_API_URL=R"https://gateway.farearth.space/api/ext/v1/stac/catalogs/farearth.gateway-bundled/farearth.gateway-bundled"

if __name__ == "__main__":

    catalog = Client.open(
        url=FE3_API_URL,
        headers={
            'X-API-Key': os.environ['FE3_API_KEY']
        }
    )

    # Get all the collections that the API key has access to
    collections = catalog.get_collections()

    for collection in collections:
        print(collection)
        # Use the last specified collection
        specific_collection_name = collection.id

    # Get an object representing a specific collection
    specific_collection = catalog.get_collection(specific_collection_name)

    search = catalog.search(
        max_items=30,
        limit=3,
        collections=[specific_collection],
        bbox=[8.518128, 3.663501, 42.038028, -35.811674],
    )

    print(f"{search.matched()} items found")

    for item in search.items():

        # Download thumbnails (previews) if they are available
        if 'THUMB_RGB' in item.assets:
            urllib.request.urlretrieve(item.assets["THUMB_RGB"].href, f"{item.id}_PREVIEW.png")

        # Alternatively, you can download an asset based on its role
        for key, value in item.assets.items():
            if value.roles == 'metadata':
                urllib.request.urlretrieve(item.assets[key].href, f"{item.id}_META.json")
```

## More examples

Also refer to the Git repository at https://github.com/pinkmatter/farearth-api-examples for more examples.

> Back to the [Developer Page](../developer.md)