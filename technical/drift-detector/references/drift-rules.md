# Documentation Drift Detection Rules

This reference defines how to identify, classify, and explain documentation drift
across different input types. Drift is any place where documentation no longer
accurately reflects the product, API, or system it describes.

Drift is not always obvious. Some of it is explicit: a parameter was renamed and
the docs still use the old name. Some of it is implicit: a behavior changed subtly
and the docs describe the old behavior without being technically wrong in any single
sentence. Both types matter because both cause readers to fail.

---

## Table of Contents

1. Drift Classification System
2. Input Type Handling
3. Docs vs OpenAPI or Swagger Spec
4. Docs vs Changelog or Release Notes
5. Docs vs Newer Document Version
6. Docs vs Informal Update (Slack message, email, ticket)
7. Cross-Cutting Drift Signals
8. Severity Scoring
9. Common Drift Patterns Cheat Sheet

---

## 1. Drift Classification System

Every piece of drift falls into one of five categories. Use these categories
consistently in the output so writers can triage and delegate effectively.

### Removed
Something documented in the existing docs no longer exists in the product or API.
The endpoint was deprecated, the parameter was removed, the feature was sunset.
This is the most urgent category because it will cause readers to attempt
something that does not work.

Examples:
- Docs describe an endpoint that no longer exists in the spec
- Docs reference a CLI flag that was removed in the new version
- Docs mention a configuration option that was deprecated and deleted

### Renamed
Something exists in both the docs and the current source but under a different name.
The endpoint path changed, the parameter was renamed, the feature was rebranded.
This causes readers to use the wrong name and get errors that are hard to diagnose.

Examples:
- Docs use `user_id` but the spec now uses `userId`
- Docs reference `/api/v1/auth` but the endpoint is now `/api/v2/authenticate`
- Docs call a feature "Workspaces" but the product now calls it "Organizations"

### Changed behavior
Something exists under the same name but works differently than documented.
The parameter accepts different values, the response structure changed, the
default value is different, the rate limit changed, authentication works differently.

Examples:
- Docs say a parameter is optional but it is now required
- Docs show a response with a `data` field but the response now wraps in `result`
- Docs describe a default timeout of 30 seconds but it is now 10 seconds
- Docs say the endpoint returns 200 on success but it now returns 201

### Added but undocumented
Something new exists in the current source that has no corresponding documentation.
New endpoints, new parameters, new features, new error codes. This is drift in
reverse: the product moved ahead of the docs.

Examples:
- New endpoints in the spec have no documentation pages
- New optional parameters are not mentioned in the existing parameter tables
- New error codes are returned but not documented in the error reference

### Structurally stale
The documentation structure no longer reflects how the product is organized.
Navigation refers to sections that were reorganized, cross-references point to
moved content, version numbers are hardcoded and outdated.

Examples:
- Docs say "see the Authentication section" but authentication was merged elsewhere
- Docs reference version 2.1 throughout but the product is on version 3.0
- Code examples use a deprecated SDK version that no longer installs cleanly

---

## 2. Input Type Handling

Writers will provide different combinations of inputs. The skill must identify
what it has received and calibrate the analysis accordingly.

### Identifying the source of truth

The "source of truth" is whatever the writer provides as the current state of
the product. This is what the docs are compared against.

Sources of truth, in order of reliability:
1. OpenAPI or Swagger spec (most structured, most reliable)
2. Changelog or release notes (structured, but only covers what changed)
3. A newer version of the same document (reliable for structural drift)
4. Informal update notes (least structured, requires more inference)

When the source of truth is partial (a changelog only covers what changed,
not the full current state), note this limitation clearly in the review.
A changelog that says "renamed `user_id` to `userId`" tells you about that
one change but does not confirm everything else is current.

### Identifying the documentation being reviewed

The documentation being reviewed is whatever the writer provides as the existing
published docs. This may be:
- A full documentation page or section
- An API reference page
- A README
- A how-to guide or tutorial
- A conceptual overview

The type of documentation affects what drift signals are most relevant.
API reference pages have different drift patterns than conceptual guides.

### When both inputs are ambiguous

If it is not clear which document is the current source of truth and which is
the documentation being reviewed, ask before proceeding. Getting this backwards
produces an inverted analysis that is worse than no analysis.

---

## 3. Docs vs OpenAPI or Swagger Spec

An OpenAPI spec is the most reliable source of truth for API documentation drift.
It is machine-generated from the codebase in most modern workflows, which means
it reflects the actual current state of the API rather than someone's memory of it.

### What to compare

**Endpoints**
- Every endpoint documented in the docs should exist in the spec
- Every endpoint in the spec should be documented (flag undocumented ones)
- HTTP methods must match (GET vs POST vs PUT)
- Path parameters must match exactly, including naming conventions

**Parameters**
- Parameter names must match between docs and spec
- Required vs optional status must match
- Data types must match (string vs integer vs boolean vs array)
- Default values must match
- Enum values must match: if the spec lists accepted values, the docs must list the same set
- Deprecated parameters in the spec should be flagged as deprecated in the docs

**Request and response structure**
- Field names in request bodies must match
- Field names in response bodies must match
- Nested structure must match
- Data types of fields must match
- Required vs optional fields in responses must match

**Authentication**
- Authentication method documented must match what the spec declares
- Security scheme names must match
- Scope requirements must match if the spec defines them

**Error codes**
- HTTP status codes documented must match what the spec declares for each endpoint
- Error response structure must match
- Any error codes in the spec that are undocumented should be flagged

### What not to flag

Do not flag prose descriptions that are accurate but worded differently from
the spec. The spec is the source of truth for structure and naming, not for
the quality of the explanatory text around it. A spec field description of
"user identifier" and a docs description of "the unique ID for the user account"
are not drift. They are just different levels of detail.

---

## 4. Docs vs Changelog or Release Notes

A changelog is a partial source of truth. It tells you what changed between
versions but not the full current state. This means drift detection against a
changelog is more targeted: focus on whether the documented behavior for the
changed items has been updated.

### What to compare

**For each change listed in the changelog:**

Removed items:
- Find every place the removed item appears in the docs
- Flag each mention as drift of type Removed

Renamed items:
- Find every place the old name appears in the docs
- Flag each mention as drift of type Renamed
- Note the new name in the flag

Changed behavior:
- Find the section of docs that covers the changed item
- Compare the documented behavior against the changelog description of the new behavior
- Flag any mismatch as drift of type Changed behavior

New additions:
- Check whether the new item has corresponding documentation
- Flag missing documentation as drift of type Added but undocumented

Version references:
- If the changelog indicates a version bump, check for hardcoded version numbers
  in the docs and flag them as drift of type Structurally stale

### Scope limitation note

Always note in the review that changelog-based drift detection is scoped to
the changes listed in the changelog. Items not mentioned in the changelog may
also have drifted but cannot be assessed from this input alone. Recommend a
full spec comparison for comprehensive coverage.

---

## 5. Docs vs Newer Document Version

When the writer provides two versions of the same document, the analysis is
a structured diff focused on meaning, not just wording.

### What to compare

**Removed content**
Sections, paragraphs, or specific claims present in the old version but absent
from the new version. Flag these as potential drift if the docs being reviewed
still reference them.

**Changed claims**
Statements that exist in both versions but say different things. A timeout value
that changed, a default that shifted, a behavior that was qualified differently.

**Added content**
New sections or claims in the newer version that are absent from the docs being
reviewed. Flag as drift of type Added but undocumented.

**Structural changes**
Section reorganization, heading changes, new prerequisites, removed warnings.

### What not to flag

Stylistic rewrites that do not change the meaning are not drift. If the old
version says "The API returns a 404 error" and the new version says "A 404
response indicates the resource was not found," the meaning is the same.
Do not flag this.

---

## 6. Docs vs Informal Update

Informal updates are the least reliable source of truth because they are
often incomplete, ambiguous, or written for an audience other than the
documentation team. Treat them carefully.

### Handling informal updates

Read the update for every concrete, verifiable claim it makes:
- Specific names that changed
- Specific behaviors that changed
- Specific features that were added or removed
- Specific version numbers mentioned

For each concrete claim, search the documentation for corresponding content
and flag any mismatch.

For vague or ambiguous statements in the update ("we improved the auth flow"),
do not flag documentation as drifted without a specific discrepancy to point to.
Note in the review that the update contained information too vague to assess
against the documentation and recommend the writer follow up with the engineer
or product manager for specifics.

### Reliability warning

Always note in the review that informal update sources are the least reliable
input type for drift detection. Recommend the writer request a changelog entry
or spec update from the engineering team for any significant product changes.

---

## 7. Cross-Cutting Drift Signals

These signals appear regardless of input type and should always be checked.

### Version numbers

Hardcoded version numbers in documentation become wrong every time the product
ships. Flag any specific version number that:
- Does not match the version indicated in the source of truth
- Appears in a code example that installs a specific package version
- Appears in a URL path that suggests a versioned API

### Deprecated patterns

Code examples or procedures that use patterns marked as deprecated in the
source of truth. These technically work but teach readers something the
product team is actively discouraging.

### Broken cross-references

References to other sections, pages, or external resources that no longer
exist or have moved. These do not require a source of truth comparison if
the referenced location is obviously wrong or missing.

### Date-sensitive claims

Statements like "as of version 2.1" or "since the March 2024 update" that
tie documentation to a specific moment in time. These are candidates for
drift even without a direct comparison if the timeframe is clearly past.

### Screenshot and diagram drift

Descriptions of UI elements, screenshots, or diagrams that reference visual
elements that may have changed. Flag any documentation that relies on a
screenshot or diagram for critical information without text-based backup,
since visual assets drift invisibly.

---

## 8. Severity Scoring

Every flagged drift item receives a severity level. This helps writers triage
when they cannot fix everything at once.

### Critical
The documentation will cause a reader to fail immediately and completely.
- Removed endpoint or feature still documented as available
- Wrong authentication method documented
- Required parameter documented as optional
- Incorrect error code documented for a critical failure path

### High
The documentation will cause a reader to fail after some effort or in specific conditions.
- Renamed parameter or endpoint
- Changed default value
- Changed response structure
- Deprecated pattern documented as current best practice

### Medium
The documentation is misleading or incomplete but a reader can work around it.
- Changed behavior that is partially documented
- New parameter not documented but existing parameters still work
- Outdated version number in a non-critical example
- Structurally stale cross-reference

### Low
The documentation is technically inaccurate but unlikely to cause reader failure.
- Terminology drift where the old term still redirects or works
- Minor response field changes in non-critical paths
- Outdated version numbers in historical context

---

## 9. Common Drift Patterns Cheat Sheet

| Pattern | Drift type | Severity | Where it usually appears |
|---|---|---|---|
| Endpoint path changed | Renamed | Critical | API reference, tutorials |
| Parameter renamed | Renamed | High | API reference, code examples |
| Parameter type changed | Changed behavior | High | API reference |
| Required/optional status flipped | Changed behavior | Critical | API reference |
| Default value changed | Changed behavior | High | API reference, how-to guides |
| Response field renamed | Renamed | High | API reference, tutorials |
| Response structure changed | Changed behavior | High | API reference, tutorials |
| Feature deprecated | Removed | High | How-to guides, tutorials |
| Feature removed | Removed | Critical | Any |
| New endpoint undocumented | Added but undocumented | Medium | API reference |
| Hardcoded version outdated | Structurally stale | Medium | Code examples, install guides |
| SDK version outdated in example | Structurally stale | High | Tutorials, quickstarts |
| Auth method changed | Changed behavior | Critical | Getting started, API reference |
| Error code changed | Changed behavior | High | API reference, troubleshooting |
| Rate limit changed | Changed behavior | Medium | API reference, best practices |
| Cross-reference broken | Structurally stale | Medium | Any |
| Screenshot outdated | Structurally stale | Low to Medium | UI guides, tutorials |
| Deprecated pattern in code example | Changed behavior | High | Tutorials, how-to guides |
| Terminology rebranded | Renamed | Medium | Any |
