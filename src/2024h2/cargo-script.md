# cargo-scrpt

| Metadata |                                                                                                          |
| -------- | -------------------------------------------------------------------------------------------------------- |
| Owner(s) | epage                                                                                                    |
| Teams    | Cargo, Lang                                                                                              |
| Status   | Accepted in [rust-lang/rust-project-goals#22](https://github.com/rust-lang/rust-project-goals/issues/22) |

## Summary

Stablize support for "cargo script", the ability to have a single file that contains both Rust code and a `Cargo.toml`.

## Motivation

Being able to have a Cargo package in a single file can reduce friction in development and communication,
improving bug reports, educational material, prototyping, and development of small utilities.

### The status quo

Today, at minimum a Cargo package is at least two files (`Cargo.toml` and either `main.rs` or `lib.rs`).
The `Cargo.toml` has several required fields.

To share this in a bug report, people resort to
- Creating a repo and sharing it
- A shell script that cats out to multiple files
- Manually specifying each file
- Under-specifying the reproduction case (likely the most common due to being the eaisest)

To create a utility, a developer will need to run `cargo new`, update the
`Cargo.toml` and `main.rs`, and decide on a strategy to run this (e.g. a shell
script in the path that calls `cargo run --manifest-path ...`).

### The next six months

The support is already implemented on nightly.
The goal is to stabilize support.
With [RFC 3502][] and [RFC 3503][] approved, the next steps are being tracked in [#12207](https://github.com/rust-lang/cargo/issues/12207).

[RFC 3502]: https://github.com/rust-lang/rfcs/pull/3502
[RFC 3503]: https://github.com/rust-lang/rfcs/pull/3503

At a high-level, this is
- Add support to the compiler for the frontmatter syntax
- Add support in Cargo for scripts as a "source"
- Polish

### The "shiny future" we are working towards

## Design axioms

- In the trivial case, there should be no boilerplate.  The boilerplate should scale with the application's complexity.
- A script with a couple of dependencies should feel pleasant to develop without copy/pasting or scaffolding generators.
- We don't need to support everything that exists today because we have multi-file packages.

[da]: ../about/design_axioms.md

## Ownership and other resources

**Owner:** epage

This section defines the specific work items that are planned and who is expected to do them. It should also include what will be needed from Rust teams.

* Subgoal:
    * Describe the work to be done and use `↳` to mark "subitems".
* Owner(s) or team(s):
    * List the owner for this item (who will do the work) or ![Help wanted][] if an owner is needed.
    * If the item is a "team ask" (i.e., approve an RFC), put ![Team][] and the team name(s).
* Status:
    * List ![Help wanted][] if there is an owner but they need support, for example funding.
    * Other needs (e.g., complete, in FCP, etc) are also fine.

| Subgoal                           | Owner(s) or team(s) | Status |
| --------------------------------- | ------------------- | ------ |
| Implementation                    | Ed Page             |        |
| Stabilization decision from lang  | ![Team][] [Lang]    |        |
| Stabilization decision from cargo | ![Team][] [Cargo]   |        |

[Help wanted]: https://img.shields.io/badge/Help%20wanted-yellow
[Complete]: https://img.shields.io/badge/Complete-green
[TBD]: https://img.shields.io/badge/TBD-red
[Team]: https://img.shields.io/badge/Team%20ask-red

[Compiler]: https://www.rust-lang.org/governance/teams/compiler
[Lang]: https://www.rust-lang.org/governance/teams/lang
[LC]: https://www.rust-lang.org/governance/teams/leadership-council
[Libs-API]: https://www.rust-lang.org/governance/teams/library#team-libs-api
[Infra]: https://www.rust-lang.org/governance/teams/infra
[Cargo]: https://www.rust-lang.org/governance/teams/dev-tools#team-cargo
[Types]: https://www.rust-lang.org/governance/teams/compiler#team-types
