The Travis jobs that use the Checker Framework download the annotated JDK from
this repository. Which version of the JDK is determined by the commit hash
specified in checker/build.xml.

Therefore, if some pull request changes the annotated JDK, a new version built
using the pull request should be added to this repository.  The pull request
should then update checker/build.gradle to use the commit hash of the new version.
If a conflict on this line occurs, then merge master into the pull request and
start over.

More specifically, you should:

1. In the branch that contains your Checker Framework pull request, do:
````
    git pull git@github.com:typetools/checker-framework.git
    ./gradlew buildJdk
````

2. To use the built version of the jdk8.jar in another tasks, pass `-PlocalJdk`. For example,
````
./gradlew allNullnessTest -PlocalJdk
````

3. Upload checker/dist/jdk8.jar (or checker/jdk/jdk8.jar, they are the same)
to this repository.  You can do by committing it to
https://github.com/typetools/annotated-libraries or via
https://github.com/typetools/annotated-libraries/upload/master.

4. In the branch that contains your Checker Framework pull request,
in file `checker/build.gradle`, in the `downloadJdk` task,
assign the hash of your commit to shaHash.

5. Wait for Travis to successfully build the pull request.

6. If the pull request suffers a merge conflict on the line that contains
the commit hash, then start over at step 1.

7. Merge the pull request.  (Never merge any pull request that does not
pass its tests!)

