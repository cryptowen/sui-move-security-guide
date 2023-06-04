# Dependencies

The move package dependencies are specified in the `[dependencies]` section of `Move.toml` file.

A common issue is that the dependencies are not fixed to a specific version(e.g. a branch).
This can lead to unexpected behavior when the dependencies are updated.
For example, a function signature may change and cause compilation error.

To avoid this, it is recommended to fix the dependencies to a specific version(e.g. a commit hash or a tag).

```toml
[dependencies]
Sui = { git = "https://github.com/MystenLabs/sui.git", subdir = "crates/sui-framework/packages/sui-framework", rev = "devnet-v1.1.0" }
```

## References

- https://docs.sui.io/build/move/manifest#dependencies-section
