# symmprimdec.lib README

`symmprimdec.lib` is a Singular library for computing **primary decompositions of symmetric ideals**.  
It provides primary decomposition methods that exploit variable permutation symmetry, including semi-symmetric saturation techniques.

## Overview

- Library name: `symmprimdec.lib`
- Category: Commutative Algebra
- Main goal: compute minimal primary decompositions of symmetric ideals
- Author: Y. Ishihara

## Dependencies

This library loads the following Singular libraries:

- `elim.lib`
- `primdec.lib`
- `symodstd.lib`
- `dmodloc.lib`

## Main Procedures

### Decomposition for Symmetric Ideals

- `symmprimdecSYC(I, sigma, mode)`
  - Computes a primary decomposition of `I` using symmetry-aware techniques.
  - `sigma`: permutation (`intvec`)
  - `mode == 1`: uses `semiSymmSatPoly`
  - `mode != 1`: uses standard saturation (`sat`)
- `newSymmprimdecSYC(I, sigma)`
  - Wrapper for `symmprimdecSYC(I, sigma, 1)`.
- `primdecSYC(I)`
  - Computes a primary decomposition based on Shimoyama-Yokoyama with colon ideals.

### Supporting Procedures

- Separator-related: `separators`, `findSeparator`, `saturatedSeparating`
- Localization: `misLocal`, `symmMisLocal, stdSat`
- Permutation/orbits: `permIdeal`, `orbitDecom`, `permOrder`
- Checks: `isSubideal`, `isSymmetricSigma`
- Symmetric operations: `symmMaxIdeal`, `symmIntersect`, `symmSatPoly`, `semiSymmSatPoly`, `symmPrimedec`, `symmRadicalNoether`

## Usage (Minimal Example)

Run the following in a Singular session:

```singular
LIB "symmprimdec.lib";
ring r=0,(x,y,z),dp;
ideal I = x+y+z, xy+yz+zx, xyz-1;
intvec sigma = 3,1,2;

list L = newSymmprimdecSYC(I, sigma);
L;
```

To compare the two saturation modes:

```singular
list L1 = symmprimdecSYC(I, sigma, 1); // semi-symmetric saturation
list L2 = symmprimdecSYC(I, sigma, 0); // standard saturation
```

## Input Assumptions

- `I`: an `ideal` in the current base ring
- `sigma`: an `intvec` representing a permutation of variables
  - Example for 3 variables: `intvec sigma = 3,1,2;`
  - Usually expected to be a permutation of `1..nvars`

## Notes

- Runtime strongly depends on degrees, number of variables, and symmetry structure.
- Several procedures call Groebner basis computations (`std`), which may be expensive for large instances.
- Correctly specifying symmetry can significantly improve decomposition performance.

## Reference

The `info` block at the top of `symmprimdec.lib` contains a concise list of procedures and their intended roles.