```python
from aide_design.play import*
import Environmental_Processes_Analysis as EPA
import importlib
importlib.reload(EPA)
import scipy
from scipy import special
from scipy.optimize import curve_fit
import collections
```
# Lab 6 Report
## Chris Galantino, Ben Gassaway, Anna Lawrence
## Gas Transfer Laboratory

## Introduction and Objectives

Gas transfer is a vital unit operation in many environmental engineering processes.  It involves either the desorption or adsorption of gas. The transfer of oxygen to liquid systems is particularly important in oxidation of iron and manganese in water treatment and in the biological treatment of wastewaters. Air stripping to remove toxic volatile organics is another wastewater application. Aeration systems are designed to promote turbulence and break the water into smaller volumes of droplets, increasing the surface area for mass transfer.  Gravity or pressurized flow systems are typically used. Gas transfer means simply the process of allowing any gas to dissolve in a fluid or the opposite of that, promoting the release of a dissolved gas from a fluid.  The gas transfer rate can be modeled as the product of a driving force (the difference between the equilibrium concentration and the actual concentration) and an overall volumetric gas transfer coefficient (a function of the geometry, mixing levels of the system and the solubility of the compound). In a system where air is forced through a tube and a porous diffuser, creating very small bubbles that rise through clean water, the transfer of oxygen takes place through the bubble gas-liquid interface.  If the gas inside the bubble is air, and an oxygen deficit exists in the water, the oxygen transfers from the bubble into the water.  Most gases are only slightly soluble in water; among these are hydrogen, oxygen and nitrogen.  Solubility is influenced by many variables such as the presence of impurities and temperature. Technology has been advanced to augment gas transfer, such as aeration diffusers, packed tower air stripping, and membrane stripping. Each of these technologies creates a high interface surface area to improve gas transfer.


## Procedures


## Results and Discussion

1. The team calculates the flow rate of air from testing the air flow controller

we wanted our flow rate to be 200 uM/s.
7.64475M = airslope


The Accumulator Pressure begins with 0 Pa. As time went on, the pressure increased linearly. I stopped the data at 60 seconds because after 60 seconds, the Accumulator Pressure started to plateau when it was equal to the Source Pressure. Then I used the ideal gas law (PV = nRT) to determine our experimental flow rate (n) and the percent error. The slope of the best fit line is  Pa/s, which is the value of our P. The volume (V) of our accumulator is 1 L.

```python
data_file_path = 'C:\\Users\\en-ce-4530\\github\\crg_4530\\initial_setup200u.xls'
print(EPA.notes(data_file_path))






#I eliminate the beginning of the data file because this is a CMFR and the first data was taken before the dye reached the sensor.
firstrow = 36
time_data = EPA.ftime(data_file_path,firstrow,-1)
concentration_data = EPA.Column_of_data(data_file_path,firstrow,-1,1,'mg/L')



```


The R constant I used was 8.31446 Pa* m^3/K*mol, then multiplied it by 1000 L to get rid of m^3. The temperature (T) of our water was 22 C, which equals to 295 K. Using n = PV/RT, I calculated our experimental n to be 238.2 uM/s, which has a percent error of 19.1%.


2.



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






After eliminating the data from each data set where the dissolved oxygen concentration was less than 0.5 mg/L, the results could ensure that all of the sulfite had been completely reacted.

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

```

Below is a graphical depiction in which dissolved oxygen is plotted
```python
#3
Temperature=22*u.degC
Pressure_air = 1*u.atm

O2_sat = EPA.O2_sat(Pressure_air,Temperature)
O2_sat

part_press_ox = 0.21
T = 293
C_star = part_press_ox*np.exp((1727/T)-2.105)
print (C_star)

```

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
