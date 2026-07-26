# PROVENANCE — Veast anatomical meshes

> Canonical record for the six Z-Anatomy-derived meshes used by Veast planes 2–7.
> Created 2026-07-24 by spec phase **PL-0** (`docs/superpowers/specs/2026-07-24-plane-interactivity-design.md`).
> Nothing here was re-exported, re-decimated, or otherwise regenerated. These are preserved bytes.

---

## The canonical vintage decision

Two vintages of each mesh existed in the (untracked) build tree `pipeline/out/poc/`:

- **embedded** — a base64 `GLB_B64` string inlined inside each self-contained `*_viewer.html`
- **on-disk** — a `veast_*_web.glb` file sitting beside the viewers

They are **not** copies of each other. Sizes diverge in both directions, and the on-disk
files reuse mesh objects across nodes while the embedded ones are strictly 1:1.

**Decision: the EMBEDDED vintage is canonical for all six planes.** Rationale:

1. **Nothing is lost for tap resolution.** The set of glTF node names is *identical*
   between the two vintages on every plane that has both (verified set-equality, not
   just counts). Name-based picking behaves the same either way.
2. **1:1 node↔mesh removes highlight ambiguity.** The embedded meshes have exactly one
   mesh per node. The on-disk files reuse meshes across nodes (e.g. circulatory 653
   meshes for 673 nodes), so a per-mesh material override could highlight several
   structures at once. PL-3 requires highlight-on-tap, so 1:1 is the safer base.
3. **Uniform provenance.** Visceral exists *only* as an embedded copy. Choosing embedded
   makes all six planes one consistent vintage instead of a mixed set.
4. **It is what was actually reviewed.** The viewers are the artifact that was looked at
   and approved; the on-disk files are stale intermediates that were never the thing on screen.
5. **Every node is named** in all six meshes (see `named_nodes` below) — the name→record
   lookup that PL-3/PL-4 depend on is fully populated.

**Cost of the choice:** 51.06 MB total vs 42.80 MB for the on-disk set (which is also
missing visceral entirely). The +8.26 MB is immaterial because the meshes stream from
Supabase Storage rather than shipping in the app bundle.

The on-disk intermediates were **not deleted** — they remain in the untracked build tree.

---

## Canonical meshes

| Plane | Mesh | File | Bytes | Meshes | Nodes | Named nodes |
|---|---|---|---:|---:|---:|---:|
| 2 | Fascia | `veast_fascia_web.glb` | 13,509,132 | 757 | 757 | 757 |
| 3 | Muscle | `veast_muscle_web.glb` | 9,411,764 | 475 | 475 | 475 |
| 4 | Circulatory | `veast_circulatory_web.glb` | 9,097,316 | 673 | 673 | 673 |
| 5 | Skeleton | `veast_skeleton_web.glb` | 4,971,852 | 277 | 277 | 277 |
| 6 | Visceral | `veast_visceral_web.glb` | 4,945,020 | 126 | 126 | 126 |
| 7 | Neural | `veast_neural_web.glb` | 11,601,036 | 583 | 587 | 587 |

**Total:** 53,536,120 bytes (51.06 MB)

### SHA-256
```
1e7af692a6ebc365d6c488c51cdea337472b2d80091579bb8579de00d90bfcf3  veast_fascia_web.glb
b2d60937f912549f9ede349f90e19f60be57ab98a9dd31ed80410a3e0c1f221e  veast_muscle_web.glb
c0531d61de1f22f72a1452c4f00cbfc21403a3017b6ea9fefd7f9543453b8227  veast_circulatory_web.glb
3fbab3ab4d7fa8d53ec0821fb013de8d7f64b653da9b8e9be091057a0f89abf8  veast_skeleton_web.glb
1efe077f4fc06e9c34e16bd69a20e2cb14c1938bd8522b5b66b8a0e08509f65a  veast_visceral_web.glb
401a40c3f29e9e08db64f8d090ef043e0fdbb8423998ffa60d7daaf9aac85447  veast_neural_web.glb
```

Verify with:
```sh
shasum -a 256 -c CHECKSUMS.sha256
```

---

## Source of each canonical file

| File | Extracted from | Source SHA-256 (identical — byte-for-byte copy) |
|---|---|---|
| `veast_fascia_web.glb` | `pipeline/out/poc/fascia_viewer.html` → `GLB_B64` | `1e7af692a6ebc365d6c488c51cdea337472b2d80091579bb8579de00d90bfcf3` |
| `veast_muscle_web.glb` | `pipeline/out/poc/muscle_viewer.html` → `GLB_B64` | `b2d60937f912549f9ede349f90e19f60be57ab98a9dd31ed80410a3e0c1f221e` |
| `veast_circulatory_web.glb` | `pipeline/out/poc/circulatory_viewer.html` → `GLB_B64` | `c0531d61de1f22f72a1452c4f00cbfc21403a3017b6ea9fefd7f9543453b8227` |
| `veast_skeleton_web.glb` | `pipeline/out/poc/skeleton_viewer.html` → `GLB_B64` | `3fbab3ab4d7fa8d53ec0821fb013de8d7f64b653da9b8e9be091057a0f89abf8` |
| `veast_visceral_web.glb` | `pipeline/out/poc/visceral_viewer.html` → `GLB_B64` | `1efe077f4fc06e9c34e16bd69a20e2cb14c1938bd8522b5b66b8a0e08509f65a` |
| `veast_neural_web.glb` | `pipeline/out/poc/neural_viewer.html` → `GLB_B64` | `401a40c3f29e9e08db64f8d090ef043e0fdbb8423998ffa60d7daaf9aac85447` |

Each was base64-decoded and written without modification. Container validated:
magic `glTF` (`0x676c5446`), glTF version 2, and the header length field matching actual byte length.

---

## The rejected on-disk vintage (recorded for audit, not shipped)

| Plane | On-disk file | Bytes | Meshes | Nodes | SHA-256 |
|---|---|---:|---:|---:|---|
| 2 | `veast_fascia_web.glb` | 7,299,524 | 756 | 757 | `a8aa3b6ae29149fc77653a4910deafef961216e09ab21c11dbd3944724861e7f` |
| 3 | `veast_muscle_web.glb` | 4,977,440 | 475 | 475 | `fb2c2810111ffa8e3535dc46954db3ade257c0c0e81d92361d27d75b4e356dfc` |
| 4 | `veast_circulatory_web.glb` | 12,051,480 | 653 | 673 | `b1ae4de2f99758de6ea5492827ea5c32c70cefc7e26a1cfd5665008a66508217` |
| 5 | `veast_skeleton_web.glb` | 4,383,796 | 277 | 277 | `5b048c4c40ad6aa05be7338ef269e2caa8da65a1e9c4eb39e6e66f53e374c7c5` |
| 6 | — none existed — | — | — | — | — |
| 7 | `veast_neural_web.glb` | 16,165,732 | 566 | 587 | `f641e6b8567db351750f3c0e38cc6e1bdfa6417658ac441915d52a0ee9ad36a4` |
| 3 | `veast_muscle.glb` (pre-web original) | 8,315,816 | 475 | 475 | `253170b1cfcf258c36a06d5d27484956c55b9d1433351b49847c134f8eefe2f8` |

---

## Technical notes

- Generator on every mesh: `Khronos glTF Blender I/O v5.1.20`
- `extensionsUsed`: `None` on all six — **no Draco/meshopt compression is applied.**
  Compression is untried headroom if PL-2's device profiling shows load time is a problem.
- No textures or images on any mesh (`images: 0`, `textures: 0`).
- Material count: one per mesh in `meshes-v1`; per-structure-class from `meshes-v2` (see below).
- Git LFS is **not** used. The largest blob is 12.88 MB, well under GitHub's 50 MB
  warning threshold, so plain git objects avoid an extra tooling dependency.

## Licence

These are modified CC BY-SA 4.0 meshes. See `NOTICE.md`. Publishing this repository
publicly is the §3(b) obligation tracked by spec phase **PL-1** — do not treat this file
as evidence that the obligation is discharged.


---

## meshes-v2 — per-structure materials (2026-07-26)

`meshes-v1` shipped **one material on every mesh**, named `veast_muscle`, dark red
(`baseColorFactor [0.1706, 0.0049, 0.0039]`). Every bone, vessel, nerve and organ in the
atlas therefore rendered as red muscle.

That was never a defect in the geometry — it is what the source carried. The colours that
were reviewed and approved lived in the **JavaScript** of `pipeline/out/poc/*_viewer.html`,
which assigned a Three.js material per structure at load time. Extracting the embedded GLB
(the `meshes-v1` decision recorded above) necessarily left that behind, because it was
never in the file.

`meshes-v2` bakes those same palettes into the assets. **Only the glTF JSON chunk was
rewritten** — `materials[]` gained one entry per structure class and each primitive was
pointed at the class its node name resolves to. The BIN chunk was verified byte-identical
on every mesh after the round-trip. No geometry, node, accessor or buffer view was touched,
and no re-export, re-decimation or Blender round-trip occurred. Node names are unchanged, so
tap resolution is unaffected.

| Plane | Mesh | Materials | Breakdown |
|---|---|---:|---|
| 2 | Fascia | 1 | **unchanged, byte-identical to v1** |
| 3 | Muscle | 1 | **unchanged, byte-identical to v1** |
| 4 | Circulatory | 3 | artery 425 · vein 231 · heart 17 |
| 5 | Skeleton | 1 | bone 277 |
| 6 | Visceral | 9 | digestive 43 · respiratory 32 · reproductive 14 · endocrine 11 · urinary 8 · immune 6 · serous 6 · lung 5 · diaphragm 1 |
| 7 | Neural | 6 | brain 268 · nerve 246 · spinal_cord 30 · sense_organ 29 · autonomic 6 · meninges 4 |

Fascia and Muscle are unchanged **deliberately**. Their viewers never override the base
material either: red is correct for muscle, and the fascia viewer differentiates by lighting
a *selected myofascial line* rather than by recolouring the body. Baking a colour into fascia
would not have made it distinguishable from muscle; only the line-selection interaction does.

Three materials are translucent, each for a reason recorded in the viewer source: **lung**
(alpha 0.20) because lit solid the two lobes bury the 28-branch bronchial tree modelled
inside them; **serous** (0.13) for pleura and mesenteries; **diaphragm** (0.42, higher because
it is muscle and not a membrane); and in Neural, **meninges** (0.16) because the spinal dura
is an 18k-vertex sheath that otherwise renders as a solid white bar hiding the cord. These use
glTF `alphaMode: BLEND`, which is why the palette was baked into the asset rather than
applied at runtime — a material the file declares `OPAQUE` cannot be made translucent by
a renderer after load.

Colours were converted sRGB → linear on the way in, since glTF factors are linear while the
viewer's hex literals are sRGB. Verified against v1: its linear
`[0.1706, 0.0049, 0.0039]` round-trips to sRGB `#74100D`, the dark blood red the app
actually rendered.
