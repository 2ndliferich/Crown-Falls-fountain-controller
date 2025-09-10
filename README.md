# Crown Falls Fountain (Horizon Worlds)

A lightweight controller that animates two water streams and (optionally) plays a looped waterfall SFX.
Attach it to the fountain root, wire the props, set speeds (and reverse, if needed), and you’re done.

**Creator:** 2ndLife Rich (HumAi LLC)
**Engine:** Horizon Worlds TypeScript API (v2.x)

---

## What it does

* Rotates each water stream around its **own world-space center** to create a natural flowing illusion.
* Independent **speed** and **reverse** per stream.
* Optional **Audio Gizmo** for ambient waterfall sound (tune on the gizmo itself).

---

## Quick Start

1. **Add the fountain** to your scene (it appears in the hierarchy).
2. **Select the fountain root** (the entity with the `crownFallsFountain` script) to open **Props**.
3. **Wire these props:**

   * `waterStream1` → first water stream mesh entity
   * `waterStream1_speed` → flow rate (e.g., `0.5`)
   * `waterStream1_reverse` → flip direction if needed
   * `waterStream` → second water stream mesh entity
   * `waterStream_speed` → flow rate for stream 2
   * `waterStream_reverse` → flip direction for stream 2
   * `soundFX` *(optional)* → drag in an **Audio Gizmo** instance
4. **If using sound:** click the Audio Gizmo in the hierarchy and set **Volume**, **Min/Max Distance**, and **Low-pass Cutoff** to fit your space.
5. **Play test.** The streams should “flow” immediately based on your speed/reverse settings.

---

## Props Reference

| Prop                   | Type        | Required | Default | Notes                                                  |
| ---------------------- | ----------- | :------: | ------- | ------------------------------------------------------ |
| `waterStream1`         | Entity      |     ✓    | —       | Mesh entity for stream 1.                              |
| `waterStream1_speed`   | Number      |     —    | `0.5`   | Radians/sec. Typical range `0.1–1.5`.                  |
| `waterStream1_reverse` | Boolean     |     —    | `false` | Flip direction if the flow looks wrong.                |
| `waterStream`          | Entity      |     —    | —       | Mesh entity for stream 2.                              |
| `waterStream_speed`    | Number      |     —    | `0.5`   | Radians/sec.                                           |
| `waterStream_reverse`  | Boolean     |     —    | `false` | Flip direction for stream 2.                           |
| `soundFX`              | Audio Gizmo |     —    | —       | Optional looped waterfall SFX. Configure on the gizmo. |

> Implementation detail: rotation step is `speed * dt` each frame around the stream’s **local axis** and the mesh’s **render-bounds center**.
> (In code, stream 1 spins on **Y**, stream 2 on **X**.)

---

## Usage Tips

* **Reverse toggles:** If a stream looks like it’s “climbing,” set its `*_reverse` to `true`.
* **Pause a stream:** Set its `*_speed` to `0`.
* **Audio tuning:** Start with Min Distance `1–2 m`, Max Distance `12–20 m`, then adjust to taste. A mild **low-pass** at distance makes the SFX feel more natural.

---

## Troubleshooting

* **Nothing moves:** Confirm the root has the `crownFallsFountain` script and that `waterStream1` / `waterStream` are wired to the **mesh entities**, not a parent container.
* **Weird rotation pivot:** You probably wired a container. Wire the **actual mesh entity** used for the visual stream.
* **Flow looks backwards:** Toggle `waterStream1_reverse` or `waterStream_reverse`.
* **Audio issues:** Ensure `soundFX` is an **Audio Gizmo**, and adjust Volume/Min/Max Distance/Low-pass on the gizmo.

---

## Changelog

* **1.0.0** — Two streams; per-stream speed & reverse; center-pivot rotation; optional Audio Gizmo.

---

## License & Credit

* **License:** MIT (recommended for remix-friendly use)
* **Credit:** 2ndLife Rich (HumAi LLC)
