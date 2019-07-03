Desipte its name `annotated-libraries`, this repository contains only
binaries for the annotated JDK.  Binaries for other annotated libraries can
be found at https://search.maven.org/search?q=annotatedlib .

The Travis jobs that use the Checker Framework download the annotated JDK from
this repository.  Which version of the JDK is determined by the commit hash
`jdkShaHash` specified in `checker/build.gradle`.

If you commit to this repository, no build will use the new version.
This means that committing to this repository cannot break anyone else's
build, and that you need to update the Checker Framework to refer to the
version you added to this repository.


## How to update the binaries in this repository

If you make a pull request that changes the annotated JDK source code in
the [checker-framework](https://github.com/typetools/checker-framework)
repository, you should add a new annotated JDK binary to this repository.

1. In the branch that contains your Checker Framework pull request, do:
````
    git pull git@github.com:typetools/checker-framework.git
    ./gradlew buildJdk -PuseLocalJdk
````

2. Upload `checker/jdk/jdk8.jar` to this repository.
The commit message should mention the fork and branch.
For example: "Fork mernst, branch remove-nullness-rawness-checker"

You upload in two ways:
 * Commit in your clone of https://github.com/typetools/annotated-libraries .
    * `git pull`
    * Copy `checker/jdk/jdk8.jar` to this repository.
    * Commit
    * `git push`
 * Or via https://github.com/typetools/annotated-libraries/upload/master

3. In the branch that contains your Checker Framework pull request,
in file `checker/build.gradle`, set `jdkShaHash` to the hash of your
commit in this repository.  Commit and push.

4. Wait for Travis to successfully build the pull request.

5. If the pull request suffers a merge conflict on the line that contains
the commit hash, then start over at step 1.

6. Merge the pull request.  (Never merge any pull request that does not
pass its tests!)

