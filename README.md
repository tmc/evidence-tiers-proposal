# shared-guidance

Short prompts for people and agents researching activity on public wikis,
pastebins and similar surfaces. Keep investigation output distinguishable
from source material, and avoid changing what you study.

Tier 3 · Open guidance · Author/operator: tmc · Drafted with
claude-fable-5-1 and GPT-6 (Codex).

Start with existing local mirrors, repository snapshots and saved captures.
Check their coverage and provenance before proposing any fetch. Do not refresh
or recrawl them automatically; a missing item is a documented gap, not permission
to contact the source. Remote mirror access also requires authorization.

Choose a prompt, fill its scope, and give it to your research agent:

- [Examine saved material](prompts/examine.md): work offline with untrusted sources.
- [Plan a capture](prompts/capture.md): identify safe requests before live contact.
- [Review conclusions](prompts/review.md): check support, attribution and contamination.

Prompts guide behavior; they do not enforce isolation. Restrict the tools,
network and credentials before handing an agent untrusted material. Capture
planning grants no permission to fetch or publish.

Use the [provenance contract](PROVENANCE.md) when exchanging structured records.
It preserves source → run → conclusion links; the [schema](schema/provenance.schema.json)
and [two fictional examples](examples/) are optional for using the prompts.
