# Building tests

Currently, the test cannot build because two rules generate the `test.js` file. This bug seems to only exist on `rules_ts` versions 1.0.0-rc8 and later.

To experience the issue, run the following command:

```sh
bazel build ...
```

You'll then see this error:

```txt
ERROR: file 'test.js' is generated by these conflicting actions:
Label: //:lib_transpile, //:test
RuleClass: swc_transpiler rule, js_test rule
Configuration: 8c7c8a83495a6b29f5e61b94373e857884c6b6f4ed04fcd868a9a81a5d062e34, 222396ca991008122b08cb633987f96b0458f6baaffef89066aa1b9535cd8cb9
Mnemonic: SWCTranspile, CopyFile
Action key: a63cd422c122b2163583001b8c2480800edd01bb4440bf438d81dd7d4d6d58af, fb400ad9a47e0d5d16818ece44b8e73612ccea044664fd86caee7348e07df5fe
Progress message: Transpiling with swc //:lib_transpile [swc bazel-out/darwin_arm64-fastbuild/bin/test.ts], Copying file test.js
PrimaryInput: File:[[<execution_root>]bazel-out/darwin_arm64-fastbuild/bin]test.ts, File:[/repo/bazel-ts-update[source]]test.js
PrimaryOutput: File:[[<execution_root>]bazel-out/darwin_arm64-fastbuild/bin]test.js
ERROR: com.google.devtools.build.lib.skyframe.ArtifactConflictFinder$ConflictException: com.google.devtools.build.lib.actions.MutableActionGraph$ActionConflictException: for test.js, previous action: action 'Copying file test.js', attempted action: action 'Transpiling with swc //:lib_transpile [swc bazel-out/darwin_arm64-fastbuild/bin/test.ts]'
INFO: Elapsed time: 0.415s
INFO: 0 processes.
FAILED: Build did NOT complete successfully (30 packages loaded, 478 targets configured)
```

To run this test using `rules_ts` version 1.0.0-rc7, just uncomment it in the WORKSPACE file.
