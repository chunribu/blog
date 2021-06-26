[🏠HOME](README.md)

# Write A File Search Function in Python

---

```python
import os
import re

def search(pattern, path='.', file_only=False, dir_only=False): 
    '''
    Search for files and/or directions under a certain path recursively.
    ''' 
    res = [] 
    for root, dirs, files in os.walk(path): 
        if not file_only: 
            for d in dirs: 
                if re.search(pattern, d): 
                    res.append(os.path.join(root, d)) 
        if not dir_only: 
            for f in files: 
                if re.search(pattern, f): 
                    res.append(os.path.join(root, f)) 
    return res
```
