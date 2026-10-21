# Proposing architecture changes

This folder is generated from Ergane and is overwritten on every export, so
edits here are lost. Changes are proposed as **change-sets** — semantic
operations validated against the canvas definitions before they are applied.

```json
{
  "title": "Raise settlement ASR risk after load test",
  "rationale": "p99 regressed in the 2026-07-30 load test",
  "operations": [
    { "op": "set", "entityId": 731, "sectionKey": "characteristics",
      "fieldKey": "risk", "value": 7 },
    { "op": "createEntity", "typeKey": "<adr typeIri>",
      "name": "Scale settlement workers" },
    { "op": "link", "sourceEntityId": 731, "targetEntityId": "$new[0]",
      "kind": "ref" }
  ]
}
```

Section and field keys, legal values and legal links are declared in
`definitions/<type>.codl-def.json`; a change-set that disagrees with the
definition is refused whole, never half-applied.

`$new[i]` names the i-th `createEntity` in the same change-set, counting
from 0, and that create must come earlier in the `operations` array.
It is accepted wherever an operation takes an entity id:
`entityId`, `sourceEntityId` and `targetEntityId`. So the `link` above,
from an existing entity to the one just created, is legal in one
change-set.

It is never inside a `$ref` value. A reference stored in a field
(`{"$ref": {"entityId": 812}}` in a `set`) needs a real id: create the
entity in one change-set, then set the reference in a second one, using
the id the first returned.

A `link` needs a `kind`: a short label you choose for the relationship
(the service requires one and does not restrict it). The graph's own
field references use `ref`.

Validate, then apply, through the BTABoK MCP server at
`https://mcp.iasaglobal.org`. It needs an API key, sent as
`Authorization: Bearer <key>` or `x-api-key: <key>`; setup for each agent
is at https://education.iasaglobal.org/mcp. The tools are
`loom_validate_change_set` and `loom_apply_change_set` (they keep the
`loom_` prefix; the product is Ergane). Validation writes nothing and says
what is wrong; run it first, every time.

The server checks field types, enum values, ranges and reference
legality, applies atomically, and records who changed what.
