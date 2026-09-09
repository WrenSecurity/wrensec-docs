Private Enterprise Numbers (PENs) are identifiers that can be used in SNMP configurations, in LDAP configurations, and wherever the use of an ASN.1 object identifier (OID) is appropriate. The [Public Technical Identifiers (PTI)](https://pti.icann.org), an affiliate of ICANN, manages and maintains the PEN registry in consultation with the [Internet Engineering Steering Group (IESG)](https://www.ietf.org/about/groups/iesg).

PENs are issued from an OID prefix that was assigned to IANA. That OID prefix is `1.3.6.1.4.1.`. Wren Security was [assigned enterprise number 64165](https://www.iana.org/assignments/enterprise-numbers/?q=64165) on September 2, 2025. This means our organization can use the unique OID base `1.3.6.1.4.1.64165` for any of its needs. However, we need a clear scheme for assigning further numbers so we don’t run into collisions.


## OID allocation scheme

The allocation scheme is a continuous effort. New branches will be introduced as needs arise.


### Product branches

The first level of branching under our base corresponds to the products we maintain.

| Product | OID                   |
| ------- | --------------------- |
| Wren:AM | `1.3.6.1.4.1.64165.1` |
| Wren:DS | `1.3.6.1.4.1.64165.2` |


### Protocol-specific branches

Within each product branch, OIDs are divided further by protocol.

| Protocol | OID                     |
| -------- | ----------------------- |
| LDAP     | `1.3.6.1.4.1.64165.*.1` |


### LDAP branches

LDAP schema definitions require multiple categories of OIDs, such as attribute types and object classes. These are defined as sub-branches under the LDAP protocol branch.

| OID                       | Type            |
| ------------------------- | --------------- |
| `1.3.6.1.4.1.64165.*.1.1` | Attribute Types |
| `1.3.6.1.4.1.64165.*.1.2` | Object Classes  |
| `1.3.6.1.4.1.64165.*.1.3` | Request / Response Controls  |


## OID registry

The table below serves as our simple, authoritative OID registry for all allocations under `1.3.6.1.4.1.64165`.

| Object Identifier | Name | Description | Allocation status | Related issue |
| - | - | - | - | - |
| `1.3.6.1.4.1.64165.1.1.1.1` | `webAuthnDeviceProfiles` | WebAuthn device profiles string | Assigned | N/A |
| `1.3.6.1.4.1.64165.1.1.2.1` | `webAuthnDeviceProfilesContainer` | Class containing WebAuthn device profiles | Assigned | N/A |
| `1.3.6.1.4.1.64165.2.1.3.1` | `TraceContextRequestControl` | OTEL trace context request control | N/A |

**Do not self-assign numbers**. When you create a new feature that requires an OID, describe the need and motivation in the feature’s pull request. In that PR, specify:

- The product, protocol, and (if applicable) schema branch the OID is intended for
- The proposed OID (or a request for the next available)

The reviewer will check for collisions, confirm the OID, and update this table. OIDs are permanent - they are never reused and remain listed forever.
