Desipte its name `annotated-libraries`, this repository contains only
the annotated JDK.  Other annotated libraries can be found at
https://search.maven.org/search?q=annotatedlib .

The Travis jobs that use the Checker Framework download the annotated JDK from
this repository. Which version of the JDK is determined by the commit hash
jdkShaHash specified in checker/build.gradle.

Therefore, if some pull request changes the annotated JDK, a new version built
using the pull request should be added to this repository.  The pull request
should then update checker/build.gradle to use the commit hash of the new
version.  If a conflict on this line occurs, then merge master into the pull
request and start over.

More specifically, you should:

1. In the branch that contains your Checker Framework pull request, do:
````
    git pull git@github.com:typetools/checker-framework.git
    ./gradlew buildJdk -PuseLocalJdk
````

2. Upload `checker/jdk/jdk8.jar` to this repository.
You can do so by committing it to
https://github.com/typetools/annotated-libraries and pushing, or via
https://github.com/typetools/annotated-libraries/upload/master.

3. In the branch that contains your Checker Framework pull request,
in file `checker/build.gradle`, set `jdkShaHash` to the hash of your
commit in this repository.  Commit and push.

4. Wait for Travis to successfully build the pull request.

5. If the pull request suffers a merge conflict on the line that contains
the commit hash, then start over at step 1.

6. Merge the pull request.  (Never merge any pull request that does not
pass its tests!)

