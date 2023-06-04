# Ownership and Mutability

There are 3 different types when we pass a parameter to a function: `move`, `borrow`, and `borrow_mut`.

Pass only the parameter with the minimum required capability.

For example, you should never pass a parameter with `&mut` or ownership to a function if you only need to read the value.

## Consumptions

There is an implicit consumption in Sui move: if you can pass a parameter to a function via RPC, you have the ownership of the object, or the object is shared.

With this consumption, we can use the [capability pattern](https://examples.sui.io/patterns/capability.html) in the authorization design.

However, if you break this consumption, you may cause security issues.

For example, if you put a capability object in a global shared object(to lock it or control the capability with programming on purpose),
if the global shared objects provides read access to the inside objects, then the capability object might be leaked.
Everyone can use the capability object to call the functions that are supposed to be called by the owner only.

## References

- <https://examples.sui.io/patterns/capability.html>
