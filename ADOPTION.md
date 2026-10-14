# Consumer adoption status

## Proven boundary

The standalone test matrix covers the two first-wave consumer policies:

- **Mantle-equivalent strict capture:** clean environment, piped stdin, accepted zero exit, timeout, process-group teardown, and rejection when either retained-output bound is exceeded.
- **Octet-equivalent truncating capture:** bounded retained prefixes, exact observed-byte counts, timeout classification, and successful exit classification when consumer policy permits truncation.

A disposable migration against exact Mantle and Octet base revisions also passed both focused test suites and both consumer-focused Clippy rails. See [`PILOT.md`](PILOT.md) for commands, line reductions, retained consumer policy, and bounded caveats. These are pilot facts, not consumer release evidence.

## Cutover gate

The current independently rooted derived source is
`https://github.com/OnixResearch/bounded-exec-public.git`, with reviewed source
root `ca4c5ccfb194c2a1bb217a37a47c25a0efde21ec`. Cairn's Bounded Exec input and
other authorized consumers must pin an exact published revision, not an
ambient `../bounded-exec` path or mutable branch. Source availability alone
does not admit a consumer cutover or release.

The earlier Radicle pilot at `29dac88ecded94457572db3fdfaaaab95fa91525`
and RID `rad:z2CpqLFpdP36fZXYUK5ZNWxMibpCo` is historical evidence, preserved
in [`docs/radicle-publication.md`](docs/radicle-publication.md). Its original
no-fallback policy and receipts are unchanged. The new public snapshot is an
explicit source selection, not an automatic fallback or a claim that the
historical Git object exists in this independently rooted repository.

After consumer-owned cutover authorization:

1. consume the reviewed immutable commit without changing the AGPL license;
2. pin `bounded-exec` and `bounded-exec-core` by exact Git revision in both consumers;
3. align Cargo and Nix source identities in each consumer;
4. add a reviewed explicit working-directory field to Mantle's Nickel-backed dispatcher command profile instead of preserving ambient current-directory behavior;
5. replace Mantle's process mechanics in `src/external_batch_dispatch.rs` while retaining executable BLAKE3 verification, Slurm projection, protocol parsing, redaction, and product error codes in Mantle;
6. replace Octet's process mechanics in `cargo-octet/src/aeneas_execution.rs` while retaining provider-path construction, environment allowlisting, stage ordering, log rendering, report validation, and proof/evidence claims in Octet;
7. review the deliberate change from direct-child kill to process-group teardown in both consumers;
8. run standalone tests plus the focused pre-cutover consumer commands;
9. remove duplicate pipe, polling, kill, reap, and capture helpers only after parity passes.

Focused consumer commands:

```sh
# Mantle
nix develop -c cargo test -p mantle --bin mantle external_batch_dispatch::tests::

# Octet
nix develop -c cargo test -p cargo-octet --lib aeneas_execution::tests::
```

Cutover success means both focused suites retain their public behavior and product diagnostics while the generic mechanics come from the same exact published revision. It does not transfer Mantle build authority, Octet proof authority, Valence evidence authority, or Cairn release-readiness authority into this repository.
