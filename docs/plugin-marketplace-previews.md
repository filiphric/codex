# Remote plugin marketplace previews

Git and npm plugin entries can show descriptions and images before installation,
without downloading the plugin or bundling its skills in the marketplace repository.

Use the existing `interface.shortDescription` and `interface.longDescription` fields
for listing text. The detail page prefers a nonblank long description, then a nonblank
short description, and otherwise keeps the install-required placeholder.

Use `marketplaceAssets` for images stored in the marketplace repository:

```json
{
  "name": "example",
  "source": {
    "source": "git-subdir",
    "url": "https://github.com/example/skills.git",
    "path": "codex-packages/example"
  },
  "interface": {
    "shortDescription": "Code review",
    "longDescription": "Review local changes before opening a pull request."
  },
  "marketplaceAssets": {
    "logo": "./assets/example.png",
    "composerIcon": "./assets/example.png"
  }
}
```

`marketplaceAssets` also supports `logoDark` and `screenshots`. Paths must start with
`./` and remain within the marketplace root, using the same path validation as plugin
assets. The root is the directory containing `.agents/plugins`, `.claude-plugin`, or
`.cursor-plugin`, not the directory containing the catalog JSON file.

These images apply only to remote previews. Existing `interface` asset paths remain
relative to the plugin package and are still omitted from uninstalled remote listings.
The `source` remains the installation and update source. Marketplace images are not
copied into the installed plugin or its fallback manifest; after installation, the
package's manifest supplies the images and descriptions. Skills and other package
details still require installation.
