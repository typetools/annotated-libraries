# Annotated Libraries

Pre-built versions of several libraries containing additional specifications.

## Instructions for users

During type-checking, put these versions on your classpath,
to obtain more precise type-checking with fewer false positive warnings.


## Instructions for people creating a new annotated library

If you annotate a new library, please inform the Checker Framework developers
so that they can include it in the Checker Framework distribution.

For jdk8.jar, see file `README.jdk`.

When adding a .jar or .astub file to this directory, update the below list.
In general, old files need not be removed; that way, we accommodate users
regardless of which version of a library they wish to use.

The annotated source code appears at the following locations:

- bcel.jar : from https://github.com/typetools/commons-bcel (version 5.2)
- commons-bcel-6.0.jar : from https://github.com/typetools/commons-bcel
- commons-io-2.5.jar : from https://github.com/typetools/commons-io
                     to build, see its file README-typetools.md
- guava-19.0.jar : from https://github.com/typetools/guava
- java-getopt-1.0.14.jar : from https://github.com/typetools/java-getopt

javadoc.astub models the JavaDoc classes in the JDK's com.sun.javadoc package,
which are not exposed by ct.sym and therefore cannot be part of an
annotated JDK. These are annotated for the Index and Nullness checkers.

awt.astub annotated for the Nullness Checker with following command it can used :  
javac -processor nullness -Astubs=awt.astub:stubs MyFile.java  
