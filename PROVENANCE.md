# Provenance records

Optional record contract for the [shared research guidance](README.md).
The record type and schema identity remain `evidence/provenance` 0.1.
Three artifact roles, four claim grades and a small JSON record.

Tier 3 · Open proposal 0.1 · Author/operator: tmc · Drafted with
claude-fable-5-1 and GPT-6 (Codex).

## Labels

| Tier | Holds |
|---|---|
| **1 — Captured** | Original surface bytes and capture metadata. |
| **2 — Instrumentation** | Investigator code, run logs and transformed copies. |
| **3 — Synthesis** | Claims and interpretations, human or generated. |

Tiers are roles, not credibility scores. Capturing a generated report
preserves the report; it does not make its conclusions independent evidence.

Grade each claim: **demonstrated** (available captured material establishes
it), **asserted** (reported without independent support), **open** (unresolved),
or **rejected** (examined and found not to hold; retain the reason).
These are not a ranking. Capturing "it worked" establishes that it was said.

## Records

Put a record in `<file>.prov.json` or an embedded `provenance` object.
One claim per synthesis record; several claims may use a sidecar array.
Keep domain fields outside the object. The [schema](schema/provenance.schema.json)
defines required fields and rejects unknown ones:

| Record | Required fields |
|---|---|
| Every record | `type: "evidence/provenance"`, `version: "0.1"`, `tier` |
| Capture | `source_url`, `captured_at`, `captured_by`, `method`, `sha256`, `surface_timestamp`, `origin` |
| Instrumentation | `author`; runs add `ran_at`, `investigator_probe`; probes add `touched`, boolean `wrote` |
| Synthesis | `author`, `written_at`, `claim`, `grade`, nonempty `cites`; `generated_by` requires `operator` |

- Hash exact stored artifact bytes, not sidecars. Preserve response bytes
  before decoding; transformations get new hashes and input links. Record
  redirects in `redirect_chain`.
- Origin is `unknown` until reviewed, then `surface`, `investigator` or
  investigation `synthesis`. Known investigator/synthesis origin requires
  `inputs` establishing it. Without that basis, retain `unknown`. `surface`
  does not identify an actor; agent-generated material under study is not
  automatically investigation synthesis. Record the basis, not guesses.
- `inputs` links derivation or origin, including earlier analysis and run logs.
  `cites` links claim support. Use `sha256:<hash>` or `msg:<Discord message ID>`;
  citations also allow `url:<HTTP(S) URL>` except for `demonstrated` claims.
  Message IDs must resolve to captured versions, not merely live messages.
  Bind selectors to hashes; for Git sources, hash the file bytes and retain
  repository, revision and path.
- `captured_by` labels a collector (tool or person); keep the accountable
  operator and model separate. Generated outputs name both model and operator.
  Keep model revisions, prompts, tool calls and settings in run logs when
  replay matters.

Examples: [agent chain](examples/agent-chain.json) and
[embedded Discord capture](examples/discord-capture.json). Both are fictional;
no capture bytes are supplied. Validate each chain `records` element or embedded
`provenance` value separately, using Draft 2020-12 with format checking:

```sh
check-jsonschema --schemafile schema/provenance.schema.json <record.json>
```

Validation checks structure. Reviewers check bytes, reference resolution,
claim support, independent origin and handling.
