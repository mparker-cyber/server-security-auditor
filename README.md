# Server Security Auditor

> Status: Planning

A defensive command-line tool that inspects a Linux server's security posture and produces a readable, evidence-based report without automatically changing the system.

## Goals

- Practice secure Python development and Linux administration.
- Detect common server-hardening gaps through transparent checks.
- Separate collection, evaluation, and reporting logic.
- Make every finding explainable and testable.
- Produce both human-readable and machine-readable reports.

## Initial scope

The first release will target a local Linux host. Remote scanning, Windows support, and automatic remediation are outside the initial scope.

## Planned checks

| Category | Example checks |
|---|---|
| System | Distribution, kernel, uptime, and time synchronization |
| Updates | Available security updates and reboot indicators |
| Accounts | Unexpected UID 0 accounts, inactive users, and password-policy settings |
| SSH | Root login, password authentication, protocol settings, and exposed configuration |
| Network | Listening services, interfaces, and firewall status |
| Services | Enabled services and failed units |
| Filesystem | Sensitive-file permissions and world-writable locations |
| Logging | Audit/logging services, retention indicators, and recent failures |
| Security tooling | Firewall, auditing, and endpoint-protection presence |

Checks will report observations and rationale; they will not claim compliance certification.

## Planned command interface

```bash
python -m server_security_auditor scan
python -m server_security_auditor scan --format json
python -m server_security_auditor check ssh
python -m server_security_auditor list-checks
```

## Planned repository structure

```text
.
├── README.md
├── pyproject.toml
├── src/
│   └── server_security_auditor/
│       ├── cli.py
│       ├── collectors/
│       ├── checks/
│       ├── models/
│       └── reporters/
├── tests/
│   ├── fixtures/
│   └── unit/
├── docs/
└── examples/
```

## Finding format

Each finding will contain:

- Check identifier and title
- Severity with stated rationale
- Observed evidence
- Expected secure state
- Recommended manual remediation
- Applicable limitations
- Reference links

## Milestones

- [ ] Define the finding schema and severity model.
- [ ] Build a read-only CLI skeleton.
- [ ] Implement system and account collectors.
- [ ] Add SSH, firewall, service, filesystem, and logging checks.
- [ ] Add JSON and Markdown reporters.
- [ ] Write unit tests using fixtures rather than the developer's live system.
- [ ] Add safe error handling for missing commands and permissions.
- [ ] Run tests in continuous integration.
- [ ] Publish sample sanitized reports.
- [ ] Document limitations and lessons learned.

## Security principles

- Read-only by default
- No credential collection
- No automatic remediation in the initial release
- Least privilege wherever possible
- Explicit handling of unavailable evidence
- No telemetry or data transmission

## Ethical use

Run this tool only on systems you own or are authorized to assess. Results must be reviewed by a qualified administrator before changes are made.
