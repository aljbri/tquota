# TQuota

[![GitHub Release](https://img.shields.io/github/v/release/aljbri/tquota)](https://github.com/aljbri/tquota/releases/latest)
[![GitHub License](https://img.shields.io/github/license/aljbri/tquota)](https://github.com/aljbri/tquota/blob/master/LICENSE)
[![PyPI - Python Version](https://img.shields.io/pypi/pyversions/tquota)](https://pypi.org/project/tquota)
[![PyPI - Format](https://img.shields.io/pypi/format/tquota)](https://pypi.org/project/tquota)
[![PyPI - Version](https://img.shields.io/pypi/v/tquota)](https://pypi.org/project/tquota)
<!--
[![wheel](https://img.shields.io/pypi/wheel/tquota)](https://pypi.org/project/tquota)
[![PyPI - Downloads](https://img.shields.io/pypi/dm/tquota)]()
-->

`tquota.Quota` is a lightweight processing timer module designed to monitor time effectively when running code on cloud platforms with quota limitations, such as [Kaggle](https://www.kaggle.com/) and [Google Colab](https://colab.research.google.com/). These platforms impose a limit of `x` hours of processing per session, the `Quota` class allows users to set a processing quota time and a buffer time before the quota limit ends, ensuring efficient resource management.

## Features

- **Quota Management**: Easily track and manage session time to avoid overuse of limited resources on platforms with quota restrictions.
- **Dynamic Gap Timing**: Automatically adjusts the buffer time (`gap_time`) based on the remaining session time when set to `'auto'`.
- **Auto Gap Calculation**: When `gap_time` is set to `'auto'`, the system dynamically calculates the optimal gap before the session ends, ensuring efficient timing without the need for manual setup.
- **Simple Interface**: The class provides Easy-to-use and intuitive methods to check whether time is still available or if the session has reached its limit.
- **Optional Logging**: Enable logging to track quota usage and gap timing for debugging or monitoring purposes.
- **Compatibility**: It can work with Python versions 2.7 and 3.0+.

---
## Quota Class

The package `tquota` includes a single class, `Quota`, which has two main parameters and an optional one:

* **quota_time**: (str) Default value: `6h`. Represents the maximum processing time for the session.
* **gap_time**: (str) Default value: `'auto'`. Represents the buffer time before the session closes, adjusted dynamically based on elapsed time.
* **enable_logging**: (bool, optional) Default value: `False`. Whether to enable logging or not.

### Time Format

The time should be specified in a strict format, consisting of two parts: *`dw`*, where: 
- **d**: Represents the time as digits
- **w**: Represents the time unit with one character:

    [ s: Seconds, m: Minutes, h: Hours, d: Days]

## Functions

The `Quota` class provides the following key methods:

**`time_up`**:
  - **Description**: This method checks whether the processing time has reached or exceeded its quota limit.
  - **Returns**: 
    - `True`: If the process has reached or exceeded the defined quota time.
    - `False`: If there is still time remaining within the quota limit.
  - **Usage**:
    ```python
    if qt.time_up():
        print('Time limit reached.')
    ```

**`hastime`**:
  - **Description**: This method checks whether there is still time left before the process reaches the quota limit.
  - **Returns**: 
    - `True`: If there is still time remaining before reaching the quota.
    - `False`: If the process has exceeded the quota time or is within the gap buffer.
  - **Usage**:
    ```python
    if qt.hastime():
        print('There’s still time to process.')
    ```

**`remaining_time`**:
  - **Description**: This method returns the remaining time before the quota limit is reached in a human-readable format.
  - **Returns**: A string representing the remaining time formatted as `"xh:xm:xs"` (e.g., `"0h:10m:15s"` for 10 minutes and 15 seconds remaining).
  - **Usage**:
    ```python
    remaining = qt.remaining_time()
    print(f'Remaining time: {remaining}')
    ```
---
## Installation

You can install the package from [PyPI](https://pypi.org/project/tquota) using the following command:

```bash
pip install tquota
```

Alternatively, you can clone the repository and install the package directly:

```bash
git clone https://github.com/aljbri/tquota.git
cd tquota
pip install .
```
---
## Usage

Import the `Quota` class as follows:

```python
from tquota import Quota
```

### Example Usage

- Using the **time_up** function:

```python
from tquota import Quota
import time

# Quota time is set for 1 minute and gap time is auto-adjusted
qt = Quota('1m')
# Set quota_time for 1 minute and gap_time for 30 seconds
# qt = Quota('1m', '30s')

for i in range(1000):
    time.sleep(1)
    if qt.time_up():
        print('The process has reached the limited time.')
        break
```
- Using the **hastime** function:

```python
from tquota import Quota
import time

# Quota time is set for 1 minute and gap time is auto-adjusted
# qt = Quota('1m')

# Set quota_time for 1 minute and gap_time for 30 seconds
qt = Quota('1m', '30s')

for i in range(1000):
    time.sleep(1)
    if not qt.hastime():
        print('The process has reached the limited time.')
        break
```

---
## Error Handling

The `Quota` class may raise the following exceptions:

- `ValueError`: Raised for invalid time formats or non-positive time values.
- `TypeError`: Raised if non-string values are provided for time parameters.
- `AttributeError`: Raised if internal properties are accessed incorrectly.
---
## License

This project is licensed under the MIT License. See the [LICENSE](https://github.com/aljbri/tquota/blob/master/LICENSE) file for details.

---
## Updates

### v0.0.1
- Initial implementation of the `quota` class.

### v0.0.2
- Major error fix `quota` class.

### v0.0.3
- **Auto Gap Time**: Added support for automatic calculation of `gap_time` when it is set to `'auto'`, dynamically adjusting the buffer time based on the session duration.
- **Error Handling Enhancements**: Improved validation for time formats, with clearer exceptions raised (`ValueError`, `TypeError`, `AttributeError`) for invalid inputs or improper usage.
- **Optimized Logging**: Added an optional logging feature that provides detailed output for quota time, gap time, and overall usage when enabled.
- **Performance Improvements**: Optimized the time-tracking logic for smoother integration into various cloud platforms.
- **Python Compatibility**: Compatible with Python versions 2.7 and 3.0+.

---
## Contributing

Contributions are welcome! If you have suggestions or improvements, please feel free to submit a pull request or open an issue.

---
## Contact

For inquiries or feedback, please contact the author at [mr.aljbri@gmail.com](mailto:mr.aljbri@gmail.com).
