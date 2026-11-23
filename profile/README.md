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
  <a href="https://github.com/MaxIOFS/MaxIOFS/releases/tag/v1.11.0">
    <img src="https://img.shields.io/badge/version-1.11.0--stable-blue?style=for-the-badge" />
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
  <a href="https://docs.maxiofs.com/">Documentation</a> ·
  <a href="https://github.com/MaxIOFS/MaxIOFS">Repository</a> ·
  <a href="https://github.com/MaxIOFS/MaxIOFS/blob/main/CHANGELOG.md">Changelog</a> ·
  <a href="https://github.com/MaxIOFS/MaxIOFS/releases">Releases</a>
</p>

---

## What MaxIOFS Is

MaxIOFS is an S3-compatible object storage server written in Go. It ships as one binary with an embedded web console, a Pebble metadata engine, and native multi-tenancy. It needs no external database, no separate console process, and no cloud account.

It runs on a single node or a cluster of up to 10 nodes, and includes what a real deployment needs: tenants, IAM, SSO, encryption, Object Lock, replication, audit logs, and monitoring.

## What It Includes

| Area | What you get |
| --- | --- |
| **S3 API** | Buckets, objects, multipart, versioning, Object Lock (COMPLIANCE and GOVERNANCE), lifecycle, bucket policies, CORS, notifications, static websites, presigned URLs. S3 Select on CSV, JSON and Parquet, compressed or not. Works with the AWS CLI, `mc`, rclone, the S3 SDKs, Veeam, and Hadoop/Spark through S3A. |
| **Identity & access** | AWS IAM model with users, groups, versioned policies, roles and `AssumeRole`. STS temporary credentials. LDAP/AD and OAuth2/OIDC SSO, with Auto Sync from LDAP, Keycloak, Google Workspace and Microsoft tenants. 2FA. |
| **Multi-tenancy** | Isolated tenants with their own users, access keys, buckets, quotas, bandwidth limits and identity providers. |
| **Security** | Always-on AES-256-GCM envelope encryption with per-object keys, KEK rotation and a recovery bundle. SSE-C. Audit log with 20+ event types. |
| **Cluster & HA** | 1 to 3 copies of each object, or Reed-Solomon parity across nodes (like RAID 5, and RAID 6 from five nodes). Storage classes on groups of nodes, with lifecycle transitions between them. Automatic failover and catch-up of returning nodes. |
| **Replication** | To AWS S3, any S3-compatible endpoint, or another MaxIOFS: realtime, scheduled or batch. |
| **Web console** | Bucket browser, uploads, version history, tenant and IAM management, audit viewer, metrics and cluster views. Available in 9 languages. |
| **Operations** | Prometheus metrics, Grafana dashboard, syslog forwarding, SMTP alerts, maintenance mode, background integrity scrubber, and offline recovery tools (`maxiofs recover`, `reconcile`, `repair-pointers`). |

## What's New in v1.11.0

- **S3 Select over Parquet**, with Snappy, GZIP, ZSTD, Brotli or LZ4 columns, and over objects compressed with GZIP or BZIP2, as AWS does.
- **Permissions**: a bucket owner holds on its bucket only what its own permissions allow, no longer `s3:*`. A tenant administrator grants only what it holds, through the console, the IAM API or an identity provider.
- **Inactive tenants stop as a whole**: no sign-ins, access keys, presigned URLs, share links, public buckets or websites until the tenant is reactivated.
- **Quotas** count the parts of multipart uploads in progress.
- **Security**: S3 Select runs only a `SELECT`; presigned URLs, POST policies, STS federation and share links are held to their signer's permissions; inactive identity providers sign nobody in; built with Go 1.27.4.
- **Documentation site** at [docs.maxiofs.com](https://docs.maxiofs.com/): installation, deployment, every console page, S3 tools, the CLI, integrations and operations.

**Before upgrading to v1.11.0**

- Users that work on their own buckets (a Veeam account, for one) need their permissions on those buckets granted first, or they get `AccessDenied`. If they list buckets, they also need **List buckets** (`s3:ListAllMyBuckets`).
- A user of no tenant that reached every tenant only through the FullAccess policy needs the Super administrator permission to keep doing so.

**Earlier releases**: v1.10.0 handled full disks, sped up S3 writes about 5 times and gave `maxiofs recover` bucket settings back. v1.9.0 added parity, storage classes and SSE-C. See the [full changelog](https://github.com/MaxIOFS/MaxIOFS/blob/main/CHANGELOG.md).

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

Change the default password after the first login. Binaries, `.deb` and `.rpm` packages are on the [releases page](https://github.com/MaxIOFS/MaxIOFS/releases), and the [installation guide](https://docs.maxiofs.com/getting-started/installation/) covers the rest.

## Scope

MaxIOFS targets practical self-hosted deployments, from one node to a 10-node cluster. Look at a larger stack if you need petabyte-scale clusters, transitions to an external cloud, erasure coding within a single node, SAML, external KMS/HSM keys, or formal compliance certifications. The [main README](https://github.com/MaxIOFS/MaxIOFS#how-maxiofs-compares) compares MaxIOFS with AIStor, Garage and Ceph.

---

<p align="center">
  Released under the <a href="https://github.com/MaxIOFS/MaxIOFS/blob/main/LICENSE">MIT License</a>
</p>
