[🏠HOME](README.md)

# Binning Algorithm for MS Features

---

Merge feature maps from differrent experiments into a consensus matrix.

The algorithm is based on the following workflow:

1. Put all mass in a sorted vector.
2. Calculate differences between each neighbor.
3. Divide the mass vector at the largest gap (largest difference) and form a left and a right bin.
4. Rerun step 3 for the left and/or the right bin if they don’t fulfill the following criteria:
    + All peaks in a bin are near to the mean (abs(mass-meanMass)/meanMass < tolerance).

The new peak positions (mass value) are the mean mass of a bin.


```python
import math

class Precursor:
    def __init__(self, sample, mz, intensity, rt):
        self.sample = sample
        self.mz = mz
        self.intensity = intensity
        self.rt = rt
    def __repr__(self):
        return repr(self.mz)

def is_near_to_mean(_list, tol):
    mz_list = [p.mz for p in _list]
    mean_mz = sum(mz_list) / len(mz_list)
    diff = max(max(mz_list)-mean_mz, mean_mz-min(mz_list))
    if diff > tol:
        return False
    return True

def max_gap_index(_list):
    mz_list = [p.mz for p in _list]
    gaps = []
    length = len(mz_list)
    for i in range(length-1):
        gaps.append(mz_list[i+1]-mz_list[i])
    max_gap = max(gaps)
    return gaps.index(max_gap)

def split(_list, tol):
    if is_near_to_mean(_list, tol):
        return [_list]
    else:
        break_point = max_gap_index(_list)+1
        left, right = _list[:break_point], _list[break_point:]
        return [*split(left,tol), *split(right,tol)]

def as_matrix(_list):
    import pandas as pd
    Peaks_df = pd.DataFrame()
    for c in _list:
        mz = sum([i.mz for i in c]) / len(c)
        for p in c:
            Peaks_df.loc[p.sample, mz] = p.intensity
    return Peaks_df

def bin_peaks(PeakList, tol=0.002):
    Peaks = []
    for s,L in PeakList.items():
        for i,p in L.iterrows():
            Peaks.append(Precursor(s,p['mz'], p['intensityApex'],p['rtApex']))
    Peaks_sort = sorted(Peaks, key=lambda P: P.mz)
    Peaks_split = split(Peaks_sort, tol)
    Peaks_matrix = as_matrix(Peaks_split)
    return Peaks_matrix
```
