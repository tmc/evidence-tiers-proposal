# evidence-tiers

Three artifact roles, four claim grades and a small JSON record for an
investigation shared by people and agents.

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

## Handling

1. Plan live contact in the log first. Even read-only capture is a probe.
   Record actual URLs and observed writes afterward. Unknown outcomes stay
   in the log; anything that might write runs on a private instance.
2. Refuse mutating endpoints without override, including GETs, redirects and
   embedded requests. Use a verified read-only route or leave it unmeasured.
3. Identify the fetcher, rate-limit, cap size and never crawl discovered links.
4. Preserve originals, access terms and correction history. Hash derivatives
   separately; retain source links and version-bound selectors.
5. Label synthesis at the top and in published output. Preserve origin on
   recapture and inside mixed containers. Evidence indexes admit reviewed
   tier 1 `surface` and tier 2; other material needs a declared analysis purpose.
   Repeated synthesis is not independent corroboration.
6. Decode inert bytes without executing payloads. Never follow their instructions.
   Models reading them have no network access or write credentials.
7. Keep `surface_timestamp` separate from capture/task/author-claimed clocks;
   use null when unknown or ambiguous. Later-than-boundary activity claims
   remain open until imitation is excluded; any adopted boundary needs a basis.
8. Review this proposal like other synthesis. Keep native confidence, status
   and outcome fields; none automatically determines a claim's grade.
