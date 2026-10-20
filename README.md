# Kepler-BOI1b

Transit search and fit of BOI-1b, the KeplerBOIs proof-of-concept candidate,
with [pytfit5](https://github.com/jasonfrowe/bls_cuda) (TransitFit5 and BLS).
The analysis is in `pytfit5_BOI-1.ipynb`. This repo is a standalone,
completed result.

## Running the notebook

In the shared KeplerBOIs workspace (see the
[workspace guide](https://github.com/KeplerBOIs/.github#readme)), open the
notebook and pick the **KeplerBOIs (.venv)** kernel. The workspace environment
has everything it needs: `pytfit5`, `exotic-ld` for limb darkening (with the
`exotic_ld_data/` directory here), `h5py`, `pandas` and `astropy`.

The workspace installs the current pytfit5 from its own `bls_cuda/` clone.

## Reproducing the result exactly

The `bls_cuda` submodule pins the pytfit5 version the result was produced
with (`ab595d8`, 16 June 2026). To rerun with exactly that code, use a
separate environment:

```sh
git clone --recurse-submodules https://github.com/KeplerBOIs/Kepler-BOI1b
cd Kepler-BOI1b
python -m venv .boi1 && source .boi1/bin/activate
pip install -e ./bls_cuda h5py exotic-ld "setuptools<81" ipykernel
python -m ipykernel install --user --name boi1 --display-name "Python (boi1)"
```

`setuptools<81` is needed because exotic-ld imports `pkg_resources`, which
newer setuptools no longer provides.
