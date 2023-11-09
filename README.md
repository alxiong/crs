# crs

Use Common/Structured Reference String (CRS/SRS) from existing ceremonies with ease

**WARNING: This is work in progress, none of the code has been audited. The library is NOT ready for production.**

## Download SRS to local

- Aztec's ignition: `./scripts/download_transcripts_aztec.sh NUM` where `NUM` can be `0..19` (`NUM=2` means download transcript `0, 1, 2`)
  - 100.8 million BN254 G1 points in total, split up into 20 files, each transcript file contains ~5 million points (~307 MB in size)
  - 2 BN254 G2 points are in the first transcript file
  - **If you only need `degree<=2^17`**, simply copy-paste one of those binary files in [`./data`](./data) folder to your `PROJECT_ROOT/data/`,
then, load into your code following the usage below (i.e. `crs::aztec20::kzg10_setup(degree)`). This is much easier and no downloads of large transcripts files is required.

## Usage

```rust
use ark_bn254::Bn254;
use ark_poly::univariate::DenseUVPolynomial;
use crs;

// simulated CRS (for test only)
let pp = KZG10::<Bn254, DenseUVPolynomial<<Bn254 as PairingEngine>::Fr>>::setup(max_degree, false, &mut rng)?;

// now, use Aztec's CRS
let pp = crs::aztec20::kzg10_setup(supported_degree)?;
```
