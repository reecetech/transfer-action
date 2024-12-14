# transfer-action

This action transfers data to/from artefact storage


## Example usage

### Checkout and upload repository

```yaml
  checkout:
    runs-on: [self-hosted]
    steps:
      - name: Upload repo
        uses: reecetech/transfer-action@v2
        with:
          checkout: 'true'
          direction: 'upload'
```

### Download repository

```yaml
  run-on-mac:
    runs-on: [macOS-12]
    needs:
      - checkout
    steps:
      - name: Download repo
        uses: reecetech/transfer-action@v2
        with:
          checkout: 'true'
          direction: 'download'
```

### Upload specific build results

```yaml
      - id: upload
        name: Upload build output
        uses: reecetech/transfer-action@v2
        with:
          direction: 'upload'
          name: 'build-result'
          path: 'dist/'  # omit path to zip & upload everything under `./`
```

### Download specific build results

```yaml
      - name: Download build output
        uses: reecetech/transfer-action@v2
        with:
          direction: 'download'
          name: 'build-result'
          path: 'dist/'  # if not specifed, action would extract to the `./` path
```


## Inputs

<!-- AUTO-DOC-INPUT:START - Do not remove or modify this section -->

|                                            INPUT                                             |  TYPE  | REQUIRED |  DEFAULT  |                                                                                                                                          DESCRIPTION                                                                                                                                          |
|----------------------------------------------------------------------------------------------|--------|----------|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                   <a name="input_checkout"></a>[checkout](#input_checkout)                   | string |  false   | `"false"` |                                                                                                Do a Git checkout before <br>transferring, either: `true` or `false`; <br>defaults to `false`                                                                                                  |
| <a name="input_checkout-fetch-depth"></a>[checkout-fetch-depth](#input_checkout-fetch-depth) | string |  false   |   `"1"`   |                                                                                                    Number of commits to fetch. <br>0 indicates all history for <br>all branches and tags                                                                                                      |
|             <a name="input_checkout-lfs"></a>[checkout-lfs](#input_checkout-lfs)             | string |  false   | `"false"` |                                                                                                                               Whether to download Git-LFS files                                                                                                                               |
|                 <a name="input_direction"></a>[direction](#input_direction)                  | string |   true   |           |                                                                                                                  Direction of transfer, either: `upload` <br>or `download`                                                                                                                    |
|     <a name="input_if-no-files-found"></a>[if-no-files-found](#input_if-no-files-found)      | string |  false   | `"error"` | The desired behavior if no <br>files are found using the <br>provided path. Available Options: warn: <br>Output a warning but do <br>not fail the action error: <br>Fail the action with an <br>error message ignore: Do not <br>output any warnings or errors, <br>the action does not fail  |
|                         <a name="input_name"></a>[name](#input_name)                         | string |  false   |           |                                                                                         Artifact name: defaults to `checkout` <br>if checkout input is `true`, <br>otherwise, please provide a value                                                                                          |
|                         <a name="input_path"></a>[path](#input_path)                         | string |  false   |           |                                          ⚠️ Conditional defaults! - if <br>`checkout` is `true`; then defaults to `./.git/` - if `checkout` is `false`; then <br>defaults to `./`  Additionally, the meaning <br>of `path` is: - if direction <br>is                                           |
|                                                                                              |        |          |           |                                                                          `upload`: a file, directory or wildcard <br>pattern that describes what to <br>upload; - if direction is <br>`download`: destination path                                                                            |

<!-- AUTO-DOC-INPUT:END -->


## Outputs

<!-- AUTO-DOC-OUTPUT:START - Do not remove or modify this section -->

|                     OUTPUT                     |  TYPE  |  DESCRIPTION  |
|------------------------------------------------|--------|---------------|
| <a name="output_name"></a>[name](#output_name) | string | Artifact name |

<!-- AUTO-DOC-OUTPUT:END -->

