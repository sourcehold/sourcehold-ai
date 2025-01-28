# sourcehold-ai
AI focused sourcehold repo for Stronghold Crusader as created by Firefly Studios

Check the AIV.md!

## Installation of tools

### Prerequisites
Python 3 is required.

(x86 is required if you want to hack around with the memory of the game or the AIV editor https://www.python.org/ftp/python/3.12.6/python-3.12.6.exe )

### Sourcehold
If you want to use sourcehold from the command line
```cmd=
python -m pip install git+https://github.com/sourcehold/sourcehold-maps
```

Or this if you want to use the examples
```cmd=
git clone https://github.com/sourcehold/sourcehold-maps
cd sourcehold-maps
python -m pip install pymem Pillow dclimplode numpy matplotlib
```


### Example 1
Open up `examples/aiv_example_one.py` from the sourcehold-maps repo for guidance

#### Viewing an AIV file
```python=
from sourcehold.aivs import AIV

aiv = AIV().from_file("C:\\Program Files (x86)\\Steam\\steamapps\\common\\Stronghold Crusader Extreme\\aiv\\saladin1.aiv")

# View the constructions
aiv.directory[2007].show()
```

### Example 2
Hacking around the editor
```python=
from sourcehold.debugtools.memory.access import Village
process = Village()

process.show('2007')

# Read in data
rawdata = process.read_section('2007')
constructions = np.frombuffer(rawdata, dtype='uint16').copy().reshape((100,100))

# Make modifications

# Write the data to process memory
process.write_section('2007', constructions.tobytes())
```

### Example 3
```py=
import struct

import numpy as np

from sourcehold.aivs import AIV

aiv = AIV().from_file("C:\\Program Files (x86)\\Steam\\steamapps\\common\\Stronghold Crusader Extreme\\aiv\\saladin1.aiv")

rawdata = aiv.directory[2007].get_data()
constructions = np.frombuffer(rawdata, dtype='uint16').copy().reshape((100,100))

# Insert your modifications here

# When done, do this:
aiv.directory[2007].set_data(constructions.to_bytes())
aiv.to_file("your_aiv.aiv")
```
