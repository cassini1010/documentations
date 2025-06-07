# Timing Your Python Code

## perf_counter

This is one of the best ways to measure the time taken by your code.

> Note: The best timing for your code can be determined by selecting the lowest time from all the attempts. Taking the average of all attempts is not efficient, because your computer may be running other processes in the background. The lowest recorded time is when other processes have the least influence.

## Timer Class Using `perf_counter`

```python
# timer.py

import time

class TimerError(Exception):
    """A custom exception used to report errors in the use of the Timer class"""

class Timer:
    def __init__(self):
        self._start_time = None

    def start(self):
        """Start a new timer"""
        if self._start_time is not None:
            raise TimerError("Timer is already running. Use .stop() to stop it.")

        self._start_time = time.perf_counter()

    def stop(self):
        """Stop the timer and report the elapsed time"""
        if self._start_time is None:
            raise TimerError("Timer is not running. Use .start() to start it.")

        elapsed_time = time.perf_counter() - self._start_time
        self._start_time = None
        print(f"Elapsed time: {elapsed_time:0.4f} seconds")
```

## timeit Built-in Function

`timeit` is a built-in function used to time your code.

`cProfile` can be used to identify which function is taking the most time.

`line_profiler` can be used to identify which line is taking the longest to run.

`memory_profiler` can be used to profile memory consumption.

The suggested approach is to first use `cProfile` to profile the functions, and then use `line_profiler` to profile the lines within those functions.
