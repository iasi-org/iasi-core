# External input boundary

## Definition

`OUTSIDE` represents information sources that exist outside an IASI project.

Material originating outside IASI enters the project by being copied or imported into `inputs/externals/`.

Conceptually:

```text
OUTSIDE
   |
   | copy / import
   v
inputs/externals/
   |
   v
INPUTS
```

`inputs/externals/` is therefore not the outside world itself. It is the internal evidence retained by IASI of material that originated outside the system.

An input is classified as external by **provenance**, not by physical location.

> Every external is an input, but not every input is external.

## Details

`inputs/externals/` receives material only from outside the IASI process.

The broader input model may also contain knowledge produced or discovered during engineering work, including knowledge derived from engine activity or from observing outputs. Such knowledge is input, but it is not external unless its provenance is outside IASI.

External material is incorporated as evidence of what IASI actually received at a particular point in time. Interpretation, normalization, correction, completion, or derived knowledge belongs elsewhere in the IASI process.

## Constraints

- External input provenance must remain distinguishable from internally derived knowledge.
- Material under `inputs/externals/` must preserve the received content faithfully.
- A later change to an outside source must not retroactively change the evidence previously retained by IASI.

## Relationships

- `OUTSIDE` is a conceptual source layer outside IASI.
- `inputs/externals/` is the IASI boundary for retained external evidence.
- `INPUTS` is the broader set of information that can feed the engine.
- `OUTPUTS` may reveal new information that becomes input, but outputs themselves are not external inputs.

## Open questions

- How external artifact identity and version relationships should be represented.
- Whether import-time hashes, filesystem protections, or both should enforce immutability.
- How the runtime should expose provenance and integrity verification.

## Sources

- IASI Journey, 2026-08-30, "La frontera también se protege".
- Existing IASI principle that `inputs/externals/` is immutable and read-only from the IASI process perspective.
