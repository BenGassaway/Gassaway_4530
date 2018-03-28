```python
from aide_design.play import *
import numpy as np
import pandas as pd
import os
import collections
import matplotlib.pyplot as plt
import matplotlib
from scipy import stats
import Environmental_Processes_Analysis as EPA
import importlib
importlib.reload(EPA)

```
# Lab 6 Report
## Helena Harris, Andrew Kang, Simon Fines
## Gas Transfer Laboratory

## Introduction and Objective



## Procedure


## Results and Discussion

1. We calculated the air flow rate from the test calibration. Below is Figure 1, with the calculations as well as the graph of Accumulator Pressure vs. Time

![AirrateFlow](https://github.com/ak694/githubcee4530-1/blob/master/Airflowrate.png?raw=true).

**Figure 1**:
The Accumulator Pressure starts off with 0 Pa. As time went on, the pressure increased linearly. I stopped the data at 60 seconds because after 60 seconds, the Accumulator Pressure started to plateau when it was equal to the Source Pressure. Then I used the ideal gas law (PV = nRT) to determine our experimental flow rate (n) and the percent error. The slope of the best fit line is 584.26 Pa/s, which is the value of our P. The volume (V) of our accumulator is 1 L. The R constant I used was 8.31446 Pa* m^3/K*mol, then multiplied it by 1000 L to get rid of m^3. The temperature (T) of our water was 22 C, which equals to 295 K. Using n = PV/RT, I calculated our experimental n to be 238.2 uM/s, which has a percent error of 19.1%.

### Conclusions



### Suggestions/Comments



### Code

1. Calculate the air flow rate from testing the air flow controller and compare with the target value.
2. Eliminate the data from each data set when the dissolved oxygen concentration was less than 0.5 mg/L. This will ensure that all of the sulfite has reacted.

3. Plot a representative data set showing dissolved oxygen vs. time.
4. Calculate   based on the average water temperature, barometric pressure, and the following equation.  $C^{\star}=P_{O_{2}}e^{\frac{1727}{T}-2.105}$ where T is in Kelvin, $P_{O_{2}}$  is the partial pressure of oxygen in atmospheres, and $C^{\star}$ is in mg/L. This equation is valid for 278 K<T<318 K.
5. Estimate $\hat{k}_{v,l}$ using linear regression and equation 1.5 for each data set.
6. Create a graph with a representative plot showing the linearized data,  $ln\frac{C^{\star}-C}{C^{\star}-C_{0}}$ vs. time, and the best-fit line.
7. Plot the reaeration model on the same graph as the dissolved oxygen vs. time data.  This is done by solving equation for C.
8. Plot $\hat{k}_{v,l}$ as a function of airflow rate (μmole/s).
9. Look at each dataset and if necessary (to make more linear plots) eliminate more data from the beginning (or end) of the dataset. You will be able to see when the oxygen level is affected by residual sulfite at the beginning of the experiments.
10. Plot OTE as a function of airflow rate (μmole/s) with the oxygen deficit $(C^{\star}-C)$ set at 6 mg/L.
11. Plot the molar rate of oxygen dissolution into the aqueous phase (μmole/s) as a function of airflow rate (μmole/s).
12. Comment on results and compare with your expectations and with theory.
13. Verify that your report and graphs meet the requirements.


```python


#2
DO_column = 2
filepaths, airflows, DO_data, time_data = EPA.aeration_data(2)

airflows
filepaths
for i in range(airflows.size):
  plt.plot(time_data[i], DO_data[i],'o')

plt.xlabel(r'$time (s)$')
plt.ylabel(r'Oxygen concentration $\left ( \frac{mg}{L} \right )$')
plt.legend(airflows.magnitude)

#plt.savefig('images/aeration.png')
plt.show()

#3
Temperature=22*u.degC
Pressure_air = 1*u.atm

O2_sat = EPA.O2_sat(Pressure_air,Temperature)
O2_sat

part_press_ox = 0.21
T = 293
C_star = part_press_ox*np.exp((1727/T)-2.105)
print (C_star)

#5
co0 = [0.509,2.01,0.51,2.52,0.528,0.539]
DATA = np.array(DO_data)
c0=np.array(DATA[0])
c1=np.array(DATA[1])
c2=np.array(DATA[2])
c3=np.array(DATA[3])
c4=np.array(DATA[4])
c5=np.array(DATA[5])
c = [c0[0:219],c1[69:307],c2,c3[109:185],c4[0:54],c5[0:47]]
TIME = np.array(time_data)
t0=np.array(TIME[0])
t1=np.array(TIME[1])
t2=np.array(TIME[2])
t3=np.array(TIME[3])
t4=np.array(TIME[4])
t5=np.array(TIME[5])
t = np.array([t0[0:219],t1[69:307]-t1[69],t2,t3[109:185]-t1[109],t4[0:54],t5[0:47]])
y = [0,0,0,0,0,0]
for i in range(6):
  y[i] = np.log((O2_sat.magnitude-c[i])/(O2_sat.magnitude-co0[i]))

y=np.array(y)
lindata = [0,0,0,0,0]
k=[0,0,0,0,0,0]
for j in range(6):
  lindata = stats.linregress(-t[j],y[j])
  k[j] = lindata[0]
k=np.array(k)
print (k)
#6
for p in range(6):
  plt.plot(t[p],y[p])

plt.xlabel(r'$time (s)$')
plt.ylabel(r'Linearized Oxygen conc. $\left ( \frac{mg}{L} \right )$')
plt.legend(airflows.magnitude)
for p in range(6):
  plt.plot(t[p],-t[p]*k[p],"--", color='#808080', label="Best Fit")
plt.show()

#7
c_model=[]
for i in range(6):
  val = np.zeros(len(t[i]))
  for j in range(len(t[i])):
    val[j] = (O2_sat.magnitude-((O2_sat.magnitude-co0[i])*(10**(-k[i]*t[i][j]))))
  c_model.insert(i,val)
print (c_model)
```
