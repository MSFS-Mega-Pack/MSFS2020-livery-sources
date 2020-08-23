# MSFS2020 Livery Sources

To be used with the MSFS2020 Livery Manager.

## Current file format versions

| File format type | Version |
| ---------------- | :-----: |
| sourceList       |    1    |
| liverySource     |    1    |
| aircraftManifest |    1    |
| liveryManifest   |    1    |

## Documentation

### Manifest documentation

#### All manifests

| Field         | Type     | Description                                                                                                                                                          |
| ------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| formatVersion | `number` | **DO NOT EDIT!** This is for internal use in case new manifest formats are released. This will allow backwards-compatibility.                                        |
| formatType    | `string` | States what type of manifest the file is. Used to prevent the attempted parsing of files as if they're another manifest type.                                        |
| humanVersion  | `string` | The version code displayed to users. This can be whatever you want (even words) but it's recommended to stick with [semver](#semantic-versioning)                    |
| versionCode   | `number` | Used by the manager itself to check if an update is available. If the number here is larger than the number held internally, we can assume the file has been updated |

#### sourceList

| Field        | Type       | Description                                                                                                     |
| ------------ | ---------- | --------------------------------------------------------------------------------------------------------------- |
| name         | `string`   | Name of the source list.                                                                                        |
| description  | `string`   | Description of the source list.                                                                                 |
| contributors | `object[]` | The contributor(s) who compiled the source list. `name` is mandatory, other entries are optional. (See example) |
| sources      | `string[]` | A string array of URLs to be parsed as `liverySource`s.                                                         |

<details>
<summary>Full example</summary>

```jsonc
{
  "formatVersion": 1,
  "formatType": "sourceList",
  "humanVersion": "0.1.0",
  "versionCode": 1,
  "name": "Official livery manager source list",
  "description": "A compilation of verified livery sources.",
  "contributors": [
    {
      "name": "David Wheatley",
      "github": "davwheat",
      "twitter": "@davwheat_",
      "msfsforums": "davwheat"
    }
  ],
  "sources": [
    "https://raw.githubusercontent.com/......./official-megapack.json"
  ]
}
```

</details>

#### liverySource

| Field             | Type       | Description                                                                                                                 |
| ----------------- | ---------- | --------------------------------------------------------------------------------------------------------------------------- |
| name              | `string`   | Name of the livery compilation.                                                                                             |
| description       | `string`   | Description of the livery compilation.                                                                                      |
| contributors      | `object[]` | The contributor(s) who helped make the liveries in the list. `name` is mandatory, other entries are optional. (See example) |
| aircraftManifests | `string[]` | An array of URLs to be parsed as `aircraftManifest`s.                                                                       |

<details>
<summary>Full example</summary>

```jsonc
{
  "formatVersion": 1,
  "formatType": "liverySource",
  "humanVersion": "0.1.0",
  "versionCode": 1,
  "name": "The official megapack",
  "description": "The livery megapack you all know and love.",
  "contributors": [
    {
      "name": "David Wheatley",
      "github": "davwheat",
      "twitter": "@davwheat_",
      "msfsforums": "davwheat"
    }
  ],
  "aircraftManifests": [
    "https://raw.githubusercontent.com/.../cessna-208b/manifest.json"
  ]
}
```

</details>

#### aircraftManifest

| Field    | Type                                              | Description                                                                                                     |
| -------- | ------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| aircraft | `object: {name: string, package_version: string}` | The aircraft the liveries are to be associated with. Similar to a package's `manifest.json` dependencies entry. |
| liveries | `object[]`                                        | A list of `liveryManifest`s. See example for full documentation.                                                |

<details>
<summary>Full example</summary>

```jsonc
{
  "formatVersion": 1,
  "formatType": "aircraftManifest",
  "humanVersion": "0.1.0",
  "versionCode": 1,
  "aircraft": {
    "name": "asobo-aircraft-208b-grand-caravan-ex",
    "package_version": "0.1.48"
  },
  "liveries": [
    {
      "name": "DHL",
      "humanVersion": "0.1.0",
      "versionCode": 1,
      "authors": [
        {
          "name": "David Wheatley",
          "github": "davwheat",
          "twitter": "@davwheat_",
          "msfsforums": "davwheat"
        }
      ],
      "manifestURL": "https://raw.githubusercontent.com/.../cessna-208b/dhl/manifest.json"
    }
  ]
}
```

</details>

#### liveryManifest

Coming soon...

## Semantic Versioning

Coming soon...
