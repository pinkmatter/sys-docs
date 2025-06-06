# Runtime configuration

##### [Home](../../README.md) > [Processing](../processing.md) > Runtimes
---

Runtimes provide the context in which processing jobs are executed.

*FarEarth* supports these runtime "types":

* [kubernetes](runtime-kubernetes.md): A language agnostic runtime which interfaces with a *FarEarth* Processor app, via an MQTT messaging bus
* [java-cmdline](runtime-java-cmdline.md): A Java processing process started by the *FarEarth* Processor app, on the same machine as itself
* [java-classpath](runtime-java-classpath.md): A Java processing process started within the same JVM as the *FarEarth* Processor app (primarily used for testing only)

