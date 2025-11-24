<h1 align="center">Welcome to <span><img src="https://raw.githubusercontent.com/MaxIOFS/MaxIOFS/refs/heads/main/web/frontend/public/assets/img/icon.png" width="20" /></span> MaxIOFS</h1>

<p align="center">
  <strong>S3-Compatible Object Storage System</strong><br/>
  Single Binary • Modern Web UI • AWS CLI Compatible
</p>

<p align="center">
  <a href="https://github.com/MaxIOFS/MaxIOFS">
    <img src="https://img.shields.io/github/stars/MaxIOFS/MaxIOFS?style=for-the-badge" />
  </a>
  <a href="https://github.com/MaxIOFS/MaxIOFS">
    <img src="https://img.shields.io/github/forks/MaxIOFS/MaxIOFS?style=for-the-badge" />
  </a>
  <a href="https://github.com/MaxIOFS/MaxIOFS">
    <img src="https://img.shields.io/github/issues/MaxIOFS/MaxIOFS?style=for-the-badge" />
  </a>
  <a href="https://github.com/MaxIOFS/MaxIOFS/releases">
    <img src="https://img.shields.io/badge/version-0.4.2--beta-blue?style=for-the-badge" />
  </a>
</p>

---

## 🚀 About MaxIOFS

MaxIOFS is a **Go-based object storage system** with S3 API compatibility and an embedded Next.js web interface, designed as a single deployable binary.

**Current Status:** Beta - suitable for development, testing, and staging environments.

### Key Features

- ✅ **Full S3 API compatibility** (bucket operations, multipart uploads, presigned URLs)
- ✅ **Embedded web console** with modern responsive UI and dark mode
- ✅ **Single binary deployment** - no external dependencies
- ✅ **Dual authentication** (JWT for console, S3 Signature v2/v4 for API)
- ✅ **Two-factor authentication (2FA)** for enhanced security
- ✅ **Multi-tenancy** with resource isolation and quotas
- ✅ **Server-side encryption (SSE)** with persistent key management
- ✅ **Complete audit logging** for compliance tracking
- ✅ **Real-time notifications** via Server-Sent Events (SSE)
- ✅ **Prometheus monitoring** integration
- ✅ **Docker support** for containerized deployments
- ✅ **Bucket notification webhooks** with event filtering
- ✅ **AWS CLI compatible** - tested with MinIO Warp stress testing

---

## 🛠 Technology Stack

<p>
  <img src="https://skillicons.dev/icons?i=go,nodejs,react,sqlite,docker,linux" />
</p>

| Technology | Purpose |
|-----------|---------|
| **Go 1.21+** | Core storage engine |
| **Next.js** | Embedded web console |
| **BadgerDB** | Metadata storage |
| **SQLite** | Authentication database |
| **Filesystem** | Object storage backend |

---

## 🏗 Current Architecture

**Single Binary Design:**
- All-in-one executable with embedded web UI
- BadgerDB for metadata management
- SQLite for user authentication
- Filesystem-based object storage
- Atomic write operations with rollback capability

**Performance (Local Benchmarks):**
- Write: ~374 MB/s
- Read: ~1703 MB/s
- Stress tested: 7000+ objects with MinIO Warp

---

## 📌 Development Roadmap

**Completed:**
- [x] S3 API compatibility layer
- [x] Web management console
- [x] Multi-tenancy support
- [x] Access key management
- [x] Bucket policies and CORS
- [x] Two-factor authentication (2FA)
- [x] Server-side encryption (SSE)
- [x] Audit logging system
- [x] Prometheus monitoring
- [x] Real-time notifications (SSE)
- [x] Bucket notification webhooks

**In Progress / Planned:**
- [ ] Multi-node distributed architecture
- [ ] Object replication
- [ ] Multi-region federation
- [ ] Enhanced IAM policies
- [ ] Object lifecycle management
- [ ] Advanced compliance features

---

## 🤝 Contributing

We welcome contributions from the community ❤️

🐞 **Report Issues:** https://github.com/MaxIOFS/MaxIOFS/issues  
🧩 **Feature Requests:** https://github.com/MaxIOFS/MaxIOFS/discussions  
📩 **Contact:** contact@maxiofs.com *(optional)*

---

## 🔗 Useful Links

| Resource | Link |
|--------|------|
| Official Website | https://maxiofs.com *(optional)* |
| Discussion Board | https://github.com/MaxIOFS/MaxIOFS/discussions |
| Releases | https://github.com/MaxIOFS/MaxIOFS/releases |

---

## 🚀 Quick Start

**Build Requirements:**
- Go 1.21+
- Node.js 18+

**Build & Run:**
```bash
make build
./build/maxiofs --data-dir ./data
```

**Access:**
- Web Console: http://localhost:8081 (default credentials: admin/admin)
- S3 API Endpoint: http://localhost:8080

**⚠️ Important:** Change default credentials before production use!

---

## ⚠️ Known Limitations (Beta)

**Architecture:**
- Currently single-node only (distributed mode in development)
- Filesystem backend only
- No multi-node replication yet

**Security:**
- No third-party security audit performed
- HTTPS recommended for production
- TLS/SSL configuration required for production deployments

**Production Readiness:**
- Suitable for development, testing, and staging
- Multi-tenancy needs production validation
- Object Lock not validated with third-party tools

---

## 📜 License

MaxIOFS is released under the **MIT License** – use, modify and distribute freely.

---

<p align="center">
  Built with ❤️ by the <b>MaxIOFS Community</b> and Contributors 🚀
</p>
