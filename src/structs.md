# Structs

## Abilities

There are 4 abilities in Move: `copy`, `drop`, `store`, and `key`.

```
struct ColorObject has key {
    id: UID,
    red: u8,
    green: u8,
    blue: u8,
}
```

Rules:
- Only specify the abilities that are needed.
- Never specify `drop` ability for structs which represents assets in case of accidental loss of assets.
- Never specify `copy` ability for structs which represents assets in case of accidental duplication of assets.
- `key` indicates that the struct can be stored as an object. If the struct will never be stored as an object independently, then do not specify `key` ability.
- In Sui Move, objects defined with only `key` ability can not be transferred by default. To enable transfers, publisher has to create a custom transfer function. If you want to disable general `public_transfer` for a struct(e.g. you want to charge a fee for ownership transfer), then use this pattern.
- A struct with no abilities is usually used as the [hot potato](https://examples.sui.io/patterns/hot-potato.html) pattern. In this struct, you must call function B after function A in the case where function A returns a potato and function B consumes it.

## Denial of Service with Unbounded Structs

The size of a struct is limited in Sui Network. If a struct is unbounded, then it can be used to cause a denial of service attack.

For example, if you have a global config struct to store all trading pairs as below, and it's permissionless to create an arbitrary trading pair.
Then an attacker can add a lot of trading pairs to the struct and cause a denial of service attack.

```
struct GlobalConfig {
    pairs: vector<TradingPair>,
}
```

To avoid this, you must guarantee that:

-  If the struct contains `vector`, `VecSet`, or `VecMap`, the number of elements must be limited.
-  If the size of a container is either unlimited or could grow significantly, you should consider using `Table` or `TableVec`. These containers store each key-value pair in a distinct object, so the size of the struct isn't impacted by the number of elements.

## References

- https://github.com/move-language/move/blob/main/language/documentation/book/src/abilities.md#abilities
- https://docs.sui.io/build/programming-with-objects/ch1-object-basics
- https://examples.sui.io/basics/custom-transfer.html
- https://examples.sui.io/patterns/hot-potato.html
