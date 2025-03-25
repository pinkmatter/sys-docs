# Runtime configuration

> Back to the [Processing Page](../processing.md)

## Background

Runtimes are meant to serve as the context in which processing jobs are executed within.

> FarEarth currently supports three types of *Runtime* **types**, and these are defined as:

* **[kubernetes](runtime-kubernetes.md)**: A language agnostic runtime which interfaces with the Processor app via an MQTT messaging bus.
* **[java-cmdline](runtime-java-cmdline.md)**: In single node static environments, a Java processing process is spawn on the same machine the Processor app resides on.
* **[java-classpath](runtime-java-classpath.md)**: Primarily for testing purposes. The Java application is executed within the same JVM as the Processor app.

> Back to the [Processing Page](../processing.md)