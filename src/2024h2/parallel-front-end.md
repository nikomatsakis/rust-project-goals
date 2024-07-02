# Stabilize Parallel Front End

| Metadata |                           |
| -------- |---------------------------|
| Owner(s) | [@SparrowLii]             |
| Teams    | [Parallel Rustc WG] |
| Status   | Existing problems need to be resolved to stabilize                          |

## Motivation

The parallel front end has been implemented in nightly, but there are still many problems that prevent it from being stable and used at scale.

### The status quo

Many current [issues] reflect ICE or deadlock problems that occur during the use of parallel front-ends. We need to resolve these issues to ensure functional correctness.

The existing compiler testing framework is not sufficient for the parallel front end, and we need to enhance it to ensure the correct functionality of the parallel front end.

The current parallel front end still has room for further improvement in compilation performance, such as parallelization of HIR lowering and macro expansion, and reduction of data contention under more threads (>= 16).

We can use parallel front end in bootstrap to alleviate the problem of slow build of the whole project.

### The next 6 months

- Solve most of the existing issues (unless they are due to lack of rare hardware environment or are almost impossible to reproduce).
- Improve the parallel compilation test framework and enable parallel front end in UI tests.
- Continue to improve parallel compilation performance, with the average speed increase from 30% to 40% under 8 cores and 8 threads.
- Enable parallel frontends in bootstrap.

### The "shiny future" we are working towards

The existing rayon library implementation is difficult to fundamentally eliminate the deadlock problem, so we may need a better scheduling design to eliminate deadlock without affecting performance.

The current compilation process with `GlobalContext` as the core of data storage is not very friendly to parallel front end. Maybe try to reduce the granularity (such as modules) to reduce data competition under more threads and improve performance.

## Design axioms

The parallel front end should be:
- safe: Ensure the safe and correct execution of the compilation process
- consistent: The compilation result should be consistent with that in single thread
- maintainable: The implementation should be easy to maintain and extend, and not cause confusion to developers who are not familiar with it.

[da]: ../about/design_axioms.md

## Ownership and other resources

**Owner:** [@SparrowLii] and [Parallel Rustc WG] own this goal

| Subgoal                              | Owner(s) or team(s) | Status |
|--------------------------------------|---------------------| ------ |
| Fix issues                           |                     |        |
| Test for parallel front end          |                     |        |
| ↳ use parallel front end in UI tests |                     |        |
| ↳ processe diagnostic output         |                     |        |
| Use parallel rustc in bootstrap      |                     |        |
| improve performance                  |                     |        |
| ↳ parallel HIR lowering              |                     |        |
| ↳ parallel macro expansion           |                     |        |

## Frequently asked questions


[@SparrowLii]: https://github.com/SparrowLii
[Parallel Rustc WG]: https://www.rust-lang.org/governance/teams/compiler#team-wg-parallel-rustc
[issues]: https://github.com/rust-lang/rust/labels/WG-compiler-parallel