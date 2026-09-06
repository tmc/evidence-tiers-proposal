# Plan a capture

Copy the prompt below and fill the scope. Tier 3: proposed research instructions.

```text
Purpose: [what must be established]
Named sources: [explicit URLs or existing captures]
Constraints: [owner policy, request budget, access restrictions]

Produce a capture plan; make no live requests. Prefer available originals.
For each necessary request, state its purpose, method, target, expected
side effects, redirects/subresources, rate and size limits, and storage.

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
