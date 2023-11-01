

# recordTimings
[![GitHub URL](https://img.shields.io/badge/github-repo-000.svg?logo=github&labelColor=gray&color=blue)](https://github.com/NLeSC/recordTimings) [![License](https://img.shields.io/github/license/citation-file-format/cff-converter-python)](https://github.com/citation-file-format/cff-converter-python) 

## Overview
recordTimings is a C++ header-only library that facilitates the recording of timing information during the execution of a program. It allows you to track the time spent on different tasks and operations within your code, enabling you to identify performance bottlenecks and optimize your application.

## Features

- **Accurate Timing:** recordTimings utilizes high-resolution clocks to ensure accurate timing measurements.
- **Support for Multi-threading:** The library supports multi-threaded applications and can handle timing measurements for each thread separately.
- **Support for CPU and GPU:** It can record timings for both CPU and GPU operations, providing insights into both types of computation.
- **Efficient Record-Keeping:** The library maintains a structured record of all recorded timings, including descriptions, time differentials, parent descriptions, and more.
- **FLOPS Calculation:** In addition to time measurements, recordTimings can calculate Floating-Point Operations Per Second (FLOPS) for specific operations.



# Usage
Add the recordTimings/record_timings.hpp header file to your C++ project and include it in your code. You can then make use of the following macros to instrument your code:

```cpp
RECORD_TIMINGS_INIT();
RECORD_TIMINGS_START(machine, desc_str);
RECORD_TIMINGS_STOP(machine, desc_str);
RECORD_TIMINGS_PARALLEL();
RECORD_TIMINGS_STOP_WITH_FLOPS(machine, desc_str, flops);
RECORD_TIMINGS_PRINT(stream);
RECORD_TIMINGS_DISABLE();
```
- `RECORD_TIMINGS_INIT()`:  should be called once outside main() function. It initializes the library and creates a root node in the timing tree.


- `RECORD_TIMINGS_START(machine, desc_str)`:  should be called at the start of a timed operation. It creates a new node in the timing tree and starts the timer.


- `RECORD_TIMINGS_STOP(machine, desc_str)`:  should be called at the end of a timed operation. The `desc_str` in `RECORD_TIMINGS_START` and `RECORD_TIMINGS_STOP` should be identical. It stops the timer and calculates the time differential between the start and stop times.


- `RECORD_TIMINGS_PARALLEL()`:  should be called before the start of a parallel region for initializing the thread-specific timing tree.


- `RECORD_TIMINGS_STOP_WITH_FLOPS(machine, desc_str, flops)`:  should be called at the end of a timed operation. The number of floating-point operations (flops) performed during the operations should be provided as the third argument. It is used to calculate the FLOPS for the operation.


- `RECORD_TIMINGS_PRINT(stream)`:  should be called at the end of the program to print the timing tree to the provided stream. The default stream is `std::cout`.


- `RECORD_TIMINGS_DISABLE()`: should be called at the beginning of the program to disable the library. It is useful for disabling the library without removing the instrumentation code.


