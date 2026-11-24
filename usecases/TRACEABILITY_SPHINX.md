---
id: traceability
title: Traceability with Sphinx-Needs
summary: Requirements traced to ECUs, models and tests, as docs-as-code
category: process
example: .
domains: [lighting]
protocols: []
key_files:
  - docs/README.md
  - docs/index.rst
  - docs/requirements
  - docs/verification
  - docs/ubproject.toml
related: [pytest, behave]
run:
  commands:
    - pip install -r docs/requirements.txt
    - sphinx-build -W -b html docs build/html
  after: Open build/html/index.html.
screenshot:
  kind: manual
---

# Traceability with Sphinx-Needs

[Sphinx-Needs](https://sphinx-needs.readthedocs.io/) allows you to combine Docs-as-Code with Application Lifecycle
Management, to track requirements, specifications, test cases, and other engineering objects in your documentation.

This example adds ISO 26262-style traceability to RemotiveCar, developed together with [useblocks](https://useblocks.com/).
It is a limited sample of what the full documentation would look like: features, system and component requirements,
the ECUs, channels and behavioral models of the platform, the test cases that verify them, and FMEA entries, all as
linked "needs" in `.rst` files next to the code.

```
Feature <- (satisfies) <- System Req <- (satisfies) <- Component Req <- (verifies) <- Test Case
                                                             ^
                                                  (mitigates) FMEA Entry
```

- Part of the [RemotiveCar example](../DOCS.md)
- [Using Sphinx-Needs](../docs/README.md): what the project contains, how to build it and the tools available
- Need types, link types and fields: [ubproject.toml](../docs/ubproject.toml)
- Validation rules that run on every build: [schemas.json](../docs/schemas.json)

Build the HTML documentation (PlantUML and Python 3.10 or later are needed):

```bash
pip install -r docs/requirements.txt
sphinx-build -W -b html docs build/html
```

Then open `build/html/index.html`.

Notice:
- `-W` turns warnings into errors, so a missing ASIL rating or a test case that verifies nothing fails the build.
