# B𝛆 Tree library in Rust

[![Crates.io](https://img.shields.io/crates/v/be-tree.svg)](https://crates.io/crates/be-tree)
[![Docs](https://docs.rs/be-tree/badge.svg)](https://docs.rs/be-tree)
[![MIT/APACHE-2.0](https://img.shields.io/crates/l/be-tree.svg)](https://crates.io/crates/be-tree)
[![GitHub Workflow Status](https://img.shields.io/github/workflow/status/PsiACE/be-tree/Check%20Code?label=workflow)](https://github.com/PsiACE/be-tree/actions)

This is a port of [Dan Hulme](https://github.com/orac)'s [b𝛆-tree implementation](https://github.com/orac/be-tree). Since he does not seem to be active on GitHub and does not continue to maintain the library, I did a port.

**The following introduction is derived from the original. Thanks Dan!**

Well, that's the goal. This was started as a "mob programming" experiment at a Rust meetup. At the meetup we didn't get as far as implementing a plain B-tree, but it's a start, and I've made some further changes since the meetup.

The idea is to implement the B𝛆-tree data structure from [this 2015 paper][1].
It's a refinement of the B-tree for faster writing (at some cost to queries). Instead of pushing changes to the relevant leaf node immediately, each branch node contains a (persistent) command queue which buffers changes. Thus, the cost of loading child nodes from disk is amortised over several operations.

[1]: http://supertech.csail.mit.edu/papers/BenderFaJa15.pdf

Unfortunately, queries are no faster (and a little slower, because they need to read the command queue). Operations that need to read an existing value and then update it would still be slow. The authors added an extra operation, *upsert*, which reads the value (if any), applies an operation to it, and writes the modified value. Upserts can be stored into the command queue like insertions, so they get the same performance benefit as inserts.

## Alternatives
* [C++ implementation of the same data structure][2], 2-clause BSD licence

[2]: https://github.com/oscarlab/Be-Tree

## Contributors

Every member of the "mob" at the meetup should go in this contributor list.
If that's you, please send a pull request that adds your name to the list.

* Dan Hulme <dan@five.ai>

## Contact

Chojan Shang - [@PsiACE](https://github.com/psiace) - <psiace@outlook.com>

Project Link: [https://github.com/psiace/be-tree](https://github.com/psiace/be-tree)

## License

Licensed under either of:

- Apache License, Version 2.0 ([LICENSE-APACHE](./LICENSE-APACHE) or [http://apache.org/licenses/LICENSE-2.0](http://apache.org/licenses/LICENSE-2.0))
- MIT license ([LICENSE-MIT](./LICENSE-MIT) or [http://opensource.org/licenses/MIT](http://opensource.org/licenses/MIT))
