# Quick Start

Ape compiler plugin around [the Cairo language](https://github.com/starkware-libs/cairo-lang).

## Dependencies

- [python3](https://www.python.org/downloads) version 3.8 or greater, python3-dev

## Installation

### via `pip`

You can install the latest release via [`pip`](https://pypi.org/project/pip/):

```bash
pip install ape-cairo
```

### via `setuptools`

You can clone the repository and use [`setuptools`](https://github.com/pypa/setuptools) for the most up-to-date version:

```bash
git clone https://github.com/ApeWorX/ape-cairo.git
cd ape-cairo
python3 setup.py install
```

## Quick Usage

### Installing Binaries

First, you must ensure you have the `sierra-compile` binary in your `$PATH`.
To obtain Cairo binaries, you can download them from their GitHub (provided there is one for your OS) as well build them yourself.

To build them yourself, first clone the `https://github.com/starkware-libs/cairo` repository.
Then run:

```bash
cargo build --release
```

After that, copy the binaries from `target/release` to a folder that is in your `$PATH`.

```bash
cp ./target/release/sierra-compile path/in/PATH
```

Verify you have `sierra-compile` in your `$PATH` by doing:

```bash
which sierra-compile
```

### Using the Compiler

In a project directory where there are `.cairo` files in your `contracts/` directory, run the `compile` command:

```bash
ape compile
```

It should create `ContractType` objects in your `.build/` folder containing the necessary Sierra code for contract declaration.

### Configure Dependencies

You can configure dependencies, such as from `GitHub`, using your `ape-config.yaml` file.

There are two things you need to add:

1. Add your dependency to Ape's root `dependencies:` key to trigger downloading and compiling it.
2. Configure the `ape-cairo` plugin to load that dependency in your project.

For more information on dependencies, [see this guide](https://docs.apeworx.io/ape/stable/userguides/config.html#dependencies).

Your `ape-config.yaml` will look something like:

```yaml
dependencies:
  - name: OpenZeppelinCairo
    github: OpenZeppelin/cairo-contracts
    version: 0.1.0
    contracts_folder: src

cairo:
  dependencies:
    - OpenZeppelinCairo@0.1.0
```

**NOTE**: We are changing the `contracts/` folder to be `src` for this dependency.

Now, in my `contracts/` folder, I can import from `openzeppelin`:

```cairo
from openzeppelin.token.erc20.library import (
    ERC20_name,
    ERC20_symbol,
    ERC20_totalSupply,
    ERC20_decimals,
    ERC20_balanceOf,
    ERC20_allowance,
    ERC20_mint,
    ERC20_burn,
    ERC20_initializer,
    ERC20_approve,
    ERC20_increaseAllowance,
    ERC20_decreaseAllowance,
    ERC20_transfer,
    ERC20_transferFrom
)
```

## Development

This project is in development and should be considered a beta.
Things might not be in their final state and breaking changes may occur.
Comments, questions, criticisms and pull requests are welcomed.
