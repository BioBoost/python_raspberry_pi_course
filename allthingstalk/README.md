# AllThingsTalk

<!-- intro what is allthingstalk -->

## Maker

<!-- intro what is allthingstalk maker -->

### Create account

### Devices

### Assets

### Pinboards



## Python

### Installing allthingstalk 

```
pip3 install allthingstalk
```
Documentation: https://allthingstalk.github.io/python-sdk/
Source code: https://github.com/allthingstalk/python-sdk

### Importing libraries

```python
from allthingstalk import *
```

or import only the used libraries

```python
from allthingstalk import Client, Device, [ASSETS]
```


### Setting authentication

```python
# Parameters used to authorize and identify your device
# Get them on maker.allthingstalk.com
DEVICE_TOKEN = '<DEVICE_TOKEN>'
DEVICE_ID = '<DEVICE_ID>'
```

```
Devices -> Settings -> Authentication
```

### Creating custom Device class

Class property names correspond with asset names in AllThingsTalk Maker

```python
class Counter(Device):
    counter = IntegerAsset()
```

#### Asset types 

```python
NumberAsset
IntegerAsset
StringAsset
BooleanAsset
GeoAsset
```

<!-- https://allthingstalk.github.io/python-sdk/api.html#assets -->

### Connecting to AllThingsTalk

```python
client = Client(DEVICE_TOKEN)
device = Counter(client=client, id=DEVICE_ID)
```

### setting asset values

Asset values will be send to AllThingsTalk automatically. Check your asset values for the device or check your Pinboard for updates.

```python
device.counter = i
```

## Example

```python
#!/usr/bin/env python3

#    _   _ _ _____ _    _              _____     _ _     ___ ___  _  __
#   /_\ | | |_   _| |_ (_)_ _  __ _ __|_   _|_ _| | |__ / __|   \| |/ /
#  / _ \| | | | | | ' \| | ' \/ _` (_-< | |/ _` | | / / \__ \ |) | ' <
# /_/ \_\_|_| |_| |_||_|_|_||_\__, /__/ |_|\__,_|_|_\_\ |___/___/|_|\_\
#                             |___/
#
# Copyright 2017 AllThingsTalk
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

#
# AllThingsTalk Counter example
#

from time import sleep

from allthingstalk import Client, Device, IntegerAsset

# Parameters used to authorize and identify your device
# Get them on maker.allthingstalk.com
DEVICE_TOKEN = '<DEVICE_TOKEN>'
DEVICE_ID = '<DEVICE_ID>'


class Counter(Device):
    counter = IntegerAsset()


client = Client(DEVICE_TOKEN)
device = Counter(client=client, id=DEVICE_ID)

for i in range(10):
    device.counter = i
    sleep(1)
```
