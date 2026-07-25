# NOTICE — attribution and licence

3D anatomical geometry adapted from **Z-Anatomy** by Gauthier Kervyn and Marcin Zielinski,
licensed **CC BY-SA 4.0**, itself adapted from **BodyParts3D** © Database Center for Life
Science (DBCLS), licensed **CC BY-SA 2.1 Japan**.

Veast has modified the meshes (polygon reduction, selective face removal, curve-to-mesh
conversion, renaming). **Modified geometry is made available under CC BY-SA 4.0 in this
repository.**

- Licence: CC BY-SA 4.0 — https://creativecommons.org/licenses/by-sa/4.0/legalcode
- Upstream: Z-Anatomy — https://www.z-anatomy.com/
- Upstream of upstream: BodyParts3D / DBCLS — https://dbcls.rois.ac.jp/

Per CC BY-SA 4.0 §3(a)(1)(B), both limbs are addressed: Veast's modifications are indicated
above, **and** the prior modification by Z-Anatomy (which itself adapted BodyParts3D) is
retained and indicated.

## Scope

This notice covers the six `.glb` meshes in `meshes/`. It does **not** cover Veast
application source, written anatomical content, or artwork, none of which is in this
repository.

## Status of the §3(b) condition

**Corrected 2026-07-24 — an earlier version of this file described §3(b) as a standing
"duty to publish". It is not.** Verified against the legal code: §3(b) opens *"**If** You
Share Adapted Material You produce, the following conditions also apply"*. It **conditions
sharing; it never compels it.** A private repository triggers nothing.

What matters is therefore not this repository's visibility on its own, but whether Veast
Shares Adapted Material. "Share" is defined in §1(k) to include distribution and public
display. **Shipping the app to users does that** — both the streamed `.glb` meshes and the
rendered stills derived from them are Adapted Material reaching the public. At that moment
§3(b) attaches and three conditions apply:

- **§3(b)(1)** — licence our adapted material under BY-SA 4.0 or a compatible licence.
  Satisfied by `LICENSE` in this repository.
- **§3(b)(2)** — include the text of, or a URI for, that licence. Satisfied by `LICENSE`
  (full legal code) plus the URI above.
- **§3(b)(3)** — apply no additional terms and **no Effective Technological Measures** that
  restrict the granted rights.

**§3(b)(3) is the only genuinely unsettled one, and it is why publishing this repository
still matters.** App Store FairPlay encrypts the shipped binary. Whether that counts as a
barred ETM over Adapted Material inside it is an open question with no case law. Publishing
the meshes through an unencumbered channel is the standard practitioner mitigation: the
material stays freely obtainable regardless of what the store does to the binary. So making
this repository public is not a licence *duty* — it is the cheapest way to make §3(b)(3)
moot rather than argued.

**Timing is the real constraint.** §6(a) terminates the licence automatically on
non-compliance and §6(b)(1) reinstates it only *prospectively*, as of the date the violation
is cured. Distribution that happens while non-compliant is not retroactively fixed. So this
must be settled **before the first build reaches users — TestFlight and OTA included**, not
merely before public launch.

Remaining counsel question, now narrowed to one: does App Store FairPlay constitute a barred
ETM under §3(b)(3) for Adapted Material inside the binary? (§4 Sui Generis Database Rights
was also checked and is not a separate exposure — §4(b) requires only §3(a) attribution on
sharing, which the in-app Credits screen already provides.)

## Anatomical honesty

Z-Anatomy is a **single male donor** dataset. Where a Veast plane renders this geometry, the
app must say so rather than implying the figure is the viewer's own body. Structures shown
are common to both sexes for Fascia, Muscular, Circulatory and Neural. Skeletal and Visceral
carry sex-specific structures and are male-derived; this is disclosed in-app and tracked by
spec phase **PL-8**. The male mesh must never be morphed toward female proportions —
that fabricates anatomy while still looking like real CT data.
