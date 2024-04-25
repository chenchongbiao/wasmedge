# NAME

**wasmedge-compile** - AOT compiler for WasmEdge

# SYNOPSIS

**wasmedge compile** [*OPTIONS*] [`--`] `WASM_OR_SO` [*ARG* `...`]

# DESCRIPTION

The **wasmedge compile** subcommand compiles WebAssembly into native machine code, i.e. it is an Ahead-of-Time (AOT) compiler.

For pure WebAssembly, the **wasmedge**(1) program (or the equivalent **wasmedge run** subcommand) will execute the WebAssembly code in interpreter mode.  However, after compiling it with the **wasmedge compile** AOT compiler, the **wasmedge** subcommand can execute the WASM in AOT mode, with substantial performance improvements.

**wasmedge compile** was previously known as **wasmedgec**.

# OPTIONS

## Generic program information

`-h`, `--help`

:   Show the help messages. Will ignore other arguments below.

`-v`, `--version`

:   Show the version information. Will ignore other arguments below.

## Basic options

`--dump`

:   Dump the LLVM IR to `wasm.ll` and `wasm-opt.ll`.

`--interruptible`

:   Generate a binary that supports interruptible execution.

`--generic-binary`

:   Generate a generic binary of the current host CPU architecture.

`--optimize`

:   Use `--optimize LEVEL` to set the optimization level. The `LEVEL` should be one of `0`, `1`, `2`, `3`, `s`, or `z`.
    The default value will be `2`, which means `O2`.

## Statistics information

`--enable-time-measuring`

:   Enable generating code for counting time during execution.

`--enable-gas-measuring`

:   Enable generating code for counting gas burned during execution.

`--enable-instruction-count`

:   Enable generating code for counting WebAssembly instructions executed.

`--enable-all-statistics`

:   Enable generating code for all statistics options include instruction counting, gas measuring, and execution time.

## WebAssembly proposals

`--disable-import-export-mut-globals`

:   Disable Import/Export of mutable globals proposal.

`--disable-non-trap-float-to-int`

:   Disable Non-trapping float-to-int conversions proposal.

`--disable-sign-extension-operators`

:   Disable Sign-extension operators proposal.

`--disable-multi-value`

:   Disable Multi-value proposal.

`--disable-bulk-memory`

:   Disable Bulk memory operations proposal.

`--disable-reference-types`

:   Disable Reference types proposal.

`--disable-simd`

:   Disable SIMD proposal.

`--enable-multi-memory`

:   Enable Multiple memories proposal.

`--enable-tail-call`

:   Enable Tail-call proposal.

`--enable-extended-const`

:   Enable Extended-const proposal.

`--enable-threads`

:   Enable Threads proposal.

`--enable-all`

:   Enable all features.

# EXAMPLE

Assuming a WebAssembly program placed under the file `fibonacci.wasm`, set up
so to export a `fib()` function and accepting a single `i32` integer as the
input parameter, one can execute the following:

```bash
$ wasmedge compile fibonacci.wasm fibonacci_aot.wasm
$ time wasmedge --reactor fibonacci_aot.wasm fib 30
```

The execution should be much faster compared to interpreter mode:

```bash
time wasmedge --reactor fibonacci.wasm fib 30
```

# AUTHOR

Copyright (c) 2019-2022 Second State INC. Licensed under the Apache License,
Version 2.0.

# SEE ALSO

## Regular manual pages

**wasmedge**(1)

## Full documentation

A [complete manual of WasmEdge](https://wasmedge.org/docs/) can be found online.
