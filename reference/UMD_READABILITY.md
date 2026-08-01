# UMD Readability Profile

The `umd` skin includes a readability profile tuned for 1920x1080 academic slides with plots, captions, and explanatory text on the same page. These defaults are intentionally conservative: text remains readable, figure grids retain a visible boundary, and content is kept above the footer.

## Defaults

The UMD skin sets:

| Setting | Default | Purpose |
|---|---:|---|
| `--body-size` | `42px` | Main body text and bullet baseline |
| `--umd-caption-size` | `22px` | Figure and table captions |
| `.slide-content` padding-bottom | `36px` | Footer-safe content boundary |
| bullet line-height | `1.28` | Readable dense bullets |
| nested bullet line-height | `1.22` | Compact secondary bullets |

## Figure Boundaries

The UMD skin applies these maximum image heights to the standard figure grids:

| Figure grid | Maximum image height |
|---|---:|
| `.fig-1` | `50vh` |
| `.fig-1x2` | `38vh` |
| `.fig-1x3` | `35vh` |
| `.fig-2x2` | `29vh` |
| `.fig-2x3` | `21vh` |

These are image limits, not a requirement to fill the slide. Use the normal `.fig` `--h` knob to tune the grid and preserve captions.

## Mixed Text and Figures

Flex-based `.fig` containers can collapse when long text blocks share the same `.slide-content`. Add `fig-fixed` when the figure row must retain a guaranteed height:

```html
<!-- fig-1x2: 1rowx2cols | --figure-row-height --gap --cap-size -->
<div class="fig fig-1x2 fig-fixed"
     style="--figure-row-height:42vh; --gap:16px; --cap-size:16px;">
    <div class="figure-frame">
        <img src="plots/example_a.png">
        <div class="caption">Example A</div>
    </div>
    <div class="figure-frame">
        <img src="plots/example_b.png">
        <div class="caption">Example B</div>
    </div>
</div>
```

Use `fig-fixed` only when surrounding text is intentionally bounded. For image-only backup slides, the normal flexible `.fig` behavior is preferred.

## Layout Rules

1. Keep the main plot row visible before adding explanatory boxes.
2. Use short callouts below or beside figures instead of large stacked boxes.
3. Reset box margins on dense mixed-content slides when they consume figure space.
4. Keep captions inside the figure boundary; do not place them in the footer area.
5. Run `scripts/bundle-html.py` before web deployment when relative plot paths or symlinks may not be served reliably.

The profile is applied automatically by:

```bash
python3 scripts/init-slides.py --skin umd ...
```
