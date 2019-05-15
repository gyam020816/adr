This is a quick writedown of steps necessary to setup IntelliJ with Async Profiler integration.

## Install

- IntelliJ IDEA Ultimate **2019.1** is required.
- Follow the [IntelliJ installation guide](https://www.jetbrains.com/help/idea/cpu-profiler.html).
  - Ignore the *Using the profiler* section of the guide for now.
- Download and extract [async-profiler](https://github.com/jvm-profiling-tools/async-profiler#download).
- In *File | Settings | Build, Execution, Deployment | Java Profiler*.
  - Add *➕ | \[Async Profiler\] CPU*.
  - Set agent path to the absolute path of the `build/libasyncProfiler.so` file within your async-profiler folder.

## Run

Follow one of the following:
- If you want to profile a simple class execution, follow [IntelliJ guide](https://www.jetbrains.com/help/idea/cpu-profiler.html#UsingTheProfiler).
- If your execution is a bit more complex i.e. the project is started through `./run.sh` script or a long `mvn` goal, then:
  - Follow [async-profiler basic guide](https://github.com/jvm-profiling-tools/async-profiler#basic-usage).
  - Generate a report with the `collapsed` output format, see example below.
  - In IntelliJ, import the report from *Run | Import Profiler Results | From File...*.

```
# Assuming 21961 is the java process ID
./profiler.sh start 21961`
./profiler.sh -o collapsed -f myoutputfile.collapsed stop 21961`
```

## Troubleshooting

- Q: My *Run with Profiler* is grayed out and disabled?
- A: Did you configure *Java Profiler* in IntelliJ settings? See *Install* section above.
