# MSFS2020 Livery Sources

To be used with the [MSFS2020 Livery Manager](https://github.com/davwheat/MSFS2020-livery-manager).

## Current file format versions

| File format type   | Version |
| ------------------ | :-----: |
| `sourceList`       |    1    |
| `liverySource`     |    1    |
| `aircraftManifest` |    1    |
| `liveryManifest`   |    1    |

## Documentation

### All manifests

| Field           | Type     | Description                                                                                                                                                          |
| --------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `formatVersion` | `number` | **DO NOT EDIT!** This is for internal use in case new manifest formats are released. This will allow backwards-compatibility.                                        |
| `formatType`    | `string` | States what type of manifest the file is. Used to prevent the attempted parsing of files as if they're another manifest type.                                        |
| `humanVersion`  | `string` | The version code displayed to users. This can be whatever you want (even words) but it's recommended to stick with [semver](#semantic-versioning)                    |
| `versionCode`   | `number` | Used by the manager itself to check if an update is available. If the number here is larger than the number held internally, we can assume the file has been updated |

### `sourceList` manifest

| Field          | Type       | Description                                                                                                     |
| -------------- | ---------- | --------------------------------------------------------------------------------------------------------------- |
| `name`         | `string`   | Name of the source list.                                                                                        |
| `description`  | `string`   | Description of the source list.                                                                                 |
| `contributors` | `object[]` | The contributor(s) who compiled the source list. `name` is mandatory, other entries are optional. (See example) |
| `sources`      | `string[]` | A string array of URLs to be parsed as `liverySource`s.                                                         |

<details>
<summary>Full example</summary>

```json
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
      "msfsforums": "davwheat",
      "discord": "MrJeeves#6969"
    }
  ],
  "sources": [
    "https://raw.githubusercontent.com/......./official-megapack.json"
  ]
}
```

</details>

### `liverySource` manifest

| Field               | Type       | Description                                                                                                                 |
| ------------------- | ---------- | --------------------------------------------------------------------------------------------------------------------------- |
| `name`              | `string`   | Name of the livery compilation.                                                                                             |
| `description`       | `string`   | Description of the livery compilation.                                                                                      |
| `contributors`      | `object[]` | The contributor(s) who helped make the liveries in the list. `name` is mandatory, other entries are optional. (See example) |
| `aircraftManifests` | `string[]` | An array of URLs to be parsed as `aircraftManifest`s.                                                                       |

<details>
<summary>Full example</summary>

```json
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
      "msfsforums": "davwheat",
      "discord": "MrJeeves#6969"
    }
  ],
  "aircraftManifests": [
    "https://raw.githubusercontent.com/.../cessna-208b/manifest.json"
  ]
}
```

</details>

### `aircraftManifest` manifest

| Field              | Type                                              | Description                                                                                                     |
| ------------------ | ------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| `aircraft`         | `object: {name: String, package_version: String}` | The aircraft the liveries are to be associated with. Similar to a package's `manifest.json` dependencies entry. |
| `simObjectsFolder` | `String`                                          | The name of the airplane's SimObjects folder.                                                                   |
| `liveries`         | `object[]`                                        | A list of `liveryManifest`s. See example for full documentation.                                                |

#### Critical information about `uniqueId`s

You **MUST** provide a `uniqueId` entry in the `liveries` array. This is used to accurately track the livery in the manager. **This value can NEVER change between livery updates.**

We recommend using a value similar in style to an Android app package ID. In the example below, we've used a structure aimed to prevent conflicts between liveries. This structure is strongly recommended.

Our structure allows for future livery variations to be created in the future at a very low risk of ID collisions.

```
<livery source name>.<original author>.<aircraft>.<livery name>.<variant>

Example:
msfs-megapack.davwheat.cessna-c172sp-as1000.blue.normal
```

<details>
<summary>Full example</summary>

```json
{
  "formatVersion": 1,
  "formatType": "aircraftManifest",
  "humanVersion": "0.1.0",
  "versionCode": 1,
  "aircraft": {
    "name": "asobo-aircraft-c172sp-as1000",
    "package_version": "0.1.57"
  },
  "simObjectsFolder": "Asobo_C172sp_AS1000",
  "liveries": [
    {
      "uniqueId": "msfs-megapack.broomhead123.cessna-c172sp-as1000.blue.normal",
      "name": "BLUE",
      "humanVersion": "0.1.0",
      "versionCode": 1,
      "authors": [
        {
          "name": "broomhead123",
          "discord": "broomhead123#3514",
          "msfsforums": "broomhead123"
        }
      ],
      "manifestURL": "https://raw.githubusercontent.com/.../cessna-c172sp-as1000/blue/liveryManifest.json"
    }
  ]
}
```

</details>

### `liveryManifest` manifest

Coming soon...

## Semantic Versioning

Coming soon...
