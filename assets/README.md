> 🌐 **Language:** [🇻🇳 Tiếng Việt](./README_vi.md) · 🇬🇧 English (current) · [🇯🇵 日本語](./README_ja.md)

# Images for extensions with a private repository

## What this folder is for
Some GP247 extensions (templates, paid plugins) keep their source in a **private** repository. Their README is still shown publicly,
for example on the product page at gp247.net — but images stored in a private repository cannot be loaded by visitors.
So the images of those extensions live here, and the extension's README links straight to them.

This folder holds **images only** (screenshots on sample data, logos) — no source code and no documentation.

## Conventions
| Item | Convention |
| --- | --- |
| Path | `assets/<RepoName>/<image-name>` — `<RepoName>` is the extension's repository name, e.g. `assets/GP247MKP/home.jpg` |
| Link in the README | `https://raw.githubusercontent.com/gp247net/gp247-docs/main/assets/<RepoName>/<image-name>` |
| Image content | Sample data only: no customer data, licenses, keys or real server addresses |
| Changing an image | Replace the file here together with the copy in the extension's repository; keep the file name so existing links keep working |

## List
| Folder | Extension |
| --- | --- |
| [GP247MKP](./GP247MKP/) | GP247MKP template — Marketplace |
