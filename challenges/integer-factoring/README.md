# Integer factoring: one machine in time N^o(1)

Frozen on 2026-10-30 from
[IsaacRudich/SubexponentialDeterministicFactoring](https://github.com/IsaacRudich/SubexponentialDeterministicFactoring)
commit `c91cc3f4947caca8977e81a5d14244f73b5ae2b1`, file `Challenge.lean`, byte for byte.
Isaac Rudich and Louis-Martin Rousseau wrote the statement and the proof. The Apache-2.0
license is kept next to the statement. See [provenance.json](provenance.json) for the
Git blob and SHA-256 values.

This is the statement of the
[Integer Factoring board](https://bigospeedrun.com/integer-factoring) at score 0.
Only `Factoring.subexponentialRate` is a target:

```lean
theorem subexponentialRate :
    ∃ M : FactoringMachine, ∀ k : ℕ, 1 ≤ k → ∃ C : ℕ,
      FactorsWithin M (fun n => C * 2 ^ (n / k))
```

One Mathlib `TM2ComputableInTime encodeNat encodeNat Nat.minFac` machine, with every
stack alphabet finite, outputs the smallest prime factor of every `N` in binary. Its time
on inputs of `n` bits is at most `C_k · 2^(n/k)` for every `k ≥ 1`. That is time
`N^o(1) = 2^o(b)`, score 0 on the board. A TM2 machine is a multi-stack machine. For a fixed
machine, one step runs a bounded number of stack operations, so it matches the
board's multitape model up to constant factors. The statement also covers `N = 0` and
`N = 1`, which the board does not need.

`Factoring.SqrtLogLogConjecture` in the same file is a definition of a proposition.
It is not a target, and nothing here proves it.

## Run

This profile is closed to issues and PRs. Only a maintainer can run it, with the
`Verify a Lean proof` workflow on GitHub Actions:

- `challenge_file`: `challenges/integer-factoring/Challenge.lean`
- `theorem_names`: `Factoring.subexponentialRate`
- `lean_toolchain`: `leanprover/lean4:v4.35.0`

The run builds their `Solution`, `Factoring_aux` and `FactoringAux` sources from the
pinned commit. It does not use their Challenge.lean, Lake files or compiled objects. The
challenge is this frozen copy. The Mathlib pin is their unchanged lake-manifest.json
(Mathlib `56a005855ea17e0b0958f73ec801ae140b0a1679`, v4.35.0), in
[profiles/factoring-lake-manifest.json](../../profiles/factoring-lake-manifest.json).

The tools are in [profiles/tools-v4.35.0.json](../../profiles/tools-v4.35.0.json).
Comparator `e3dcf3083fc5` and lean4export `5a9a355dc6c5` are the v4.35.0 builds of
the code that the v4.34 profile uses: from our earlier pins, only their toolchain,
manifest and test files changed. nanoda, landrun and elan are unchanged.

Their lakefile sets no Lean options, so their sources elaborate with Lean's default
`autoImplicit=true`. The profile keeps that default (`auto_implicit`). Other profiles
build with `autoImplicit=false`. The option changes only how the sources elaborate.
Comparator still compares the elaborated statement with this frozen copy.
