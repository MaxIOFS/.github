<h1 align="center">
  <img src="https://raw.githubusercontent.com/MaxIOFS/MaxIOFS/refs/heads/main/web/frontend/public/assets/img/icon.png" width="24" />
  MaxIOFS
</h1>

<p align="center">
  <strong>Self-hosted S3-compatible object storage</strong><br/>
  Single binary · Embedded web console · Multi-tenant · AWS CLI compatible
</p>

<p align="center">
  <a href="https://github.com/MaxIOFS/MaxIOFS">
    <img src="https://img.shields.io/github/stars/MaxIOFS/MaxIOFS?style=for-the-badge" />
  </a>
  <a href="https://github.com/MaxIOFS/MaxIOFS/releases/tag/v1.4.2">
    <img src="https://img.shields.io/badge/version-1.4.2--stable-blue?style=for-the-badge" />
  </a>
  <a href="https://github.com/MaxIOFS/MaxIOFS/blob/main/LICENSE">
    <img src="https://img.shields.io/badge/license-MIT-green?style=for-the-badge" />
  </a>
  <a href="https://github.com/MaxIOFS/MaxIOFS/actions">
    <img src="https://img.shields.io/badge/tests-3900%2B_backend_|_106_frontend-green?style=for-the-badge" />
  </a>
</p>

<p align="center">
  <a href="https://github.com/MaxIOFS/MaxIOFS">Repository</a> ·
  <a href="https://github.com/MaxIOFS/MaxIOFS#quick-start">Quick Start</a> ·
  <a href="https://github.com/MaxIOFS/MaxIOFS/blob/main/CHANGELOG.md">Changelog</a> ·
  <a href="https://github.com/MaxIOFS/MaxIOFS/releases">Releases</a>
</p>

---

## What MaxIOFS Is

MaxIOFS is a Go-based object storage server with an S3-compatible API and an embedded React web console. It is designed for teams that want self-hosted object storage without operating a separate database, console service, or cloud account.

It fits single-node deployments and small to mid-range clusters where the priority is a practical, batteries-included storage system: users, tenants, access keys, policies, auditing, monitoring, encryption, replication, and a usable admin console in one deployable binary.

**Current status:** stable `v1.4.2`, suitable for production evaluation and mid-range deployments. See the main repository for current limitations and release notes.

---

## What's New In v1.4.2

`v1.4.2` focuses on security hardening, tenant isolation, concurrency correctness, and dependency refreshes.

| Area | Highlights |
| --- | --- |
| Security | Constant-time S3 secret comparison, encrypted S3 access secrets at rest, stronger PBKDF2 key derivation, safer console request body limits, HSTS on the console, CSP hardening, and stricter object path validation. |
| Multi-tenancy | Bucket permissions are scoped by bucket tenant, tenant admins no longer receive cross-tenant SSE notifications, and global admins can manage ACL/legal-hold operations on tenant buckets correctly. |
| Correctness | Atomic tenant quota updates, fixed versioning metrics races, exact-version HA fanout replication, safer version deletion under concurrent writes, and fixed metadata updates for versioned buckets. |
| Operations | Proxy streaming no longer buffers large request bodies in RAM, rate limiter races and cleanup leaks were fixed, sidebar navigation works correctly when collapsed, and inventory can be disabled from the console. |
| Dependencies | Go and frontend dependencies were refreshed within existing major versions; build, verification, core Go tests, frontend production build, and Vitest suite passed for the release. |

[Read the full v1.4.2 changelog](https://github.com/MaxIOFS/MaxIOFS/blob/main/CHANGELOG.md#142---2026-06-30)

---

## Why MaxIOFS

<table>
<tr>
<td width="25%" align="center">
<h4>Single Binary</h4>
<p>No external database and no separate console service. Download, configure, run.</p>
</td>
<td width="25%" align="center">
<h4>S3 Compatible</h4>
<p>Works with AWS CLI, SDKs, MinIO Client, Veeam-style backup workflows, and common S3 tools.</p>
</td>
<td width="25%" align="center">
<h4>Admin Ready</h4>
<p>Users, tenants, access keys, roles, bucket permissions, audit logs, and monitoring are built in.</p>
</td>
<td width="25%" align="center">
<h4>Cluster Aware</h4>
<p>Replication, HA read fallback, write quorum, health states, and inter-node sync for small clusters.</p>
</td>
</tr>
</table>

---

## Core Capabilities

### S3 API

- Bucket, object, multipart, tagging, ACL, CORS, lifecycle, notification, website, logging, and versioning APIs
- Signature V4 and V2 support, presigned URLs, POST policies, and conditional writes
- Object Lock with COMPLIANCE/GOVERNANCE modes and per-version enforcement
- S3 Select for CSV and JSON Lines, RestoreObject, OwnershipControls, PublicAccessBlock, and GetObjectAttributes
- AWS CLI, `aws s3api`, MinIO Client, SDK, and backup-tool compatibility

### Web Console

- Bucket browser with folder navigation, upload progress, object detail pages, tags, ACLs, legal hold, and version history
- Tenant, user, group, access-key, identity-provider, and role-capability management
- Audit log viewer, security controls, metrics dashboards, cluster view, and settings pages
- Multilingual UI: English, Spanish, French, German, Italian, Brazilian Portuguese, Chinese, Japanese, and Russian

### Security And Identity

- Local users, roles, groups, access keys, 2FA, rate limiting, account lockout, and password policies
- LDAP/Active Directory and OAuth2/OIDC SSO with group mappings
- AES-256-GCM encryption at rest, encrypted replication credentials, audit logging, and hardened console/S3 headers
- Tenant isolation with scoped quotas, permissions, users, buckets, and identity providers

### Operations

- Prometheus metrics, Grafana dashboard, syslog/HTTP log forwarding, SMTP alerts, and maintenance mode
- Background integrity scrubber and crash-safe Pebble metadata engine
- Replication to AWS S3, MinIO, or other MaxIOFS nodes
- Cluster sync for users, tenants, access keys, bucket permissions, IDP providers, group mappings, and capabilities

---

## Quick Start

### Docker

```bash
docker run -d \
  --name maxiofs \
  -p 8080:8080 \
  -p 8081:8081 \
  -v maxiofs-data:/var/lib/maxiofs \
  maxiofs/maxiofs:latest
```

### Build From Source

```bash
make build
./build/maxiofs --data-dir ./data
```

Default endpoints:

- Web console: `http://localhost:8081`
- S3 API: `http://localhost:8080`

Change the default credentials before using MaxIOFS outside local testing.

---

## Project Scope

MaxIOFS is intentionally positioned for practical self-hosted deployments rather than hyperscale object storage.

Use MaxIOFS when you want:

- A single deployable object-storage server
- Native multi-tenancy and a full web console
- S3 compatibility for common tooling and backup workflows
- Built-in security, audit, monitoring, identity, and replication features
- A permissive MIT-licensed alternative for small to mid-range environments

Consider a larger distributed object-store stack when you require erasure coding, cloud tiering, petabyte-scale clusters, SAML, HSM-backed tenant keys, or formal compliance certifications.

---

## Links

<p align="center">
  <a href="https://github.com/MaxIOFS/MaxIOFS">
    <img src="https://img.shields.io/badge/Repository-MaxIOFS-blue?style=for-the-badge" />
  </a>
  <a href="https://github.com/MaxIOFS/MaxIOFS/blob/main/CHANGELOG.md">
    <img src="https://img.shields.io/badge/Changelog-View_History-green?style=for-the-badge" />
  </a>
  <a href="https://github.com/MaxIOFS/MaxIOFS/releases">
    <img src="https://img.shields.io/badge/Releases-Download-red?style=for-the-badge" />
  </a>
</p>

---

MaxIOFS is released under the [MIT License](https://github.com/MaxIOFS/MaxIOFS/blob/main/LICENSE).
