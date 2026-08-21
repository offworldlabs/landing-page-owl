# learn.offworldlabs.com

An interactive primer on how RETINA's passive radar "sees" the sky, built from the
[owl-os wiki](https://github.com/offworldlabs/owl-os/wiki/3-Understanding-Node-Data)
science page. One self-contained scrollytelling page: vanilla HTML/CSS/JS, no build
step, no dependencies, matching the `offworldlabs.com` (owl) surface.

## Structure

`index.html` walks top to bottom through the passive-radar story. Each concept that
the wiki illustrates with a static screenshot becomes something you can drive:

**Hero** — bistatic geometry: transmitter → aircraft → node, animated signal paths.

1. **Two antennas, two paths** — drag the aircraft; watch reference vs echo path and
   the extra distance that becomes *range*.
2. **The Doppler effect** — send a source past the observer; wavefronts compress and
   stretch, with a live Hz readout crossing zero at closest approach. A fixed 120°
   surveillance-antenna beam gates the whole thing: outside it the tone, the readout and the echo
   trace all go silent. Two stacked traces compare the unshifted reference against the
   Doppler-shifted echo, with live frequencies (wave spacing exaggerated ~10⁶×).
3. **The delay-Doppler plot** — drag the aircraft *and* its AIM knob; its detection dot
   moves live on the range × Doppler plane. Bistatic Doppler is zero when the velocity is
   perpendicular to the *sum* of the two unit legs (the ellipse normal), **not**
   perpendicular to the node — the cyan "0 Hz flight line" in the scene shows where that
   actually is, and the snap button parks the heading on it.
4. **Max hold, gated by a steerable beam** — a scripted flyby traces the characteristic
   track that crosses 0 Hz at closest approach; sliders reshape it, and the AIM/WIDTH
   knobs (120° by default) decide which parts of the pass get plotted at all. Also
   carries the range-ambiguity/ellipse explanation.
5. **Pinning it down** — the equal-range ellipse clipped to the beam leaves an *arc*, and
   every point on it returns the same range with a heading that reproduces the same
   Doppler. All four figures in this section are the same base picture (`ambiguityScene`),
   so the three resolution methods visibly act on one image: ADS-B laid over the arc,
   a second node's ellipse cutting it, and Two-Tower Triangulation (one node, two towers
   on different frequencies). Each marks one candidate confirmed and crosses out the rest.
6. **Flight Path Doppler Simulator** — draw any flight path on the map, loop the
   simulation, and watch the track paint on a delay-Doppler plot, broken wherever the path
   leaves the beam. A button in the hero skips straight here.

## Conventions

**Axes.** Every delay-Doppler plot on the page uses the same orientation: **range on the
x-axis** (left → right, "how far") and **Doppler on the y-axis** (bottom → top, +300 Hz
at the top). Keep any new plot consistent with that.

**Colour.** Follows the brand guide §8: green/amber for explanatory geometry, the live
map's Doppler gradient (blue → cyan → red) and teal "truth" for genuine detection plots.
Teal also marks "currently inside the beam" on the interactive scenes.

**Naming.** The node has a **reference antenna** (direct signal from the tower, the
*reference signal*) and a **surveillance antenna** (the *surveillance signal*, containing
the echo). "Echo" is fine for the reflected signal itself, but name the antenna that picks
it up wherever it matters. Don't call them ears.

**Shared beam widget.** `makeBeam(svg, node, opts)` builds the steerable wedge used in
sections 4 and 6 — draggable AIM (bearing + reach) and WIDTH knobs, plus `inBeam(p)`.
Pass `bg`/`fg` groups to sandwich other artwork between the wedge and its knobs.

## Deploying the subdomain

The content lives at `/learn/`. Pointing the real `learn.offworldlabs.com` subdomain
at it is a separate DNS/GitHub-Pages step (a `CNAME` DNS record plus Pages config),
not done here.
