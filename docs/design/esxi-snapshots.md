# ESXi snapshots

| Item | Value |
|---|---|
| VM | Windows Server 2025 domain controller (sypheit.com) |
| Snapshot name | Before-FSSO-LDAPS-NPS-working |
| Taken on | 2026-11-12 |
| Memory included | No |
| State captured | AD DS, DNS, AD CS, LDAPS, NPS and WPA2-Enterprise Wi-Fi all working |
| Matching repo tag | phase0-complete |

To restore: shut the VM down, then Actions > Snapshots > Manage snapshots > Restore.
Anything changed on the DC after this snapshot is lost on restore.
