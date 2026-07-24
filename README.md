# veast-anatomy-meshes

Canonical 3D anatomical geometry for **Veast** planes 2–7, preserved under version control.

| Plane | Name | File |
|---|---|---|
| 2 | Fascia | `meshes/veast_fascia_web.glb` |
| 3 | Muscular | `meshes/veast_muscle_web.glb` |
| 4 | Circulatory | `meshes/veast_circulatory_web.glb` |
| 5 | Skeletal | `meshes/veast_skeleton_web.glb` |
| 6 | Visceral | `meshes/veast_visceral_web.glb` |
| 7 | Neural | `meshes/veast_neural_web.glb` |

## Why this repository exists

Two reasons, one urgent and one legal.

**Backup.** These meshes previously existed only inside `pipeline/out/` in the main Veast
repository — a directory that is gitignored and had **zero** tracked files. The visceral
mesh was worse still: it was not a file at all, existing only as a base64 string inlined in
an HTML viewer. A disk loss would have destroyed it outright.

**Licence.** The meshes are modified CC BY-SA 4.0 material. §3(b) requires that modified
material be made available under a compatible licence. See `NOTICE.md`.

## Integrity

```sh
shasum -a 256 -c CHECKSUMS.sha256
```

`PROVENANCE.md` records where each file came from, why that vintage was chosen over the
alternative, and the full structural profile of both vintages.

## What these are not

- **Not re-exported.** Every byte here was preserved, not regenerated. No decimation, no
  re-encoding, no format conversion.
- **Not compressed.** `extensionsUsed` is absent on all six — no Draco, no meshopt.
- **Not the app's copy.** Veast streams these from Supabase Storage at runtime; they are
  deliberately kept out of the app bundle.

## Licence

Meshes: **CC BY-SA 4.0**, adapted from Z-Anatomy, itself adapted from BodyParts3D (DBCLS).
Full attribution in `NOTICE.md`.
