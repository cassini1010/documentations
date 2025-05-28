# Timing your python code

## perf_counter

This is one of the best ways to calculate time taken by the code. 

> Note: Best time of the code can be calculated by selecting the lowest time of all the tries. Average of all the tries is not an efficient way, because of computer running other process in the background. The recorded lowest time is when the other processes has less influence.

## Timer class using `perf-counter`

```python
# timer.py

import time

class TimerError(Exception):
    """A custom exception used to report errors in use of Timer class"""

class Timer:
    def __init__(self):
        self._start_time = None

    def start(self):
        """Start a new timer"""
        if self._start_time is not None:
            raise TimerError(f"Timer is running. Use .stop() to stop it")

        self._start_time = time.perf_counter()

    def stop(self):
        """Stop the timer, and report the elapsed time"""
        if self._start_time is None:
            raise TimerError(f"Timer is not running. Use .start() to start it")

        elapsed_time = time.perf_counter() - self._start_time
        self._start_time = None
        print(f"Elapsed time: {elapsed_time:0.4f} seconds")
```

## timeit built in function

`timeit` is a builtin function used to time your code

`cProfile` can be used to identify which function  is taking longer time. 

`line_profiler` can be used to identify which line is taking long time to run.

`memory-profile` can be used to profile the memory consumption.

Suggested way if to first use `cProfile` to profile the functions and then use `line_profiler` to profile the lines of that function .
