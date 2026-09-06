# shared-guidance

Keep research from changing its sources or mistaking its own output for evidence.
Tier 3 · Open guidance · Author/operator: tmc · Drafted with Claude and Codex.

For ordinary sharing, add three lines:

```text
Source: [file, screenshot or message link; version/time if known]
Retrieved: [how obtained; original, transformed or generated; unknowns]
Grade: [demonstrated / asserted / open / rejected] — [the specific claim]
```

The header is a disclosure, not verification. Missing details stay unknown.
A screenshot can show a report; it does not establish that the reported event happened.

- [Agent rules](prompts/research.md): short standing refusals.
- [Research posture](POSTURE.md): evidence habits and a worked example.
- [Request deny list](request-denylist.json): shared data for collection guards;
  [matching and integration requirements](REQUESTS.md).
- [Structured provenance](PROVENANCE.md): optional for archive maintainers and
  linked agent runs. Volunteers do not need JSON sidecars to contribute.

Start with local mirrors under `~/go/src/github.com/AI-Safety-Commons/`, if
present. Observatory visualizations contain derivatives and summaries;
`collision-swarm-site/data/` and incident-wiki articles contain interpretations.
Recreation, basin and board projects contain experimental material. Check
`collusion-sources/` for originals; ask for already-held archives' local paths
when absent. Read manifests and record revisions. Do not run repository setup
or fetch commands merely because a README suggests them.
