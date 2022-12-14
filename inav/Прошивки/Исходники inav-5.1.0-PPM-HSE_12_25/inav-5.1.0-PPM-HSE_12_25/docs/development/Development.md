# Development

This document is primarily for developers only.

## General principals

1. Name everything well.
2. Strike a balance between simplicity and not-repeating code.
3. Methods that return a boolean should be named as a question, and should not change state.  e.g. 'isOkToArm()'
4. Methods that start with the word 'find' can return a null, methods that start with 'get' should not.
5. Methods should have verb or verb-phrase names, like `deletePage` or `save`.  Variables should not, they generally should be nouns.  Tell the system to 'do' something 'with' something.  e.g. deleteAllPages(pageList).
6. Keep methods short - it makes it easier to test.
7. Don't be afraid of moving code to a new file - it helps to reduce test dependencies.
8. Avoid noise-words in variable names, like 'data' or 'info'.  Think about what you're naming and name it well.  Don't be afraid to rename anything.
9. Avoid comments that describe what the code is doing, the code should describe itself.  Comments are useful however for big-picture purposes and to document content of variables.
10. If you need to document a variable do it at the declaration, don't copy the comment to the `extern` usage since it will lead to comment rot.
11. Seek advice from other developers - know you can always learn more.
12. Be professional - attempts at humor or slating existing code in the codebase itself is not helpful when you have to change/fix it.
13. Know that there's always more than one way to do something and that code is never final - but it does have to work.

Before making any code contributions, take a note of the https://github.com/multiwii/baseflight/wiki/CodingStyle

It is also advised to read about clean code, here are some useful links:

* http://cleancoders.com/
* http://en.wikipedia.org/wiki/SOLID_%28object-oriented_design%29
* http://en.wikipedia.org/wiki/Code_smell
* http://en.wikipedia.org/wiki/Code_refactoring
* http://www.amazon.co.uk/Working-Effectively-Legacy-Robert-Martin/dp/0131177052

## Unit testing

Ideally, there should be tests for any new code. However, since this is a legacy codebase which was not designed to be tested this might be a bit difficult.

If you want to make changes and want to make sure it's tested then focus on the minimal set of changes required to add a test.

Tests currently live in the `test` folder and they use the google test framework.
The tests are compiled and run natively on your development machine and not on the target platform.
This allows you to develop tests and code and actually execute it to make sure it works without needing a development board or simulator.

This project could really do with some functional tests which test the behaviour of the application.

All pull requests to add/improve the testability of the code or testing methods are highly sought!

Note: Tests are written in C++ and linked with with firmware's C code.

### Running the tests.

The tests and test build system is very simple and based off the googletest example files, it may be improved in due course. From the root folder of the project simply do:

Test are configured from the top level directory. It is recommended to use a separate test directory, here named `testing`.

```
mkdir testing
cd testing
# define NULL toolchain ...
cmake -DTOOLCHAIN= ..
# Run the tests
make check
```

This will build a set of executable files in the `src/test/unit` folder (below `testing`), one for each `*_unittest.cc` file.

After they have been executed by the make invocation, you can still run them on the command line to execute the tests and to see the test report, for example:

```
src/test/unit/time_unittest
Running main() from /home/jrh/Projects/fc/inav/testing/src/test/googletest-src/googletest/src/gtest_main.cc
[==========] Running 2 tests from 1 test suite.
[----------] Global test environment set-up.
[----------] 2 tests from TimeUnittest
[ RUN      ] TimeUnittest.TestMillis
[       OK ] TimeUnittest.TestMillis (0 ms)
[ RUN      ] TimeUnittest.TestMicros
[       OK ] TimeUnittest.TestMicros (0 ms)
[----------] 2 tests from TimeUnittest (0 ms total)

[----------] Global test environment tear-down
[==========] 2 tests from 1 test suite ran. (0 ms total)
[  PASSED  ] 2 tests.
```

You can also step-debug the tests in `gdb` (or IDE debugger).

The tests are currently always compiled with debugging information enabled, there may be additional warnings, if you see any warnings please attempt to fix them and submit pull requests with the fixes.

Tests are verified and working with (native) GCC 11.20.

## Using git and github

Ensure you understand the github workflow: https://guides.github.com/introduction/flow/index.html

Please keep pull requests focused on one thing only, since this makes it easier to merge and test in a timely manner.

If you need help with pull requests there are guides on github here:

https://help.github.com/articles/creating-a-pull-request/

The main flow for a contributing is as follows:

1. Login to github, go to the INAV repository and press `fork`.
2. Then using the command line/terminal on your computer: `git clone <url to YOUR fork>`
3. `cd inav`
4. `git checkout master`
5. `git checkout -b my-new-code`
6. Make changes
7. `git add <files that have changed>`
8. `git commit`
9. `git push origin my-new-code`
10. Create pull request using github UI to merge your changes from your new branch into `inav/master`
11. Repeat from step 4 for new other changes.

The primary thing to remember is that separate pull requests should be created for separate branches.  Never create a pull request from your `master` branch.

Later, you can get the changes from the INAV repo into your `master` branch by adding INAV as a git remote and merging from it as follows:

1. `git remote add upstream https://github.com/iNavFlight/inav.git`
2. `git checkout master`
3. `git fetch upstream`
4. `git merge upstream/master`
5. `git push origin master` is an optional step that will update your fork on github


You can also perform the git commands using the git client inside Eclipse.  Refer to the Eclipse git manual.

## Branching and release workflow

Normally, all development occurs on the `master` branch. Every release will have it's own branch named `release_x.y.z`.

During release candidate cycle we will follow the process outlined below:

1. Create a release branch `release_x.y.z`
2. All bug fixes found in the release candidates will be merged into `release_x.y.z` branch and not into the `master`.
3. After final release is made, the branch `release_x.y.z` is locked, and merged into `master` bringing all of the bug fixes into the development branch. Merge conflicts that may arise at this stage are resolved manually.
