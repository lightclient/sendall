# `sendall`

This is an [`ekt`][etk] contract that sends all accrued value to coinbase.

## Getting Started

To setup a dev environment capable of assembling, analyzing, and executing the
repository's assembly you will need to install [`foundry`][foundry] and
[`etk`][etk]. This can be accomplished by running:

```console
$ curl -L https://foundry.paradigm.xyz | bash
$ cargo install --features cli etk-asm etk-dasm etk-analyze
```

## Building

To assemble `src/main.etk` you will need to invoke `eas`:

```console
$ eas src/main.etk
```

It's also possible to remove the `etk` preproccessing by doing a roundtrip --
first assembling the program, then disassembling the program:

```console
$ disease --code 0x$(eas src/main.etk)
```

### Control-flow Graph

`etk` has the ability to generate a [control-flow graph][cfg] to analyze the
possible paths the code may execute under. To generate, you  need `graphviz`.
Installation instructions can be found [here][graphviz].

The diagram can then be generated using the following:

```console
ecfg -c 0x$(eas ./src/main.etk) | dot -Tpng -o out.png
```

Open `out.png` with your choice of image viewer.

## Testing

The tests can be executed using the `builder-wrapper` script with the same
arguments as [forge][forge]:

```console
$ ./build-wrapper test
[⠆] Compiling...
No files changed, compilation skipped

Running 2 tests for test/Contract.t.sol:ContractTest
[PASS] testRead() (gas: 18514)
[PASS] testUpdate() (gas: 53953)
Test result: ok. 2 passed; 0 failed; 0 skipped; finished in 3.35ms
Ran 1 test suites: 2 tests passed, 0 failed, 0 skipped (2 total tests)
```

A step-by-step debugger can be brought up using `./build-wrapper test --debug {test name}`.

[cfg]: https://en.wikipedia.org/wiki/Control-flow_graph
[etk]: https://github.com/quilt/etk
[forge]: https://github.com/foundry-rs/foundry/blob/master/forge
[foundry]: https://getfoundry.sh/
[graphviz]: https://graphviz.org/download/
