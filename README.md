```c
NAME : SHIVANI M
REG-NO : 212224040313
DATE : 20-03-2025
```
# EXP 2: Fitting Poisson  distribution
# Aim : 

To fit poisson distribution for the arrival of objects per minute from the feeder

# Software required :  

Python and Visual component tool

# Theory:

The Poisson distribution is the discrete probability distribution of the number of events occurring in a given time period, given the average number of times the event occurs over that time period.

![image](https://user-images.githubusercontent.com/104613195/166248326-fd042076-8b0b-40c4-8b11-1d8e8fcb74db.png)

 Conditions for Poisson Distribution:

1. An event can occur any number of times during a time period.
2. Events occur independently. I
3. The rate of occurrence is constant.
4. The probability of an event occurring is proportional to the length of the time period. 
 
# Procedure :

![image](https://user-images.githubusercontent.com/104613195/166251988-d0c53205-6080-4f7b-ae4c-398178586637.png)

# Experiment :

![image](https://user-images.githubusercontent.com/103921593/230282876-f4a5afbf-cac1-4648-a1b0-c78840638a8e.png)

# Program :

 ```python
import numpy as np
import math
import scipy.stats

L = [int(i) for i in input("Enter the observations: ").split()]
N = len(L)
M = max(L)

X = []
f = []

for i in range(M + 1):
    c = 0
    for j in range(N):
        if L[j] == i:
            c += 1
    f.append(c)
    X.append(i)

print("X:", X)
print("Observed Frequencies (f):", f)

sf = np.sum(f)

p = []
for i in range(M + 1):
    p.append(f[i] / sf)

mean = np.inner(X, p)

P = []
E = []
xi = []

print(" X  P(X=x)  Obs.Fr  Exp.Fr   xi")
print("---------------------------------")

for x in range(M + 1):
    px = (math.exp(-mean) * (mean ** x)) / math.factorial(x)
    P.append(px)
    expected = px * sf
    E.append(expected)
    chi_term = ((f[x] - expected) ** 2) / expected if expected != 0 else 0
    xi.append(chi_term)

    print("%2d  %0.3f   %4d    %5.2f   %5.2f" % (x, px, f[x], expected, chi_term))

print("---------------------------------")

cal_chi2_sq = np.sum(xi)
print("Calculated value of Chi-square is %5.2f" % cal_chi2_sq)

table_chi2 = scipy.stats.chi2.ppf(1 - 0.01, df=M)
print("Table value of Chi-square at 1%% level is %5.2f" % table_chi2)

if cal_chi2_sq < table_chi2:
    print("The given data can be fitted to a Poisson distribution at 1%% level of significance.")
else:
    print("The given data cannot be fitted to a Poisson distribution at 1%% level of significance.")

```

# Output : 


![image](https://github.com/user-attachments/assets/2e18db55-4fc0-49fa-bd47-21db354794be)

# Results

The Poisson distribution is fitted for the objects arrived from feeder per minute and the data is tested using Chi-square test. 
 
