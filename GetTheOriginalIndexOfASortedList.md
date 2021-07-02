[🏠HOME](README.md)

# Get The Original Index of a Sorted List

---

```python
# Python Implementation
def sorted_index(_list):
    return sorted(range(len(_list)), key=lambda k: _list[k])
```
