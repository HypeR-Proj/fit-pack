<!--
SPDX-FileCopyrightText: 2026 roolrz
SPDX-License-Identifier: Apache-2.0
-->

# fit-pack

Host tool for constructing Linux guest FIT containers.

Combines kernel and initramfs payloads with architecture, load and entry metadata. Uses
`lib-vm-image` vocabulary so producer and Native loader agree on the image format.

See the [implementation entry](src/main.rs) and [component declaration](component.json)
for the public interfaces, build dependencies and delivered artifacts.

## Usage

On the host after building this tool:

```sh
hyper-fit-pack OUTPUT ARCH KERNEL LOAD ENTRY INITRAMFS
```

## Boundaries

ARCH is arm64 or riscv. Both payloads must be nonempty. This tool packages existing
artifacts; it does not compile Linux, sign images or run the guest. Identical output is
left unchanged.

## Build and test

Use this checkout inside the [repo-managed workspace](https://github.com/HypeR-Proj/HypeR).
From this repository directory:

```sh
make
make test
```

An absolute `OUT=/path/to/out` selects a shared output directory. The module
entry delegates to build/system, which prepares the installed SDK and declared
dependencies. Native binaries require HypeR; host module checks cover the tests
selected by component.json. A standalone clone does not contain the workspace’s
other source repositories or Native SDK.
