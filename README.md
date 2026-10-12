# siox-apb

The AMBA APB4 interface for [siox](https://github.com/Siox-lang/sioxc): one
struct with every signal, and one view per endpoint role.

- Struct: `Apb<A, D>`, where `A` address width, `D` data width (8, 16 or 32)
- Views: `Requester` and `Completer`

The clock and reset are not part of the struct; they stay ordinary ports of
the endpoint entities. See the header of `apb.siox` for what is left out.

## Use

Until siox has a package manager, put `apb.siox` at your project root (copy,
symlink or submodule) and import it:

```siox
use apb::{Apb, Completer};

entity Peripheral { clk: Bit in, bus: Apb<12, 32> Completer }
```

A parent connects a `Requester` and a `Completer` through one `let wire: Apb<12, 32>;`.

## Test

```bash
sioxc --std <sioxc>/std --test apb_test.siox -o apb_test && ./apb_test
```

`apb_test.siox` is a small completer driven by a testbench. Needs a
`sioxc` with Siox-lang/sioxc#68: width-parameterised struct ports.
