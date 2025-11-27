# Action - Semantic Versioning
Calculate a [semantic version](https://semver.org/) using [GitVersion](https://gitversion.net/docs/). The version calculated will be based on the tags and git history.

## Usage
You can use your own configuration file as in the example below, or you can just use a plain version of the action to quickly generate a simple version.

Using the default and below configuration you can bump the major version by creating a commit message like this.

```
git commit -am "+semver: major | Update to node 21"
```

### Outputs

| Name | Example |
| --- | --- |
| Major | 0, 1, 2, 3 |
| FullSemVer | 1.0.0, 0.3.0-alpha.2, 0.3.0-feat-add-kitties.0 |

### Examples
Basic usage of the composite action without any parameters.

``` yaml
jobs:
  versioning:
    name: Determine
    uses: suspectsoftware/action-semantic-versioning/.github/workflows/main.yml@v1
```

This example shows how to implement the action with a custom configuration and use the output.

``` yaml
jobs:
  versioning:
    name: Determine
    uses: suspectsoftware/action-semantic-versioning/.github/workflows/main.yml@v1
    with:
      configFilePath: .github/gitversion.yml

  Build:
    runs-on: ubuntu-latest
    needs: 
      - Versioning
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Print
        run: |
          echo ${{ needs.Versioning.outputs.Major }}
```
