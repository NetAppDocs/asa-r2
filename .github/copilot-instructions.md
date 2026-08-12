## Copilot instructions for ASA r2 documentation

### Repository overview
Product: NetApp ASA r2 storage systems

*ASA r2* documents NetApp SAN-only storage systems that run the *ASA r2 personality* of ONTAP. The repository covers hardware setup, SAN host access, storage provisioning, data protection, security, monitoring, and administration for ASA A1K, ASA A90, ASA A70, ASA A50, ASA A30, ASA A20, and ASA C30 systems.

### Repository structure
- `_include/` – Shared include directory reserved for reusable content snippets.
- `administer/` – Cluster administration, networking, storage VM access, capacity growth, node operations, user accounts, certificates, and host connectivity.
- `data-protection/` – Snapshots, snapshot reserve, SnapMirror replication relationships, *SnapMirror active sync* and *consistency groups*.
- `get-help/` – AutoSupport and support case tasks.
- `get-started/` – Product introduction, quick start, and entry points into installation and setup.
- `install-setup/` – Hardware requirements, site preparation, rack and cable tasks, power-on, cluster initialization, and SAN host setup.
- `learn-more/` – Architectural comparisons, platform limitations, and ASA r2-specific CLI and REST API behavior.
- `manage-data/` – SAN storage provisioning, *storage units*, host groups,data cloning, storage VM migration, and storage limits.
- `media/` – Shared images, diagrams, icons, and other media assets.
- `monitor/` – Cluster and node performance, capacity, insights, events, and job monitoring content.
- `release-notes/` – New features, support, and limitations for ASA r2 systems for supported ONTAP releases
- `secure-data/` – Encryption, key management, autonomous ransomware protection, and secure NVMe/TCP or IP-based SAN connections.
- `videos/` – Task videos and transcript pages.

### Product-specific context
**Architecture and components:**
- *ASA r2* systems deliver a unified hardware and software solution that creates a simplified SAN-only experience. On an ASA r2 system, ONTAP software and System Manager are streamlined to provide support for essential SAN functionality while removing features and functions not supported in SAN environments.
.
- Direct attach is supported for *iSCSI* and *NVMe/TCP* hosts, but not for *FC* or *NVMe/FC* hosts.
- The *ASA r2 personality* streamlines *System Manager*, the CLI, and the REST API around SAN workflows and limits non-SAN storage operations.
- Storage uses *storage availability zones* instead of aggregates; each HA pair shares one storage availability zone and both nodes in the pair can access its disks.
- *Storage VMs* serve SAN data through *LIFs*; IP LIFs can carry *iSCSI* and *NVMe/TCP*, while *FC* and *NVMe/FC* use separate LIFs.
- *SnapMirror active sync* provides symmetric active/active protection between two ASA r2 systems and uses *ONTAP Mediator* for monitoring and failover support.

**Key concepts:**
- A *storage unit* is the object users provision for hosts; it means a *LUN* for SCSI hosts or an *NVMe namespace* for NVMe hosts.
- A *consistency group* is a collection of storage units managed as one unit for storage management, snapshots, and replication; hierarchical consistency groups use parent and child relationships.
- A *host group* is the access-control object mapped to storage units; it means an *igroup* for SCSI hosts or an *NVMe subsystem* for NVMe hosts.
- Storage units are thin provisioned by default, and ONTAP automatically creates the backing volume for a storage unit in the appropriate storage availability zone.
- The default data *storage VM* is created during cluster setup, and new storage units are created inside that storage VM unless a different storage VM is selected.
- *Dual-layer encryption* combines hardware encryption with *NVE* software encryption.

**Naming conventions and terminology:**
- Use *ASA r2* for this platform and when distinguishing it from *ASA*, *FAS*or *AFF* systems.
- Use *storage availability zone* instead of aggregate terminology; capacity balancing and monitoring are described at the storage availability zone level.
- Use *ARP/AI* for *Autonomous Ransomware Protection with Artificial Intelligence*.
- Use *NSE* for *NetApp Storage Encryption*, *NVE* for *NetApp Volume Encryption*, and *SED* for *self-encrypting drive* when describing data-at-rest encryption.

### Typical user workflows
**Initial deployment:** Review hardware requirements → Prepare the site and hardware → Install and cable controllers and shelves → Power on the system → Initialize the ONTAP cluster → Set up SAN host access

**Provision SAN storage:** Create storage units → Add or select host groups and initiators → Map storage units to hosts → Complete host-side zoning or discovery steps → Start serving data

**Protect application data:** Create snapshots or consistency groups → Create storage VM peering if replication is needed → Configure snapshot replication or *SnapMirror active sync* → Restore data or fail over when required
