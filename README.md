# ARC-AGI Symbolic Reasoning Agent

Standalone Hugo PaperMod website for the ARC-AGI Symbolic Reasoning Agent portfolio case study.

The full implementation lives in a separate ARC-AGI code repository. Update the GitHub link in `hugo.yaml` after the public implementation URL is finalized.

## Local Development

```powershell
hugo server -D
```

## Build

```powershell
hugo --minify
```

## Theme

PaperMod is included as a Git submodule under `themes/PaperMod`.

After cloning:

```powershell
git submodule update --init --recursive
```
