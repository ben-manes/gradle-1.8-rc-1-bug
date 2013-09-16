An example of [dependency resolution leak](http://forums.gradle.org/gradle/topics/_gradle_1_8_rc_1_alternative_to_latestversionsemanticcomparator)
bug. To switch gradle versions, update the URL in `gradle/wrapper/gradle.properties`.

## Gradle 1.7
```
$ ./gradlew printDependencies
:a:printDependencies
a) Delcared:
 - DefaultExternalModuleDependency{group='backport-util-concurrent', name='backport-util-concurrent', version='3.1', configuration='default'}
 - DefaultExternalModuleDependency{group='backport-util-concurrent', name='backport-util-concurrent-java12', version='3.1', configuration='default'}
a) Resolved:
 - backport-util-concurrent:backport-util-concurrent:3.1;default
 - backport-util-concurrent:backport-util-concurrent-java12:3.1;default
:b:printDependencies
b) Delcared:
 - DefaultExternalModuleDependency{group='com.google.inject', name='guice', version='2.0', configuration='default'}
 - DefaultExternalModuleDependency{group='com.google.inject.extensions', name='guice-multibindings', version='2.0', configuration='default'}
b) Resolved:
 - com.google.inject:guice:2.0;default
 - com.google.inject.extensions:guice-multibindings:2.0;default
```

## Gradle 1.8-rc-1
```
$ ./gradlew printDependencies
:a:printDependencies
a) Delcared:
 - DefaultExternalModuleDependency{group='backport-util-concurrent', name='backport-util-concurrent', version='3.1', configuration='default'}
 - DefaultExternalModuleDependency{group='backport-util-concurrent', name='backport-util-concurrent-java12', version='3.1', configuration='default'}
a) Resolved:
 - backport-util-concurrent:backport-util-concurrent:3.1;default
 - backport-util-concurrent:backport-util-concurrent-java12:3.1;default
:b:printDependencies
b) Delcared:
 - DefaultExternalModuleDependency{group='com.google.inject', name='guice', version='2.0', configuration='default'}
 - DefaultExternalModuleDependency{group='com.google.inject.extensions', name='guice-multibindings', version='2.0', configuration='default'}
b) Resolved:
 - backport-util-concurrent:backport-util-concurrent:3.1;default
 - backport-util-concurrent:backport-util-concurrent-java12:3.1;default

$ ./gradlew :b:printDependencies
:b:printDependencies
b) Delcared:
 - DefaultExternalModuleDependency{group='com.google.inject', name='guice', version='2.0', configuration='default'}
 - DefaultExternalModuleDependency{group='com.google.inject.extensions', name='guice-multibindings', version='2.0', configuration='default'}
b) Resolved:
 - com.google.inject:guice:2.0;default
 - com.google.inject.extensions:guice-multibindings:2.0;default
```
