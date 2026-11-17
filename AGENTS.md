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

## CI scheduling

The complete dependency audit, strict YAML lint and schema tests run for every
pull request to master and every master push on each provider. Feature pushes
remain excluded. Superseded pull-request runs can cancel; main runs remain
independent. Python dependency caching uses the complete requirements file and
does not replace the audit or install step. Checkout does not retain credentials.
Do not split schema tests across workers without preserving the global
duplicate-slug check.
