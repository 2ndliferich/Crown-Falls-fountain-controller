# Crown Falls Fountain (Horizon Worlds)

> **Prefab-specific controller — not a generic fountain script**

Lightweight controller that animates the two water streams and (optionally) plays looped SFX for the **Crown Falls** fountain prefab included in this project. It’s designed around this prefab’s mesh layout, pivots, and axes and is **not** intended as a drop-in for other fountains.

Creator: **2ndLife Rich (HumAi LLC)**
Engine: **Horizon Worlds TypeScript API (v2.x)**

---

## What it does

* Spins each water stream **around its own world-space center** to fake flowing water.
* Independent **speed** and **reverse** per stream.
* Optional **Audio Gizmo** for ambient waterfall sound (volume/distance/low-pass controlled on the gizmo).

> Implementation notes:
>
> * Stream A (`waterStream1`) is rotated around the **Y** axis.
> * Stream B (`waterStream`) is rotated around the **X** axis.
> * Speeds are treated as **radians per second**.
> * Center is computed from `getRenderBounds().center` with a safe fallback to the entity’s current position.

---

## Compatibility & Scope

* ✅ **Works only with the Crown Falls prefab** provided in this repo/world.
* ❌ **Not plug-and-play** for other fountains or arbitrary meshes without code changes.
* If you change the mesh hierarchy, pivots, or axes, you’ll need to **update the script** accordingly (see “Adapting to other fountains (advanced)” below).

---

## Quick Start (from the in-world editor)

1. **Drop** the **Crown Falls fountain** prefab into your scene.
2. **Select the root** entity (the one with the `crownFallsFountain` script) to open **Props**.
3. **Wire props** (exact names as in the script):

   * `waterStream1` → mesh entity for stream A
   * `waterStream1_speed` → flow rate for stream A (e.g., `0.5`)
   * `waterStream1_reverse` → flip direction for stream A if needed
   * `waterStream` → mesh entity for stream B
   * `waterStream_speed` → flow rate for stream B
   * `waterStream_reverse` → flip direction for stream B
   * `soundFX` (optional) → an **Audio Gizmo** instance
4. If using **soundFX**: select the Audio Gizmo in the hierarchy and set **Volume**, **Min/Max Distance**, and **Low-pass Cutoff** to taste.
5. **Play test**. The streams should “flow” based on the speed/reverse settings.

---

## Props Reference

| Prop                   | Type        | Required | Default | Notes                                       |
| ---------------------- | ----------- | :------: | ------- | ------------------------------------------- |
| `waterStream1`         | Entity      |     ✓    | —       | Stream A mesh entity (expects Y-axis spin). |
| `waterStream1_speed`   | Number      |     —    | `0.5`   | Radians/sec. Typical range `0.1–1.5`.       |
| `waterStream1_reverse` | Boolean     |     —    | `false` | Flip if the visual flow looks backwards.    |
| `waterStream`          | Entity      |     —    | —       | Stream B mesh entity (expects X-axis spin). |
| `waterStream_speed`    | Number      |     —    | `0.5`   | Radians/sec.                                |
| `waterStream_reverse`  | Boolean     |     —    | `false` | Flip direction for stream B.                |
| `soundFX`              | Audio Gizmo |     —    | —       | Optional; looped waterfall SFX.             |

---

## Usage Tips

* **Reverse**: If a stream looks like it’s “climbing” instead of falling, toggle the corresponding `*_reverse`.
* **Pause**: Set a stream’s `*_speed` to `0` to stop it without rewiring.
* **Audio radius**: Start with Min Distance `1–2m`, Max Distance `12–20m` and adjust for your scene scale. Use low-pass to soften at range.

---

## Troubleshooting

* **Nothing moves**
  Ensure the root entity has the `crownFallsFountain` script and that `waterStream1` / `waterStream` are wired to the **mesh entities**, not to a high-level container.
* **Rotates around the wrong point**
  You likely wired a parent container instead of the actual mesh. Wire the child mesh entity used for the stream.
* **Direction looks wrong**
  Toggle `waterStream1_reverse` or `waterStream_reverse`.
* **Audio issues**
  Verify `soundFX` is an **Audio Gizmo**. Adjust Volume and Min/Max Distance on the gizmo itself.

---

## Adapting to other fountains (advanced)

This script hardcodes:

* Stream A axis = **Y**
* Stream B axis = **X**
* The expectation that each stream is an individual **mesh entity** with a sensible render-bounds center.

To retrofit another fountain:

1. **Replicate the Crown Falls hierarchy**: two child mesh entities for the streams, each with predictable bounds and pivots.
2. **Expose axis as props** (optional refactor): replace the hardcoded `'y'` / `'x'` with string props (e.g., `'x' | 'y' | 'z'`) per stream.
3. **Validate bounds**: ensure `getRenderBounds()` returns a center that makes sense (or provide a manual center).
4. **Retune speeds**: meshes with different scale/UVs may require different speed values.

> If you need this to be prefab-agnostic, plan on a small refactor to parameterize axes and (optionally) a manual center override.

---

## Changelog

* **1.0.0** — Initial release for the **Crown Falls** prefab (two streams, per-stream speed & reverse, optional Audio Gizmo, center-pivot rotation).

---

## License & Credit

* Recommended license: **MIT** (remix-friendly).
* Credit: **2ndLife Rich (HumAi LLC)**.

---

## Support

Questions or ideas? Open a GitHub issue for this repo or reach out in-world.
