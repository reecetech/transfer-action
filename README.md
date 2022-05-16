# transfer-action

This action transfers data to/from artefact storage


## Example usage

### Checkout and upload repository

```yaml
  checkout:
    runs-on: [self-hosted]
    steps:
      - name: Upload repo
        uses: reecetech/transfer-action@v1
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
        uses: reecetech/transfer-action@v1
        with:
          direction: 'download'
          name: 'checkout'
```

### Upload specific build results

```yaml
      - id: upload
        name: Upload build output
        uses: reecetech/transfer-action@v1
        with:
          direction: 'upload'
          name: 'build-result'
          path: 'dist/'  # omit path to zip & upload everything under `./`
```

### Download specific build results

```yaml
      - name: Download build output
        uses: reecetech/transfer-action@v1
        with:
          direction: 'download'
          name: 'build-result'
          path: 'dist/'  # if not specifed, action would extract to the `./` path
```


## Inputs

<!-- AUTO-DOC-INPUT:START - Do not remove or modify this section -->

|        INPUT         |  TYPE  | REQUIRED |  DEFAULT  |                                                                                                                                       DESCRIPTION                                                                                                                                        |
|----------------------|--------|----------|-----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| checkout             | string | false    | `"false"` | Do a Git checkout before<br>transferring, either: `true` or `false`;<br>defaults to `false`                                                                                                                                                                                              |
| checkout-fetch-depth | string | false    | `"1"`     | Number of commits to fetch.<br>0 indicates all history for<br>all branches and tags                                                                                                                                                                                                      |
| checkout-lfs         | string | false    | `"false"` | Whether to download Git-LFS files<br>                                                                                                                                                                                                                                                    |
| direction            | string | true     |           | Direction of transfer, either: `upload`<br>or `download`                                                                                                                                                                                                                                 |
| if-no-files-found    | string | false    | `"error"` | The desired behavior if no<br>files are found using the<br>provided path. Available Options: warn:<br>Output a warning but do<br>not fail the action error:<br>Fail the action with an<br>error message ignore: Do not<br>output any warnings or errors,<br>the action does not fail<br> |
| name                 | string | false    |           | Artifact name: defaults to `checkout`<br>if checkout input is `true`,<br>otherwise, please provide a value<br>                                                                                                                                                                           |
| path                 | string | false    | `"./"`    | Defaults to `./` - additionally,<br>the meaning of `path` is:<br>if direction is `upload`: a<br>file, directory or wildcard pattern<br>that describes what to upload;<br>if direction is `download`: destination<br>path                                                                 |

<!-- AUTO-DOC-INPUT:END -->


## Outputs

<!-- AUTO-DOC-OUTPUT:START - Do not remove or modify this section -->

| OUTPUT |  TYPE  |  DESCRIPTION  |
|--------|--------|---------------|
| name   | string | Artifact name |

<!-- AUTO-DOC-OUTPUT:END -->

