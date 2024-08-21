# llvm-test-suite-legacy

Adapts an older version of LLVM's external test suite to run on the LNT testing infrastructure.

This adaptation allows tests to be run in a temporary sandbox, instead of using `Make` in the llvm's build directory. It produce more consistent test results and avoiding certain linking problems.

The older version of the LLVM test suite assumes the compiler under test is `llvm-gcc`, with tests compiled in multiple steps: starting with `llvm-gcc`, optimizing with LLVM's `opt`, and finally linking with the system's `gcc`. The output of execution of this compilation unit is then compared with that from the system's compiler. The newer testing infrastructure compiles the tests in a single stage and compares the output with a reference output.

The main branch contains test suite for `llvm-3.0`, the oldest version which LNT can reliably run.

## Example Usage
To run `llvm-2.7` test on `llvm/clang-2.7`, run:
```
git checkout 2.7
lnt runtest nt     --sandbox /tmp/SANDBOX     --cc ~/llvm-2.7-build/Release/bin/clang     --test-suite ~/llvm-test-suite-legacy/ --cflag=-fPIC -j32
```