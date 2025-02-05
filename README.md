[market:actions:checkout]: https://github.com/marketplace/actions/checkout

# Resolve Submodule by Name

GitHub Action `h-subaru/resolve-submodule-action` provides the SHA-1 ref and relevant metadata for the submodule in the current HEAD.

😎️ Features
---------

- Tracks the latest .gitmodules settings, to reduce the hard-coded values in workflow.
- Incorporating with the official action [`actions/checkout`][market:actions:checkout], use the outputs named accodingly in `steps[*].with`. 


📑️ Usage
---------

```yaml
inputs:
  name:
    required: true
    description: the submodule name. Found in the section name in .gitmodules.
```

```yaml
outputs:
  path:
    description: the path to the submodule working directory, under the superproject.
    
  ref:
    description: the SHA-1 ref of the commit in the submodule, which the superproject tracks.
    
  repository:
    description: the Git repository name of the submodule.
    
  url:
    description: the Git repository url where to clone the submodule contents from
```

### Example

If you have a .gitmodules in your superproject:

```toml
[submodule "blobcat-server"]
  url = https://github.com/example-user/blobcat-server.git
  path = lib/blobcat-server
  active = true
```

You can write like this:

```yaml:./.github/workflows/your-workflow.yaml
...
jobs:
  checkout-repo:
    steps:
      # (1) Checkout your repository first.
      - name: Checkout main repo
        uses: actions/checkout@v4

      # (2) Find the submodule by `name`.
      - uses: h-subaru/resolve-submodule-action@v1
        # Set step `id` for following steps
        id: server
        with:
          name: blobcat-server

      # (3) Checkout the private repository
      - uses: actions/checkout@v4
        with:
          # `steps.<step-id>.outputs.<output-id>`
          repository: ${{ steps.server.outputs.repository }}
          ref: ${{ steps.server.outputs.ref }}
          path: ${{ steps.server.outputs.path }}
          # specify other keys you need, such as `token`, `ssh_key`, etc......
          token: ${{ secrets.BLOBCAT_SVR_PAT }}
      ...
```

That's it! 🍵️

🙇️ Limitations
----------

- Supports Linux Runners only.

