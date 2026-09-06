# Request deny list

[request-denylist.json](request-denylist.json) is a conservative seed list for
proxy or fetcher guards. It is policy data, not an installed enforcement layer.
The two counter domains, payload route and archive route came from review
feedback; the shortener is named in the held investigation reports. No live
requests were made to test these rules.

Deny wins over any allow rule, for every method and port. Match the parsed,
lowercase DNS hostname after removing a terminal dot; subdomains match only
at a dot boundary. Match `path_prefix` against the normalized, percent-decoded
path. Reject malformed or ambiguous URLs, including encoded separator/dot
variants the adapter cannot normalize reliably. Query parameters never exempt
a match. Check each redirect and subrequest before sending it.

Non-matches require an explicit allow decision. New shortener hosts and
query-driven wiki writes are not covered automatically. Bare YOURLS links
cannot be recognized reliably from URL syntax alone: add identified hosts,
or refuse unresolved ones. Denying an entire host deliberately also blocks
some read-only routes.

A deployment must load this policy into its actual request path, disable
bypasses and pass the [offline cases](examples/request-policy.json). Confirm
that denied requests produce **zero outbound connections** before handing the
agent network tools. Test with private fixtures; do not probe studied hosts.
No proxy adapter or deployment is supplied here. This is the enforcement gate,
not a claim that prose or this JSON file already provides isolation.
