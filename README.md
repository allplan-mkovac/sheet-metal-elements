# Klempířské výrobky / Sheet Metal Products

**User Manual — Allplan 2026**

This tool creates 3D sheet-metal elements by extruding a cross-section profile along a polyline path you draw directly in the model.  Typical applications include flashings, copings, gutters, fascia panels, sill trims, and similar sheet-metal components.

---

## What the tool does

- You draw a path (a series of points) along any wall, roof edge, or other 3D line in the model.
- The tool sweeps a sheet-metal profile (loaded from the symbol library) along that path and produces a solid 3D body.
- A 2D plan view is generated automatically.
- After placement you can drag handles directly in the viewport to adjust the path, offsets, and joint angles — without touching the palette.

---

## Prerequisites

- **Allplan 2026** must be installed.


---

## What you can control

- **Profile shape** — choose any cross-section from the symbol library.
- **Angled / mitered ends** — rotate the cut at the start or end of the path independently to create clean miter joints.
- **Start / end setback** — pull the start or end of the element back from the path endpoint by a set distance.
- **Closed path** — join the ends for continuous elements such as gutters around a roof perimeter.
- **Profile position** — choose from 10 reference points (corners, edge midpoints, centre) to control how the profile sits on the path, with additional X/Y offsets.
- **Mirror** — flip the profile left-to-right.
- **Surface material** — assign an Allplan surface texture.
- **IFC data** — fill in IFC entity, type, and custom attributes.

---

## Placing the element

1. Start the tool from the Allplan toolbar or the library.
2. The palette opens on the right. Choose a profile symbol and set your options.
3. Click **Confirm** (or press Enter) to begin drawing the path.
4. **Click** in the model to place path points one by one. A 3D preview follows the cursor.
5. **Double-click** the last point (or press Enter) to finish — the element is placed immediately.

> **Tip:** The first point you click becomes the anchor point of the element. All subsequent path points are stored relative to it, so the element moves correctly when you use the Allplan Move or Copy commands.

---

## Editing after placement

Click the element to select it and enter modification mode. You can then:

| Action | How |
|--------|-----|
| Move a path point | Drag the square vertex handle |
| Add a new path point | Drag the round mid-segment handle |
| Delete a path point | **Shift + click** a vertex handle |
| Change start / end setback | Drag the arrow handle at the path end |
| Change the miter angle | Drag the arc handle at the path end |
| Switch between endpoint and offset handles | Click the checkbox handle next to the path end |
| Change any other setting | Edit the palette and confirm |

The 3D solid updates live as you drag handles.

---

## Palette reference

### Profile geometry

| Setting | Description |
|---------|-------------|
| **Symbol** | The cross-section profile. Click the folder button to browse the library and pick a `.sym` file. |
| **Reference point** | Which point of the profile bounding box is placed on the path. Use the 3×3 grid button to pick a corner, edge midpoint, or centre. |
| **Offset X / Y** | Fine-tune the profile position sideways (X) or up/down (Y) relative to the path. |
| **Mirror profile** | Tick to flip the profile left-to-right. Useful when the same profile is used on opposite sides of a building. |
| **Polygonization length** | Controls the smoothness of curved profiles (arcs, rounded corners). Decrease this value for smoother curves; the default 100 mm is adequate for most use cases. |

### Path geometry

| Setting | Description |
|---------|-------------|
| **Closed path** | Tick to close the path into a loop (e.g. a gutter running all the way around a roof). When active, the start/end settings below are ignored. |
| **Start offset** | How far to pull the element back from the start of the path. Useful when two elements meet at a corner and you do not want them to overlap. |
| **Start angle horizontal** | Rotate the start face of the element to create an angled miter joint. Range: −89° to +89°. |
| **End offset** | How far to pull the element back from the end of the path. |
| **End angle horizontal** | Rotate the end face to create an angled miter joint. |

> **Note:** The start/end offset and angle handles are only visible in the viewport when both offsets are zero. Tick **Switch endpoint/offset handles** (or use the checkbox handle in the viewport) to toggle between editing the path endpoints and editing the offsets/angles.

### Format

| Setting | Description |
|---------|-------------|
| **Common properties** | Pen, colour, layer — same as any other Allplan element. |
| **Surface** | Surface material / texture shown in the 3D view and rendering. |

### Attributes

| Setting | Description |
|---------|-------------|
| **Description** | Free text description of the element (Allplan attribute 1448). |
| **IFC predefined type** | IFC classification for export. |
| **IFC entity** | IFC entity class for export. |
| **Attribute set category / object** | Allplan attribute set fields. |
| **Attributes** | Open list — add any Allplan attribute you need. |

---

## Automatically filled attributes

When the element is placed (or updated), the following attributes are written automatically and are visible in the Allplan attribute inspector:

| Attribute | Content |
|-----------|---------|
| Length (attr 220) | Total developed length of the path in metres, including any start/end setbacks and miter extensions. |
| Symbol name (attr 507) | File name of the profile symbol used. |

---

## Profile library

Profiles are `.sym` files stored in the Allplan library under `allplan-cz\profiles\`.
Any symbol containing **lines, polylines, arcs, or splines** works as a profile — the tool traces their outline and uses it as the cross-section.

If a symbol cannot be loaded (e.g. the file has been moved or renamed), the tool falls back to a plain 200 × 20 mm rectangle so you can still see the element in the model. Check the symbol path in the palette if the shape looks wrong.

---

## Language support

The palette and handle labels are available in:

| Language | File |
|----------|------|
| English | `Klempirske_eng.xml` |
| Czech | `Klempirske_tch.xml` |
| German | `Klempirske_deu.xml` |

The correct language is selected automatically based on your Allplan language setting.

---

## Tips and known behaviour

- The path needs **at least 2 points**. The element appears as soon as you confirm the second point.
- **Miter angles** can be set between −89° and +89°. A 90° angle is not possible (it would produce a zero-thickness edge).
- When **Closed path** is active, start/end offsets and miter angles have no effect.
- The 2D plan outline is regenerated when you finish editing. It is not updated while you are actively dragging a handle, to keep the viewport responsive.
- If the geometry cannot be computed (e.g. a very tight path with a large miter angle), the angled cuts are disabled automatically and a straight-ended element is shown instead. A message is printed to the Allplan report window. Adjust the path or reduce the miter angle to restore the cuts.
