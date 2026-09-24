# Delphes DA / DA4D b-tagging preprocessing

Configuration and documentation for a paired comparison between:

- z-only deterministic annealing vertexing (`DA`);
- four-dimensional deterministic annealing vertexing (`DA4D`).

The final b-tagging training uses Salt/GN2 on HDF5 files produced after
preprocessing.

## Physics comparison

The DA and DA4D samples must use:

- the same generated events;
- the same reconstructed-jet and track selections;
- the same b-versus-light flavour definition;
- the same event-level train/validation/test split;
- the same preprocessing and normalisation procedure.

The intended difference is restricted to quantities derived from the reconstructed
primary/secondary-vertex information.

## Labels

- `bjets`: raw flavour label `5`;
- `ujets`: raw flavour labels `0`, `1`, `2`, `3`, `21`;
- raw flavour label `4` (charm) is excluded.

## Repository policy

This directory contains configuration and documentation only.

Do not commit:

- raw or preprocessed HDF5 files;
- ROOT or Delphes files;
- model checkpoints (`.ckpt`);
- `salt_runs/` or Lightning logs;
- machine-specific absolute paths.

## Status

Initial configuration branch for the Delphes DA/DA4D b-tagging study.
