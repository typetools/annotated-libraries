Despite its name `annotated-libraries`, this repository contains only
binaries for the annotated JDK.  Binaries for other annotated libraries can
be found at https://search.maven.org/search?q=annotatedlib .

The Checker Framework can download the annotated JDK from this repository
rather than building it, which would take a long time.  Which version of
the JDK is determined by the commit hash `jdkShaHash` specified in
`checker/build.gradle`.

If you commit to this repository, no build will use the new version.
This means that:
 * committing to this repository cannot break anyone else's build, and
 * you need to update the Checker Framework to refer to the
   version you added to this repository.


## How to update the binaries in this repository

If you make a pull request that changes the annotated JDK source code in
the [checker-framework](https://github.com/typetools/checker-framework)
repository, you should add a new annotated JDK binary to this repository.

(You also need to make the same edits in the Java 11  annotated JDK, in
repository https://github.com/typetools/jdk.  Ensure that each of the pull
requests refers to the other, so that they can be merged at the same time.)

1. In the branch that contains your Checker Framework pull request, run
(using JDK 8):
````
    git pull git@github.com:typetools/checker-framework.git
    ./gradlew buildJdk -PuseLocalJdk
````

2. Upload `checker/jdk/jdk8.jar` to this repository.
   The commit message should mention the fork and branch.
   For example: "Fork mernst, branch remove-nullness-rawness-checker"

   If you do not have write permission in this repository, make a pull
   request, which the maintainers should merge rather than squash-and-merge.

   If you have write permission to this repository,
   you upload in one of two ways:
   * Commit in your clone of https://github.com/typetools/annotated-libraries .
     * `git pull`
     * Copy `checker/jdk/jdk8.jar` to this repository.
     * Commit
     * `git push`
   * Or via https://github.com/typetools/annotated-libraries/upload/master

3. In the branch that contains your Checker Framework pull request,
in file `checker/build.gradle`, set `jdkShaHash` to the hash of your
commit in this repository.  Commit and push.

4. Wait for CI to successfully build the pull request.  If the pull request
suffers a merge conflict on the line that contains the commit hash, then
start over at step 1.

5. Merge the pull request.  (Never merge any pull request that does not
pass its tests!)


## How to determine from what sources a particular annotated JDK binary was built

Running `unzip -p jdk8.jar META-INF/MANIFEST.MF` outputs something like:

````
Manifest-Version: 1.0
Checker-Framework-Version: 2764d848a
Creation-Date: Wed 03 Jul 2019 03:57:29 PM PDT
Created-By: 1.8.0_212 (Oracle Corporation)
````

The `Checker-Framework-Version` is the commit hash from which the annotated JDK was built.
The commit message should tell you from which fork and branch of the Checker Framework
the sources are.
