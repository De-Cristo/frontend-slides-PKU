# Figure Layout System — Quick Reference

> **Core principle: change a few numbers = control figure position and size**

---

## 1. Knobs (CSS Custom Properties)

Fine-tune any `.fig` container via `style="--variable:value"`:

| Knob | Effect | Example | Default |
|------|--------|---------|---------|
| `--w` | Image width | `--w:80%` | `100%` |
| `--h` | Image height | `--h:35vh` | Per preset |
| `--x` | Horizontal shift | `--x:30px` (right) / `--x:-30px` (left) | `0px` |
| `--y` | Vertical shift | `--y:-20px` (up) / `--y:20px` (down) | `0px` |
| `--gap` | Grid gap | `--gap:8px` | `15px` |
| `--split` | Dual-column ratio | `--split: 1fr 1fr` | `4fr 6fr` |
| `--cap-size` | Caption font size | `--cap-size:20px` | Auto (~17px) |
| `--cap-y` | Caption vertical offset | `--cap-y:-5px` (up) | `0px` |

```html
<!-- fig-1: single image | --w --h --x --y --gap --cap-size --cap-y -->
<div class="fig fig-1" style="--w:80%; --y:-20px;">
    <div class="figure-frame">
        <img src="plot.png">
        <div class="caption">Run 4482, VoV=3V</div>
    </div>
</div>
```

> **Captions are hidden by default**. They only appear when a `<div class="caption">` is placed inside `<div class="figure-frame">`.
> Captions auto-center below the image with adaptive font size. Adjust with `--cap-size` or `--cap-y`.

---

## 2. Preset Layouts (1×1 through 4×4)

### `.fig-1` — Single image
```
┌───────────────────┐
│                   │
│     ┌───────┐     │
│     │  IMG  │     │
│     └───────┘     │
│                   │
└───────────────────┘
```
**HEP use case:** Single fit plot, Landau fit, time resolution comparison

```html
<div class="fig fig-1">
    <img src="fit_result.png">
</div>
```

---

### `.fig-1x2` — 1 row × 2 columns
```
┌─────────┬─────────┐
│         │         │
│  IMG 1  │  IMG 2  │
│         │         │
└─────────┴─────────┘
```
**HEP use case:** Before/After comparison (with/without cut), L/R channel comparison

```html
<div class="fig fig-1x2" style="--h:60vh;">
    <div class="figure-frame"><img src="no_cut.png"><div class="caption">Without cut</div></div>
    <div class="figure-frame"><img src="with_cut.png"><div class="caption">With 78 ADC cut</div></div>
</div>
```

---

### `.fig-1x3` — 1 row × 3 columns
```
┌──────┬──────┬──────┐
│      │      │      │
│ IMG1 │ IMG2 │ IMG3 │
│      │      │      │
└──────┴──────┴──────┘
```
**HEP use case:** Three thresholds / three VoV comparison

```html
<div class="fig fig-1x3" style="--gap:10px;">
    <div class="figure-frame"><img src="th5.png"><div class="caption">th=5</div></div>
    <div class="figure-frame"><img src="th10.png"><div class="caption">th=10</div></div>
    <div class="figure-frame"><img src="th20.png"><div class="caption">th=20</div></div>
</div>
```

---

### `.fig-2x1` — 2 rows × 1 column
```
┌───────────────────┐
│     ┌───────┐     │
│     │ IMG 1 │     │
│     └───────┘     │
│     ┌───────┐     │
│     │ IMG 2 │     │
│     └───────┘     │
└───────────────────┘
```
**HEP use case:** Vertical stack (e.g. singleHit + doubleHit for the same bar)

```html
<div class="fig fig-2x1">
    <img src="single_hit.png">
    <img src="double_hit.png">
</div>
```

---

### `.fig-2x2` — 2 rows × 2 columns
```
┌─────────┬─────────┐
│  IMG 1  │  IMG 2  │
├─────────┼─────────┤
│  IMG 3  │  IMG 4  │
└─────────┴─────────┘
```
**HEP use case:** singleHit/doubleHit × with/without cut (4-panel comparison)

```html
<div class="fig fig-2x2" style="--gap:8px; --h:38vh;">
    <div class="figure-frame"><img src="sh_nocut.png"><div class="caption">SingleHit, no cut</div></div>
    <div class="figure-frame"><img src="sh_cut.png"><div class="caption">SingleHit, with cut</div></div>
    <div class="figure-frame"><img src="dh_nocut.png"><div class="caption">DoubleHit, no cut</div></div>
    <div class="figure-frame"><img src="dh_cut.png"><div class="caption">DoubleHit, with cut</div></div>
</div>
```

---

### `.fig-2x3` — 2 rows × 3 columns (TB classic)
```
┌──────┬──────┬──────┐
│ IMG1 │ IMG2 │ IMG3 │
├──────┼──────┼──────┤
│ IMG4 │ IMG5 │ IMG6 │
└──────┴──────┴──────┘
```
**HEP use case:** 3 thresholds × ±cut 6-panel grid (most common at TB meetings)

```html
<div class="fig fig-2x3" style="--gap:8px;">
    <div class="figure-frame"><img src="th5_nocut.png"><div class="caption">th=5 (no cut)</div></div>
    <div class="figure-frame"><img src="th10_nocut.png"><div class="caption">th=10 (no cut)</div></div>
    <div class="figure-frame"><img src="th20_nocut.png"><div class="caption">th=20 (no cut)</div></div>
    <div class="figure-frame"><img src="th5_cut.png"><div class="caption">th=5 (with cut)</div></div>
    <div class="figure-frame"><img src="th10_cut.png"><div class="caption">th=10 (with cut)</div></div>
    <div class="figure-frame"><img src="th20_cut.png"><div class="caption">th=20 (with cut)</div></div>
</div>
```

---

### `.fig-3x2` — 3 rows × 2 columns
```
┌─────────┬─────────┐
│  IMG 1  │  IMG 2  │
├─────────┼─────────┤
│  IMG 3  │  IMG 4  │
├─────────┼─────────┤
│  IMG 5  │  IMG 6  │
└─────────┴─────────┘
```
**HEP use case:** 6-panel vertical layout (e.g. one plot per bar pair)

```html
<div class="fig fig-3x2" style="--gap:6px;">
    <img src="bar2.png"><img src="bar3.png">
    <img src="bar4.png"><img src="bar5.png">
    <img src="bar6.png"><img src="bar7.png">
</div>
```

---

### `.fig-3x3` — 3 rows × 3 columns (9-panel grid)
```
┌──────┬──────┬──────┐
│ IMG1 │ IMG2 │ IMG3 │
├──────┼──────┼──────┤
│ IMG4 │ IMG5 │ IMG6 │
├──────┼──────┼──────┤
│ IMG7 │ IMG8 │ IMG9 │
└──────┴──────┴──────┘
```
**HEP use case:** 3 VoV × 3 threshold 9-panel grid

```html
<div class="fig fig-3x3" style="--gap:5px;">
    <img src="v1_t1.png"><img src="v1_t2.png"><img src="v1_t3.png">
    <img src="v2_t1.png"><img src="v2_t2.png"><img src="v2_t3.png">
    <img src="v3_t1.png"><img src="v3_t2.png"><img src="v3_t3.png">
</div>
```

---

### `.fig-3x1` — 3 rows × 1 column

```html
<!-- fig-3x1: 3 rows × 1 column | --w --h --x --y --gap -->
<div class="fig fig-3x1">
    <img src="a.png"><img src="b.png"><img src="c.png">
</div>
```

---

### `.fig-4x1` — 4 rows × 1 column

```html
<!-- fig-4x1: 4 rows × 1 column | --w --h --x --y --gap -->
<div class="fig fig-4x1">
    <img src="a.png"><img src="b.png"><img src="c.png"><img src="d.png">
</div>
```

---

### `.fig-4x2` — 4 rows × 2 columns

```html
<!-- fig-4x2: 4 rows × 2 columns | --w --h --x --y --gap -->
<div class="fig fig-4x2" style="--gap:6px;">
    <img src="1.png"><img src="2.png">
    <img src="3.png"><img src="4.png">
    <img src="5.png"><img src="6.png">
    <img src="7.png"><img src="8.png">
</div>
```

---

### `.fig-4x3` — 4 rows × 3 columns

```html
<!-- fig-4x3: 4 rows × 3 columns | --w --h --x --y --gap -->
<div class="fig fig-4x3" style="--gap:5px;">
    <!-- 12 images -->
</div>
```

---

### `.fig-1x4` — 1 row × 4 columns

**HEP use case:** Four thresholds / four VoV horizontal comparison

```html
<!-- fig-1x4: 1 row × 4 columns | --w --h --x --y --gap -->
<div class="fig fig-1x4" style="--gap:10px;">
    <img src="a.png"><img src="b.png"><img src="c.png"><img src="d.png">
</div>
```

---

### `.fig-2x4` — 2 rows × 4 columns

```html
<!-- fig-2x4: 2 rows × 4 columns | --w --h --x --y --gap -->
<div class="fig fig-2x4" style="--gap:8px;">
    <!-- 8 images -->
</div>
```

---

### `.fig-3x4` — 3 rows × 4 columns

```html
<!-- fig-3x4: 3 rows × 4 columns | --w --h --x --y --gap -->
<div class="fig fig-3x4" style="--gap:6px;">
    <!-- 12 images -->
</div>
```

---

### `.fig-4x4` — 4 rows × 4 columns (16-panel grid)

```html
<!-- fig-4x4: 4 rows × 4 columns | --w --h --x --y --gap -->
<div class="fig fig-4x4" style="--gap:5px;">
    <!-- 16 images -->
</div>
```

---

## 3. Combining with `.dual-layout`

### `--split` variable controls left-right ratio

```html
<!-- Default 4:6 (left text, right image) -->
<div class="dual-layout">
    <div class="left-col">bullets...</div>
    <div class="right-col">
        <div class="fig fig-1"><img src="plot.png"></div>
    </div>
</div>

<!-- Equal split -->
<div class="dual-layout" style="--split: 1fr 1fr;">...</div>

<!-- Left wider, right narrower -->
<div class="dual-layout" style="--split: 6fr 4fr;">...</div>
```

---

## 4. Caption Styling

Each `.figure-frame` can optionally include a `.caption`:

```html
<div class="figure-frame">
    <img src="plot.png">
    <div class="caption">Run 4482, VoV=3V, th=10</div>
</div>
```

Captions auto-inherit `calc(var(--body-size) * 0.5)` font size, centered gray text.

---

## 5. AI Generation Rule: Inline Comment Required

> **⚠️ MANDATORY**: When generating any HTML containing `.fig`, the AI **must** add a comment above `<div class="fig ...">` in this format:
> ```html
> <!-- fig-RxC: R rows × C columns | --w --h --x --y --gap --cap-size --cap-y -->
> ```
> This makes it immediately clear to users reading the source what values can be adjusted.

---

## 6. Quick Combo Reference

| Scenario | Syntax |
|----------|--------|
| Full-width single image | `<div class="fig fig-1"><img src="..."></div>` |
| Single image at 80% width | `<div class="fig fig-1" style="--w:80%;"><img src="..."></div>` |
| Single image shifted up 20px | `<div class="fig fig-1" style="--y:-20px;"><img src="..."></div>` |
| Left-right comparison | `<div class="fig fig-1x2">` |
| 6-panel TB grid | `<div class="fig fig-2x3" style="--gap:8px;">` |
| 4-column horizontal | `<div class="fig fig-1x4">` |
| Left text, right image (equal) | `<div class="dual-layout" style="--split: 1fr 1fr;">` |
| Limit image height to 35vh | Add `style="--h:35vh;"` |
| Enlarge caption font | Add `style="--cap-size:24px;"` |
| Shift caption upward | Add `style="--cap-y:-5px;"` |

---

## 7. Backward Compatibility

Legacy `.image-grid` and hand-written inline styles still work perfectly. The `.fig` system is an **addition** — it does not modify any existing CSS.
