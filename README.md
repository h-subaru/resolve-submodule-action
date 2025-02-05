[market:actions:checkout]: https://github.com/marketplace/actions/checkout

# Resolve Submodule by Name

GitHub Action `h-subaru/resolve-submodule-action` provides the SHA-1 ref and relevant metadata for the submodule in the current HEAD.
- Tracks the latest .gitmodules settings, to reduce the hard-coded values in workflow.
- Incorporating with the official action [`actions/checkout`][market:actions:checkout], use the outputs named accodingly in `steps[*].with`. 

