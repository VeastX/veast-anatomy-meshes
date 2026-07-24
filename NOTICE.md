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

## Status of the §3(b) obligation

Publishing this repository publicly is what discharges the CC BY-SA §3(b) duty to make
modified material available. That step is tracked as spec phase **PL-1** and is gated on
counsel review of two open questions:

1. Whether distributing *renders* of modified meshes triggers §3(b).
2. §4 Sui Generis Database Rights exposure on the derived data layer.

Until that review completes and this repository is public, the obligation is **not**
discharged. Reinstatement under §6(b)(1) is *prospective* — any distribution made while
non-compliant is not retroactively cured.

## Anatomical honesty

Z-Anatomy is a **single male donor** dataset. Where a Veast plane renders this geometry, the
app must say so rather than implying the figure is the viewer's own body. Structures shown
are common to both sexes for Fascia, Muscular, Circulatory and Neural. Skeletal and Visceral
carry sex-specific structures and are male-derived; this is disclosed in-app and tracked by
spec phase **PL-8**. The male mesh must never be morphed toward female proportions —
that fabricates anatomy while still looking like real CT data.
