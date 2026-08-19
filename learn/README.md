# learn.offworldlabs.com

An interactive primer on how RETINA's passive radar "sees" the sky, built from the
[owl-os wiki](https://github.com/offworldlabs/owl-os/wiki/3-Understanding-Node-Data)
science page. One self-contained scrollytelling page: vanilla HTML/CSS/JS, no build
step, no dependencies, matching the `offworldlabs.com` (owl) surface.

## Structure

`index.html` walks top to bottom through the passive-radar story. Each concept that
the wiki illustrates with a static screenshot becomes something you can drive:

1. **Bistatic geometry** (hero) — transmitter → aircraft → node, animated signal paths.
2. **Two antennas, two paths** — drag the aircraft; watch reference vs echo path and
   the extra distance that becomes *range*.
3. **The Doppler effect** — move a source past the observer; wavefronts compress and
   stretch, with a live Hz readout crossing zero at closest approach.
4. **The delay-Doppler plot** — drag the aircraft and its velocity; its detection dot
   moves live on the Doppler × range plane.
5. **10-second max hold** — a scripted flyby traces the characteristic track that
   crosses 0 Hz at closest approach; sliders reshape it.
6. **Range ambiguity** — one range is a whole circle; a directional antenna narrows it
   to an arc.
7. **Resolving it** — ADS-B truth subtraction, two-node triangulation, and a note on
   the planned multi-tower method.

## Colour convention

Follows the brand guide §8: green/amber for explanatory geometry, the live map's
Doppler gradient (blue → cyan → red) and teal "truth" for genuine detection plots.

## Deploying the subdomain

The content lives at `/learn/`. Pointing the real `learn.offworldlabs.com` subdomain
at it is a separate DNS/GitHub-Pages step (a `CNAME` DNS record plus Pages config),
not done here.
