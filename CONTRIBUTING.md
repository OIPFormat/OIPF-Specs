# Contributing to OIPF

OIPF is specified by extraction, not invention. Contributions are most welcome when they
come **from a real deployment**.

## How to propose a change
1. Open an issue describing the use case and the gap in the current format.
2. Attach (or link) a concrete package that motivates the change.
3. Propose the minimal schema/spec change. Avoid speculative generality.

## Bar for promotion into the spec
A new object or field is promoted only when it has appeared, in materially the same shape,
in **at least two independent packages across two sites or domains**. Until then it lives
in the example as a package-local extension under `x-`.

## Versioning
Semantic versioning. Breaking changes to any schema bump the MAJOR version.
The format is pre-1.0 and unstable by design.
