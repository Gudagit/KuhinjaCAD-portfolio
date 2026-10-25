# Licenses and compliance

Audit date: 24 October 2026. Author: Ivana.

## 1. Ownership of this repository

- All text and screenshots in this repository were created by the author. The screenshots show only the author's own program (with a demo project that contains no real customer data) and standard Windows window frames.
- License: **All rights reserved** (see [LICENSE](LICENSE)). The repository contains **no source code**; the software is proprietary and private.
- The software was developed with the help of an AI coding assistant (Claude Code). Use of its output is governed by Anthropic's terms of service, which should be re-read when the project is commercialized.

## 2. Third-party code and assets in the software

A source audit of the whole code base found:

| Check | Result |
|---|---|
| Third-party source files, copied snippets, copyright headers of other authors | None |
| NuGet / external libraries / DLLs | None — only the .NET Framework assemblies that ship with Windows |
| Bundled fonts, icons, images, sounds | None — the program uses Windows system fonts only |
| Network access, telemetry, accounts | None — the program works fully offline |
| Personal or customer data in code or documentation | None |

The program is compiled with the C# compiler that is part of Windows (.NET Framework 4); the .NET Framework is a Microsoft component used under the Windows license and is **not redistributed**.

## 3. Tools used (not distributed with the project)

| Tool | License (as understood on the audit date — verify before commercial use) |
|---|---|
| Visual Studio Code | Microsoft Software License Terms (free for personal and commercial use); built from the open-source "Code – OSS" project (MIT) |
| C# extension | Open source (MIT) source code on GitHub; distributed through the VS Marketplace under Microsoft's terms |
| C# Dev Kit | Microsoft Software License Terms; per Microsoft's documentation free for individuals, academic use and open-source development, with commercial teams covered by Visual Studio subscriptions — see [Microsoft's FAQ](https://code.visualstudio.com/docs/csharp/cs-dev-kit-faq) |
| Claude Code (extension) | Anthropic's terms of service |
| Rainbow CSV | MIT |
| Git | GPL-2.0 (used as a tool; not redistributed) |
| GitHub CLI | MIT |

## 4. Material deliberately left out

To keep everything clean, the following were **removed from the project and its backups** or never published:

- Machine-vendor project templates and tool-library files (they contain the vendor's proprietary machine configuration) — the feature that depended on them was removed from the program.
- Sample CNC files from other people's software and workplace.
- A texture image of unknown origin embedded in a demo project.
- Machine-specific tool tables — replaced by generic router-bit defaults.
- Customer or workplace data.

## 5. Trademarks and compatibility

Product and company names that appear in documentation or software descriptions (for example hardware, machine and software brands, Windows, Zebra, AutoCAD) are trademarks of their respective owners and are used only to describe compatibility. This project is not affiliated with, endorsed by, or sponsored by any of them. File formats (DXF and machine program text) were implemented for interoperability from publicly observable plain-text samples; no vendor code or documentation is included.

## 6. Safety disclaimer

The program is a learning and portfolio project. Hardware dimensions are starting values to be checked against manufacturer catalogues, and every generated CNC program must be simulated in the machine's own software before cutting material.

## 7. Checklist for publishing

- [x] Source code audited for third-party code, assets and personal data
- [x] Vendor and third-party files removed
- [x] Proprietary "all rights reserved" license, with clear statement that no code is published
- [x] Trademark and non-affiliation notice
- [x] Safety disclaimer
- [x] Tool licenses listed
- [x] No source code in the public repository
