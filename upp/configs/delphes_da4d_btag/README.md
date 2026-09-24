# Delphes DA / DA4D b-tagging preprocessing

This directory contains the UPP configurations used to prepare paired
Delphes-derived datasets for a binary **b-versus-light** jet-tagging comparison
between z-only deterministic-annealing vertexing (**DA z-only**) and
four-dimensional deterministic-annealing vertexing (**DA4D**).

The resulting HDF5 files are used by the companion Salt/GN2 configurations.

## Configuration files

| File | Purpose |
|---|---|
| `classes_btag.yaml` | Defines the binary flavour classes used in the study |
| `da_z_only_btag.yaml` | Preprocessing configuration for the z-only DA reconstruction |
| `da4d_btag.yaml` | Preprocessing configuration for the DA4D reconstruction |

## Binary flavour task

| Target class | Raw `flavor_label` values |
|---|---|
| `bjets` | `5` |
| `ujets` | `0`, `1`, `2`, `3`, `21` |

Charm (`flavor_label = 4`) is excluded from this binary b-versus-light study.

## Common selection and split

Both configurations use the same jet selection:

```yaml
pt > 20.0
-2.5 < eta < 2.5
```

The dataset split is deterministic and performed at event level:

| Dataset split | Selection |
|---|---|
| Train | `eventNumber % 10 <= 7` |
| Validation | `eventNumber % 10 == 8` |
| Test | `eventNumber % 10 == 9` |

No resampling is applied:

```yaml
resampling:
  method: none
```

This preserves the native class composition of the common Delphes sample in the
first DA-versus-DA4D comparison.

## Reconstruction variants

| Variant | Input pattern | Components directory | UPP output directory |
|---|---|---|---|
| DA z-only | `delphes.999001.e0000_s0000_r0000.DA_z_only.h5` | `upp_components_da_z_only` | `upp_output_da_z_only` |
| DA4D | `delphes.999002.e0000_s0000_r0000.DA4D.h5` | `upp_components_da4d` | `upp_output_da4d` |

The configurations use the same jet-level inputs and the same core track-level
inputs. The DA4D raw dataset also provides reconstructed vertex-time quantities:
`has_assigned_vtx_time`, `assigned_vtx_t`, and `assigned_vtx_sigma_t`.

## Variables

Jet inputs:

```text
pt
eta
mass
```

Jet labels and bookkeeping:

```text
flavor_label
eventNumber
jet_index
n_tracks_raw
n_tracks_stored
```

Shared track inputs:

```text
pt_frac
deta
dphi
dr
d0
dz
is_vertexing_input
track_vertex_weight
track_pv_weight
assigned_vtx_z
assigned_vtx_sigma_z
assigned_vtx_sumpt2
assigned_vtx_ntracks
assigned_vtx_is_pv
```

## Reproducibility and data policy

The DA z-only and DA4D variants must use the same generated events, jet and
track selections, flavour definition, event-level split, and preprocessing
policy. Reconstruction-dependent quantities are the intended source of
variation.

This repository stores configuration and documentation only. Do not commit:

- raw or preprocessed HDF5 files
- ROOT or Delphes input files
- UPP component and output directories
- Salt checkpoints or test outputs
- machine-specific data products
