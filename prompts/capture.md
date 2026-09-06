# Plan a capture

Copy the prompt below and fill the scope. Tier 3: proposed research instructions.

```text
Purpose: [what must be established]
Available mirrors: [local paths, snapshots and capture manifests; use the README checkout map]
Evidence gap: [specific missing artifact or version]
Constraints: [owner policy, request budget, access restrictions]

Check the supplied local mirrors and saved captures first; make no network
requests or automatic refreshes. Record snapshot dates, coverage, byte hashes
and whether material is original, transformed or generated. A mirror is not
independent corroboration or automatically a capture.

If existing data answers the question, return its locators and stop. Otherwise
state the exact gap and why it matters. Prefer an already-held snapshot from
another investigator over new collection. Remote mirror retrieval is still
network access; never trigger archive-on-demand or origin fallback implicitly.

Only propose live capture for a remaining gap. State the necessary targets,
methods, side effects, redirects/subresources, rate/size limits and storage.
No proposed request is authorized by this prompt.

GET is not proof of read-only behavior. Exclude counters, edit/save/delete
paths, message-posting parameters and other mutating endpoints. Apply the
same exclusions to redirects, browser tools and embedded requests. Never use
discovered credentials or expand access beyond the authorized sources. If a
safe route is unverified, leave the value unmeasured. Do not crawl links or
use an archiver that transfers unknown traffic to the studied host.

Specify guards tested on private fixtures before collection, an identified
fetcher, and a durable request log. If execution is separately authorized,
record actual URLs contacted and observed writes, including failures or
accidents. Unknown outcomes remain unknown; do not invent wrote=false.
Check response bodies as well as HTTP status: a 200 response may be a block
page. Stop on throttling, unexpected mutation or scope changes; record failures
and affected artifacts without treating them as successful captures.

Preserve response bytes before decoding, source URL, method/options,
redirects, collector, capture time and hash. Keep surface timestamps and
origin separate. Preserve access terms; public derivatives require their
own hashes, input links and review for sensitive data.

Return only the bounded plan, unresolved safety assumptions and checks
needed before execution. Never treat this prompt as permission to collect.
```
