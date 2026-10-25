# Tools, workflow and what I learned

## How the project was built

KuhinjaCAD grew over about three weeks in October 2026 as a hands-on way to learn C#, desktop-application design, 3D graphics and the basics of CNC woodworking software.

**My role:** I defined what the program must do, based on how cabinets are actually built and cut; I decided the priorities, tested every result and steered the direction.
**AI collaboration:** I worked with **Claude Code** (Anthropic's AI coding assistant) as a pair-programming partner — it drafted and refactored much of the code and explained concepts as I went, and I reviewed, tested and corrected the results. Working this way let me build far more than I could have typed alone, and I can explain the architecture and data flow of every part of the program.

**Working practices that kept it reliable**
- Small steps — one feature per session — each followed by a dated backup of the working state.
- A written project log: what was done, what is open, and honestly what was *not yet tested by hand*.
- Built-in self-check modes instead of an external test framework (see [How it works](HOW_IT_WORKS.md)).
- Anything that reaches a real machine — CNC programs, hardware dimensions — is documented as "must be verified"; generated output is never trusted blindly.
- A license and provenance audit before publishing (see [Licenses and compliance](../LICENSES_AND_COMPLIANCE.md)).

## Tools and what they were used for

| Tool | Used for |
|---|---|
| **Visual Studio Code** | Editing, reading diffs, terminal |
| **C# extension** (`ms-dotnettools.csharp`) | IntelliSense, navigation and diagnostics for C# |
| **C# Dev Kit** (`ms-dotnettools.csdevkit`) | Additional C# tooling in VS Code |
| **Claude Code extension** (`anthropic.claude-code`) | AI pair-programming inside VS Code: features, refactoring, explanations, pre-publication review |
| **Rainbow CSV** (`mechatroner.rainbow-csv`) | Reading exported cut-list and nesting CSV files with colored columns |
| **C# compiler `csc.exe`** (part of Windows, .NET Framework 4) | One-click build with no installation and no packages |
| **Windows Forms and GDI+** | All user interface, 2D drawing, printing and print preview |
| **Git and GitHub CLI** | Version control and publishing |
| **Microsoft Print to PDF** | Vector PDF export of drawings and lists |
| **Machine vendor's simulation software** | Checking generated CNC programs before trusting them |

## What I learned

**Programming**
- Structuring a 25,000-line C# desktop application: splitting one large window class by feature, data classes that serialize to XML, and a clean *data → generation → output* pipeline.
- Windows Forms and GDI+ in depth: custom-drawn controls, owner-drawn lists, double buffering, printing and preview, property grids with conditional visibility.
- Building a 3D renderer without libraries: projection, depth buffer, edge extraction, then a Monte Carlo path tracer with an acceleration structure, progressive refinement and denoising on a background thread.
- Algorithms: sheet nesting (guillotine and free placement), polygon clipping and offsetting, formula parsing.
- Writing file formats: DXF, CNC program text.
- Making a UI bilingual without touching the business logic.
- Verification without a test framework: command-line self-check modes and generated screenshots.

**Domain knowledge**
- How cabinets are constructed: panels, edge banding, back panels in grooves, toe kick versus legs, hinge cups and mounting plates, drawer slides, dowel / confirmat / cam-lock joinery.
- How CNC boring and routing machines are programmed: coordinate systems per panel face, tool selection, depth passes, tool-path offsets, and why every program must be simulated first.
- How a cut list, nesting and labels connect a design to a workshop.

**Professional habits**
- Keeping a running log and frequent backups.
- Auditing my own work for licenses and third-party material before publishing.
- Documenting limitations honestly.
