### Summary

On Windows, running nested yarn commands from lint-staged hangs the process in 90% of cases.

    "scripts": {
        "foo1": "yarn foo2",
        "foo2": "yarn foo3",
        "foo3": "yarn foo4",
        "foo4": "echo Foo"
    },
    "lint-staged": {
        "linters": {
            "*": "yarn foo"
        }
    }

### Reproduce the issue

Checkout this repo and run yarn to install dependencies.

Modify a file and add the change to git:

    echo "test" >> README.md
    git add README.md

Then run:

    yarn lint-staged

It hangs forever in most cases (~9 out of 10).

### Specs

Reproduced on Windows 10 Enterprise, build 10586, in both regular command prompt and in Git Bash. 
Node version: 6.9.2.
Issue occurs with both yarn 1.3.2 and 1.5.1.

### Observations

Linux works fine.
Running `yarn foo1` directly works fine. The issue only occurs when lint-staged is involved.
Replacing `yarn` with `npm run` also works fine.

The repro rate can be lowered by using less nesting. I.e more nesting = more problems. Been able to reproduce with only one nested call.


