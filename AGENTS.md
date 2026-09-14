# Repository Agent Guide

This repository stores NetBox device-type and module-type YAML definitions.
Changes must preserve schema validity and the established formatting rules.

## Validation

Use Python 3.12 and install the pinned dependencies from `requirements.txt`.
Before submitting a change, run:

```bash
pip-audit --progress-spinner off -r requirements.txt
yamllint --format parsable --strict -c=tests/yamllint.yaml device-types/ module-types/
pytest --tb=short -v
```

Do not suppress dependency advisories, weaken the YAML rules, or skip schema
validation to make a change pass. Update the affected dependency or definition
and retain a reproducible validation result.

## Scope

Keep dependency-security changes separate from device definition changes.
Update `README.md` whenever the supported validation runtime or commands
change.
