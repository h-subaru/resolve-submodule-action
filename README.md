[market:actions:checkout]: https://github.com/marketplace/actions/checkout

# Resolve Submodule by Name

GitHub Action `h-subaru/resolve-submodule-action` provides the SHA-1 ref and relevant metadata for the submodule in the current HEAD.
- Tracks the latest .gitmodules settings, to reduce the hard-coded values in workflow.
- Incorporating with the official action [`actions/checkout`][market:actions:checkout], use the outputs named accodingly in `steps[*].with`. 


Usage
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
