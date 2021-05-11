
# TQuota
Processing timer module : help if the code is running on the  cloud server which have a quote limitation, such as [kaggle](https://www.kaggle.com/) and [colab](https://colab.research.google.com/) which have a limit for 9 houres of processing on each seesion

# quota class
The package has only one class (quota) that has two parameters
* **quota_time**: type (str) defualt value (6h) : represent the quota time for the session
* **gap_time**: type (str) defualt value (30m) : represent the time gap between the quota limit and the actual closing time for the session

Thie time has strict format to be passed with; it has to part *dw* while 
d: represent the time as digits
*w*: the time and one character(w) to represent the time period

 - **s** : Seconds
 - **m** : Minutes
 - **h** : Hours
 - **d** : Days

## functions
quota class has two functions:
  * time_up : return True if the process reach it is limit
  * hastime : return True if the process still has time to be process
    
# install
you can install the package from [pypi](https://pypi.org/project/tquota).

    pip install tquota


# usage
to import the module

    from tquota import quota

Example of using the package:

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