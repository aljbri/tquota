

# TQuota
Processing timer module: help if the code is running on the  cloud server which has a quota limitation, such as [kaggle](https://www.kaggle.com/) and [colab](https://colab.research.google.com/) which have a limit for 9 hours of processing on each session

# quota class
The package has only one class (quota) that has two parameters
* **quota_time**: type (str) default value (6h) : represent the quota time for the session
* **gap_time**: type (str) default value (30m): represent the time gap between the quota limit and the actual closing time for the session

The time has a strict format to be passed with; it has to part *dw* while
*d*: represent the time as digits
*w*: the time and one character(w) to represent the time period
 - **s** : Seconds
 - **m** : Minutes
 - **h** : Hours
 - **d** : Days

## functions

quota class has two functions:
  * time_up : return True if the process reaches it is limit
  * hastime : return True if the process still has time to process
   
# install
you can install the package from [pypi](https://pypi.org/project/tquota).

    pip install tquota


# usage
Import the quota class as following

    from tquota import quota

Example on using the package:

 - Using **time_up** function:
```python
from tquota import quota
import time
# quota _time was set for 1 minute and the gap _time as 30 second
qt = quota('1m','30s')
for i in range(1000):
    time.sleep(1)
    if qt.time_up():
        print('The process has reached the limited time')
        break
```
 - Using **hastime** function:
```python
from tquota import quota
import time
# quota _time was set for 1 minute and the gap _time as 30 second
qt = quota('1m','30s')
for i in range(1000):
    time.sleep(1)
    if not qt.hastime():
        print('The process has reached the limited time')
        break
```