# Held-out benchmark corpus

`cases.yaml` is the v0.4 benchmark corpus requested in issue #1. It is
deliberately separate from `evals/cases/`, which is the package's regression
and behavior-specification set. The benchmark cases are not intended to be
loaded as runtime examples or copied into training prompts.

## Case schema

Each case contains:

- `id`: stable identifier for result tables
- `pattern` and `group`: the primary taxonomy area under test
- `input`: the text shown to the compared systems
- `instruction`: the same task context given to both systems
- `positive_control`: whether the text is expected to remain unchanged
- `dimensions`: case-specific notes for fidelity, native Turkish, pattern
  resolution, register, and restraint
- `exact_invariants`: facts, identifiers, or entities that must survive

The corpus intentionally does not include a target rewrite. For open-ended
Turkish, a single reference string would turn a reader-preference study into
an exact-match test.

## Reproducible protocol

1. Freeze the corpus revision, model versions, prompts, temperature, and date.
2. Run every case with the skill disabled and enabled using identical settings.
3. Randomize the A/B labels before showing outputs to native Turkish readers.
4. Have at least two independent readers score fidelity, native Turkish,
   pattern resolution, register, and restraint from 1 to 5. Record ties and
   disagreements instead of forcing a consensus.
5. Report aggregate scores, native-reader preference, positive-control
   preservation, exact-invariant failures, and per-pattern failures.

Do not mix these cases with `evals/cases/` when measuring a model. Keeping the
benchmark held out makes cross-model comparisons less vulnerable to regression
examples that were already visible during development.
