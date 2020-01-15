# Example structure

First, the name of the package (as specified in `Cargo.toml`) is `dining`. This name is used as the library crate name; if you've got a combination binary/library package (in other words, you have both `src/lib.rs` _and_ `src/main.rs`), you can reference and import the library crate from the binary crate using this name.

I've done this -- `src/lib.rs` is the library crate root. Within the library crate root, I've declared two public modules: `front_of_restaurant` and `back_of_restaurant`.

Inside `src/lib/front_of_restaurant.rs` there are two public submodules declared: `hosting` and `serving`. Similarly, `src/lib/front_of_restaurant.rs` declares two public submodules: `cooking` and `management`.

`src/front_of_restaurant/serving.rs` defines a public function `take_payment`. `src/back_of_restaurant/management.rs` defines a public function `balance_accounts`.

Within a crate the keyword `crate` can be used to specify a path that starts at the crate root. (it's similar to the `/` directory on unix-like systems). So, inside `take_payment`, we can reference the `balance_accounts` function using the absolute path `crate::back_of_restaurant::management::balance_accounts`.

# Binary vs Library crates

Another possible source of confusion is the split between binary and library crates. `src/main.rs` is the root of a binary crate, while `src/lib.rs` is the root of the library crate. To reference (via use, or otherwise) items from the _library_ crate, it needs to be specified by _name_ -- trying to use `crate::...` won't work if you've defined your tree of modules in `src/lib.rs`.

For example, to call our `take_payment` function (which is in the _library_ crate) from our `main` function, you'd use the path `dining::front_of_restaurant::serving::take_payment`.
