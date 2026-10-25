# How KuhinjaCAD works

*Conceptual overview. No source code is included in this repository.*

## The core idea

```
 Project
   ├─ Construction settings   thicknesses, joinery, hinge and slide models, toe kick …
   ├─ Room                    walls, doors, windows
   └─ Cabinets                type, width, doors, drawers, free interior subdivision …
            │
            ▼   Part generator   ← the only place that knows how a cabinet is built
        Parts  ── each with ──►  Operations (holes, grooves, pockets, contours)
            │
            ├──► Cut list (CSV / print)
            ├──► Nesting ──► sheet layouts ──► CNC nesting programs
            ├──► CNC post-processor ──► machine program text
            ├──► DXF / PDF drawings, shop drawings
            ├──► Part labels, hardware specification
            └──► 3D scene ──► 3D view, exploded view, path-traced render
```

**Design decision:** there is exactly one component that knows how a cabinet is built. Everything else — elevations, 3D, CNC, cut list, labels — only *reads* the generated parts. A change to, say, the hinge position therefore shows up consistently everywhere, and no number is ever copied by hand.

## Units and coordinates

- All dimensions are stored in millimetres; inches exist only at the input/display edge (including fractions such as `34 1/2"`).
- Fields accept formulas, for example `x/2` or `y-50`, relative to the part being edited.
- On a part, X runs along the length, Y along the width, and Y = 0 is the front edge.

## Notable techniques

- **Parametric construction.** Cabinets are described by a few inputs; options that do not apply are hidden automatically so the property dialog stays short.
- **Free interior subdivision.** A cabinet interior is modelled as a tree of spaces that can be split horizontally, vertically or into a grid; each space then holds open shelving, doors, drawers, an appliance, a hanging rod and so on. The same plan produces the parts, the drilling, the 3D view and the drawing.
- **Nesting.** Two modes: panel-saw nesting (every cut passes through the whole sheet, with saw-blade thickness and edge trim) and CNC nesting (free placement with cutting contours and depth passes). Both support grain matching between neighbouring fronts.
- **Geometry.** Polygon clipping and offsetting produce tool paths for free-form shapes such as the glass "river" inlay, and drilling that would fall into a cut-out zone is flagged or removed.
- **Software 3D.** Everything in the scene is built from boxes. The fast preview uses a depth buffer with edge lines; the realistic render is a Monte Carlo path tracer with an acceleration structure, progressive refinement and noise removal on a background thread, so the window stays responsive.
- **Undo / redo by snapshots.** After each change the whole project is serialized and compared with the previous state; differences go on the undo stack. This is robust against forgetting to record an edit.
- **Localization without risk.** The interface is translated at display time only; internal names used by the logic are never translated.
- **Safety nets for CNC output.** Operations that would break through a visible face are flagged, collisions with cut-outs produce warnings, and the output is always documented as "simulate before use".

## How it was verified

There is no external test framework. Instead the executable has command-line self-check modes that build sample projects, generate every output (parts, CNC text, nesting, 3D images, drawings) into a folder and check invariants — for example, a CNC script that has not been edited must be written back byte-for-byte identical. The screenshots in this repository are produced by the same mechanism, so the documentation is reproducible.

## Possible next steps

Automated unit tests for the part generator, migration to a current .NET version, more interface languages, and verification on a real machine.
