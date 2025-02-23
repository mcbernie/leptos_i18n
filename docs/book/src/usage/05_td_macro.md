# The `td!` Macro

The `td!` macro works just like the `t!` macro but instead of taking the context as its first argument, it takes the desired locale:

```rust,ignore
td!(Locale::fr, hello_world)
```

This is useful if, for example, you want the buttons to switch locale to always be in the language they switch to:

```rust,ignore
use crate::i18n::*;
use leptos::prelude::*;

#[component]
pub fn Foo() -> impl IntoView {
    let i18n = use_i18n();

    view! {
        <For
            each = Locale::get_all
            key = |locale| **locale
            let:locale
        >
            <button on:click = move|_| i18n.set_locale(*locale)>
                {td!(*locale, set_locale)}
            </button>
        </For>
    }
}
```

This could just be written as

```rust,ignore
use crate::i18n::*;
use leptos::prelude::*;

#[component]
pub fn Foo() -> impl IntoView {
    let i18n = use_i18n();

    view! {
        <button on:click = move|_| i18n.set_locale(Locale::en)>
            {td!(Locale::en, set_locale)}
        </button>
        <button on:click = move|_| i18n.set_locale(Locale::fr)>
            {td!(Locale::fr, set_locale)}
        </button>
    }
}
```

But the above scale is better.
