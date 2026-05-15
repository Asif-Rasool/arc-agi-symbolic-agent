# A Knowledge-Based Agent for ARC-AGI

Standalone Hugo PaperMod website for A Knowledge-Based Agent for ARC-AGI.

Live website: https://asif-rasool.github.io/arc-agi-symbolic-agent/

The full implementation currently lives in a separate ARC-AGI code repository. I may make selected implementation files public after reviewing course and repository-sharing constraints.

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
