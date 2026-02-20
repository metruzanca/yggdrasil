# yggdrasil

Privacy-focused family tree app.

## Product plan (v0)

### 1) Core idea

- Anyone can sign up and create a family tree.
- Creator of a tree = **Family Head** (tree owner/admin).
- Family members collaborate on one shared tree.

### 2) Privacy + access model

- Default private-by-family.
- Users outside a family can only see:
  - names
  - relationships
  - who the Family Head is
- No external access to full profiles, private docs, or sensitive metadata.
- End-to-end encryption (E2EE) is a core requirement:
  - family members in same tree can decrypt shared family data
  - keys and sharing model must prevent broad data leaks if infrastructure is
    compromised

### 3) Family data model (high level)

- **Person**: names, life events, dates, locations, relationships.
- **Relationship**: parent/child, partner, sibling, etc.
- **Family**: tree container + head/owner + member roles.
- **Movement history**: each person can record timeline of places lived/moved.
- **Lifecycle rules**:
  - deceased members are editable by any member in that same family tree
    (collaborative history preservation)

### 4) Documents + media

- Upload images and plain-text documents.
- Store metadata:
  - upload date
  - date(s) document is about (historical period/date ranges)
  - optional location tags
- Metadata must be searchable.
  Example: story written now but about 1940s should be discoverable via 1940s
  filters/search.

### 5) Cross-family visibility + potential overlap

- Platform-wide limited discovery graph (publicly visible minimum data only).
- If possible relation overlap is detected across trees:
  - notify potentially related family members/heads
  - do not expose full private details unless explicit sharing happens

### 6) Graph/canvas experience

- Provide a canvas graph view (Obsidian-style) showing families + connections.
- Graph edges informed by:
  - relationships
  - time periods
  - locations
  - movement history
- Separate visual layers:
  - private family detail layer
  - limited cross-family/public layer

### 7) Family-to-family sharing

- Support external tree sharing links/connections between families.
- Sharing must be explicit and revocable.
- Shared scope should be configurable (which branches/people/docs are visible).
- E2EE model must support selective cross-family decryption without exposing
  full trees.

### 8) Hosting + deployment

- Primary path: managed hosting.
- Self-hosting must be first-class documented:
  - infra requirements
  - environment variables
  - storage setup
  - backup/restore
  - key management and security caveats

### 9) Proposed stack

- **Frontend/App**: Next.js
- **Database**: PostgreSQL
- **ORM**: Drizzle
- **Hosting**: Railway (initial managed target)
- Keep architecture compatible with future self-hosted deployments.

## Delivery plan (phased)

### Phase 1: Foundations

- Auth + account setup
- Family/tree creation
- Roles (Family Head, Family Member)
- Baseline schema (person, relationship, family)

### Phase 2: Privacy + permissions

- Access controls (private-by-family)
- Limited external visibility (name, relationship, head only)
- Audit trail for sensitive actions

### Phase 3: Collaboration + records

- Deceased-member collaborative editing within family
- Image/document upload
- Metadata indexing (upload date + historical date + location)
- Search/filter by timeline

### Phase 4: Graph + overlap intelligence

- Family graph canvas view
- Time/location/movement overlays
- Potential-overlap detection + notifications

### Phase 5: Secure sharing + hardening

- External family-to-family sharing model
- E2EE rollout (MVP keys -> hardened key lifecycle)
- Threat modeling, incident response plan, security testing

### Phase 6: Deployment paths

- Managed deployment on Railway
- Self-hosting docs + scripts + operational playbooks

## Open questions

- E2EE key model: per-family key, per-member keys, or hybrid?
- Who can invite/remove members besides Family Head?
- Should overlap detection run opt-in or default-on?
- What exact fields are visible externally by default?
- How granular should external sharing permissions be?
