<h1 align="center">
  <img src="https://raw.githubusercontent.com/MaxIOFS/MaxIOFS/refs/heads/main/web/frontend/public/assets/img/icon.png" width="24" />
  MaxIOFS
</h1>

<p align="center">
  <strong>Self-hosted S3-compatible object storage</strong><br/>
  Single binary · Embedded web console · Multi-tenant · MIT licensed
</p>

<p align="center">
  <a href="https://github.com/MaxIOFS/MaxIOFS">
    <img src="https://img.shields.io/github/stars/MaxIOFS/MaxIOFS?style=for-the-badge" />
  </a>
  <a href="https://github.com/MaxIOFS/MaxIOFS/releases/tag/v1.10.0">
    <img src="https://img.shields.io/badge/version-1.10.0--stable-blue?style=for-the-badge" />
  </a>
  <a href="https://github.com/MaxIOFS/MaxIOFS/blob/main/LICENSE">
    <img src="https://img.shields.io/badge/license-MIT-green?style=for-the-badge" />
  </a>
  <a href="https://github.com/MaxIOFS/MaxIOFS/actions">
    <img src="https://img.shields.io/badge/tests-4400%2B_backend_|_161_frontend-green?style=for-the-badge" />
  </a>
</p>

<p align="center">
  <a href="https://maxiofs.com">Website</a> ·
  <a href="https://github.com/MaxIOFS/MaxIOFS">Repository</a> ·
  <a href="https://github.com/MaxIOFS/MaxIOFS/tree/main/docs">Documentation</a> ·
  <a href="https://github.com/MaxIOFS/MaxIOFS/blob/main/CHANGELOG.md">Changelog</a> ·
  <a href="https://github.com/MaxIOFS/MaxIOFS/releases">Releases</a>
</p>

---

## What MaxIOFS Is

MaxIOFS is an S3-compatible object storage server written in Go. It ships as one binary with an embedded web console, a Pebble metadata engine, and native multi-tenancy. It needs no external database, no separate console process, and no cloud account.

It runs on a single node or a cluster of up to 5 nodes, and includes what a real deployment needs: tenants, IAM, SSO, encryption, Object Lock, replication, audit logs, and monitoring.

## What It Includes

| Area | What you get |
| --- | --- |
| **S3 API** | Buckets, objects, multipart, versioning, Object Lock (COMPLIANCE and GOVERNANCE), lifecycle, bucket policies, CORS, notifications, static websites, S3 Select, presigned URLs. Works with the AWS CLI, `mc`, the S3 SDKs, Veeam, and Hadoop/Spark through S3A. |
| **Identity & access** | AWS IAM model with users, groups, versioned policies, roles and `AssumeRole`. STS temporary credentials. LDAP/AD and OAuth2/OIDC SSO, with Auto Sync from LDAP, Keycloak, Google Workspace and Microsoft tenants. 2FA. |
| **Multi-tenancy** | Isolated tenants with their own users, access keys, buckets, quotas, bandwidth limits and identity providers. |
| **Security** | Always-on AES-256-GCM envelope encryption with per-object keys, KEK rotation and a recovery bundle. SSE-C. Audit log with 20+ event types. |
| **Cluster & HA** | 1 to 3 copies of each object, or Reed-Solomon parity across nodes (like RAID 5, and RAID 6 from five nodes). Storage classes on groups of nodes, with lifecycle transitions between them. Automatic failover and catch-up of returning nodes. |
| **Replication** | To AWS S3, any S3-compatible endpoint, or another MaxIOFS: realtime, scheduled or batch. |
| **Web console** | Bucket browser, uploads, version history, tenant and IAM management, audit viewer, metrics and cluster views. Available in 9 languages. |
| **Operations** | Prometheus metrics, Grafana dashboard, syslog forwarding, SMTP alerts, maintenance mode, background integrity scrubber, and offline recovery tools (`maxiofs recover`, `reconcile`, `repair-pointers`). |

## New Since v1.8.0

**v1.10.0**

- **Full disks handled**: writes stop at 99.5% disk usage with `507 InsufficientStorage`; reads, deletes and retention keep working.
- **Recovery**: `maxiofs recover` restores each bucket's settings and Object Lock, shows progress, and accepts `--storage-root`.
- **Performance**: S3 writes are about 5 times faster under load, large PUTs about 25% faster (uploads are encrypted as they arrive), and a server with millions of objects starts in seconds.
- **Integrity**: scans cover every version and multipart objects, and report corruption with an audit event and an alert.
- **Cluster**: a joining node takes everything the cluster replicates; settings and logging targets are the same on every node.
- **Auto Sync** reads Google Workspace and Microsoft tenants.
- **Security**: a bucket owner's console permissions are limited to its own bucket, and reading a bucket's settings needs permission on that bucket.

**v1.9.0**

- **Parity**: Reed-Solomon erasure coding across nodes, from three nodes.
- **Storage classes**: groups of nodes keep a class such as `GLACIER`, with lifecycle transitions and filters by tags and size.
- **SSE-C** as in AWS, blocked per bucket until allowed.
- **Identity providers**: a session follows its provider, back-channel logout, and hourly Auto Sync from LDAP and Keycloak.
- **Security**: write digests and signed chunks are checked, a COMPLIANCE retention cannot be turned into GOVERNANCE, multipart parts in progress are encrypted, and the build uses Go 1.27.3.
- **Compatibility**: S3 error codes, ETags and `null` versions as in AWS; Hadoop and Spark verified through S3A; signed PUTs about 10 times faster.

**Upgrading from v1.8.0**

- `/metrics` now requires a bearer token (`metrics.token`) and answers `401` until one is set. Add it to the Prometheus scrape config.
- `trust_private_networks` is `false` by default. Behind a proxy or WAF, list its address in `trusted_proxies`.
- A node joins a cluster with a one-time join code, not a username and password.

[Full changelog](https://github.com/MaxIOFS/MaxIOFS/blob/main/CHANGELOG.md)

## Quick Start

```bash
docker run -d \
  --name maxiofs \
  -p 8080:8080 \
  -p 8081:8081 \
  -v maxiofs-data:/data \
  -e MAXIOFS_BOOTSTRAP_ACCESS_KEY=maxiofsadmin \
  -e MAXIOFS_BOOTSTRAP_SECRET_KEY=pick-your-own-secret \
  maxiofs/maxiofs:latest
```

- **Web console:** `http://localhost:8081`, login `admin` / `admin`
- **S3 API:** `http://localhost:8080`, with the key pair above

Change the default password after the first login. Binaries, `.deb` and `.rpm` packages are on the [releases page](https://github.com/MaxIOFS/MaxIOFS/releases).

## Scope

MaxIOFS targets practical self-hosted deployments, from one node to a 5-node cluster. Look at a larger stack if you need petabyte-scale clusters, transitions to an external cloud, erasure coding within a single node, SAML, external KMS/HSM keys, or formal compliance certifications. The [main README](https://github.com/MaxIOFS/MaxIOFS#how-maxiofs-compares) compares MaxIOFS with AIStor, Garage and Ceph.

---

<p align="center">
  Released under the <a href="https://github.com/MaxIOFS/MaxIOFS/blob/main/LICENSE">MIT License</a>
</p>
