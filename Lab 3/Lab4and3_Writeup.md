```python
from aide_design.play import*
```
### Group 6 (Ben Gassaway, Anna Lawrence, Christopher Galantino)
## Laboratory 4 Lab Report



##Introduction and Objectives
Our firm was hired in order to study why a specific species was dropping off. We have observed that there has been increased rainfall in the area so we believe the species drop off has something to do with the pH of surrounding water. Acid precipitation is caused by a chemical reaction that begins when compounds like sulfur dioxide and nitrogen oxide are released into the air. These substances rise into the atmosphere where they mix and react with water, oxygen, and other chemicals to form more acidic pollutants, such as acidic precipitation. The ecological effects of acid rain can be seen in aquatic environments, such as streams, lakes, and marshes where it can be harmful to certain ecosystems. We hypothesized that the acid rain will have a non-negligible impact on the natural pH of the lake. The team sought to quantify the scope with which the natural pH is impacted by influx of acid rain. Lakes are most vulnerable to acidification due to their downwind location, insoluble bedrock surroundings, high runoff to infiltration ratio and low watershed to lake surface area. Acid neutralizing capacity, or ANC, measures a lakes susceptibility to acidification, of the lake water. In the presence of acid rain input, lakes with a high ANC will maintain a neutral pH whereas lake with ANC lower than the acid input will not maintain a neutral pH.

##Procedures

####Lab 3


####Lab 4


##Results and Discussion



##Lab 3 Questions required of us (**complete**)
####1
*Plot measured pH of the lake versus hydraulic residence time (t/theta).*

```python
file = pd.read_csv('Lab3AcidRain_bestdata.csv')
array = np.array(file)
V = 4*(u.L)
Q = 267*(u.mL/u.min)
theta = V/Q
theta=theta.to(u.sec)
time = array[1:1255,1]*(u.sec)
restime = time/theta
pH = array[1:1255,3]
## plotting
plt.figure()
plt.plot(restime,pH)
plt.xlabel('Hydraulic Residence Time', fontsize=15)
plt.ylabel('pH', fontsize=15)
plt.savefig('./Photos/HydraulicResTimevspH.png')
plt.show()
```
####2, 3, and 4

In graphing conservative, closed, and open ANC on the same plot...

```python
K1 = 10**-6.3
K2 = 10**-10.3
Hconc = 10**(-1*pH)
ao = 1/(1+(K1/Hconc)+((K1*K2)/(Hconc**2)))
a1 = 1/((Hconc/K1)+1+(K2/Hconc))
a2 = 1/(((Hconc**2)/(K1*K2))+(Hconc/K2)+1)

Kh = 10**-1.5
P_CO2 = 10**-3.5
Kw = 10**(-14)
ANCo = .001854
ANCin = -(10**(-3))
ANCcons = ANCin*(1-np.exp(restime*(-1)))+ANCo*np.exp(restime*(-1))

cT4 = ANCo
ANCclosed = ANCo*(a1+2*a2)+(Kw/Hconc)-Hconc

cT5 = (P_CO2*Kh)/ao
ANCopen = cT5*(a1+2*a2)+(Kw/Hconc)-Hconc

x = restime
y1 = ANCcons
y2 = ANCclosed
y3 = ANCopen

plt.figure('ax',(10,8))
plt.plot(x,y1, '-b', label = 'Conservative ANC')
plt.plot(x, y2, '-r', label = 'Closed ANC')
plt.plot(x, y3, '-g', label = 'Open ANC')
plt.xlabel('Hydraulic Residence Time', fontsize=15)
plt.ylabel('ANCout', fontsize=15)
plt.legend(loc='upper left')
plt.savefig('./Photos/ANC_plot_Lab4.png')
plt.show()
```
####5
*Analyze the data from the 2nd experiment and graph the data appropriately. What did you learn from the 2nd experiment?*

```python
file = pd.read_csv('Lab3AcidRain_baddata.csv')
array = np.array(file)
V = 4*(u.L)
Q = 267*(u.mL/u.min)
theta = V/Q
theta=theta.to(u.sec)
time = array[1:1223,1]*(u.sec)
restime = time/theta
pH = array[1:1223,2]
## plotting
plt.figure()
plt.plot(restime,pH)

plt.xlabel('Hydraulic Residence Time', fontsize=15)
plt.ylabel('pH', fontsize=15)
plt.show()
```

```python
K1 = 10**-6.3
K2 = 10**-10.3
Hconc = 10**(-1*pH)
ao = 1/(1+(K1/Hconc)+((K1*K2)/(Hconc**2)))
a1 = 1/((Hconc/K1)+1+(K2/Hconc))
a2 = 1/(((Hconc**2)/(K1*K2))+(Hconc/K2)+1)

Kh = 10**-1.5
P_CO2 = 10**-3.5
Kw = 10**(-14)
ANCo = .001854
ANCin = -(10**(-3))
ANCcons=ANCin*(1-np.exp(restime*(-1)))+ANCo*np.exp(restime*(-1))

cT4 = ANCo
ANCclosed = ANCo*(a1+2*a2)+(Kw/Hconc)-Hconc

cT5 = (P_CO2*Kh)/ao
ANCopen = cT5*(a1+2*a2)+(Kw/Hconc)-Hconc

x = restime
y1 = ANCcons
y2 = ANCclosed
y3 = ANCopen

plt.figure('ax',(10,8))
plt.plot(x,y1, '-b', label = 'Conservative ANC')
plt.plot(x, y2, '-r', label = 'Closed ANC')
plt.plot(x, y3, '-g', label = 'Open ANC')
plt.xlabel('Hydraulic Residence Time', fontsize=15)
plt.ylabel('ANCout', fontsize=15)
plt.legend(loc='upper left')
plt.savefig('./Photos/ANC_plot_Lab4.png')
plt.show()
```
Because it wasn't mixed properly, the pH trend did not track as tightly as the effect should have been displayed. This was due to the uneven distribution of the carbonate in the reservoir. The ANC appeared to be buffering the solution well, but after one residence time, pH dropped dramatically.

Furthermore, the ANC is skewed and does not signify the exponential decay. This is a trend that is consistent with our first set of data.

###Lab 4 Questions required of us (**in progress**)

####1
Plot the titration curve of the t=0 sample with 0.05 N HCl (plot pH as a function of titrant volume). Label the equivalent volume of titrant. Label the 2 regions of the graph where pH changes slowly with the dominant reaction that is occurring. (Place labels with the chemical reactions on the graph in the pH regions where each reaction is occurring.) Note that in a third region of slow pH change no significant reactions are occurring (added hydrogen ions contribute directly to change in pH).

```python
file = pd.read_csv('lab4_t0_trial1and2.csv')
array = np.array(file)
V_titrant = array[6:17,0]*u.mL
pH = array[6:17,1]
Ve = 0.739305 #mL
x1 = 0.2
y1 = 6.721113
x2 = 0.8
y2 = 4.065912

def slope(x1, y1, x2, y2):
    m = 0
    b = (x2 - x1)
    d = (y2 - y1)
    if b != 0:
        m = (d)/(b)

    return m

pH_equiv = -slope(x1, y1, x2, y2)*Ve
pH_equiv
plt.figure()

plt.plot(V_titrant,pH)
plt.plot(Ve,0
, 'ko', label = 'Equivalent Volume' )

plt.axvline(x=0.0, color = 'g', label = 'Reaction 1')
plt.axvline(x=0.1, color = 'g')
plt.axvline(x=0.11, color = 'blue', label = 'Reaction 2')


plt.axvline(x=0.2, color = 'blue')
plt.axvline(x=0.21, color = 'pink', label = 'Reaction 3')
plt.axvline(x=1, color = 'pink')

plt.legend(loc='upper right')
plt.plot
plt.xlabel('Volume of titrant added (mL)')
plt.ylabel('pH')
plt.show()

```


####2

Prepare a Gran plot using the data from the titration curve of the t=0 sample. Use linear regression on the linear region or simply draw a straight line through the linear region of the curve to identify the equivalent volume. Compare your calculation of Ve with that was calculated by ProCoDA.

```python
from scipy import stats

V_titrant = V_titrant.magnitude
V_sample = 48.964500 #mL
pH_array = np.zeros(11)
V_array = np.zeros(11)


for i in range(0,11):
  pH_array[i] = float(pH[i])

for i in range(0,11):
  V_array[i] = float(V_titrant[i])

  V_titrant

Hconc_array = 10**(-1*pH_array)

def F1(V_sample,V_titrant,pH):
  return (V_sample + V_titrant)/V_sample*Hconc_array
#Create an array of the F1 values.
F1_data = F1(V_sample,V_titrant,pH_array)
#By inspection I guess that there are 4 good data points in the linear region.
N_good_points = 4
#use scipy linear regression. Note that the we can extract the last n points from an array using the notation [-N:]
slope, intercept, r_value, p_value, std_err = stats.linregress(V_titrant[-N_good_points:],F1_data[-N_good_points:])
#reattach the correct units to the slope and intercept.
intercept = intercept*u.mole/u.L
slope = slope*(u.mole/u.L)/u.mL
V_eq = -intercept/slope


```

####3

Plot the measured ANC of the lake on the same graph as was used to plot the conservative, volatile, and nonvolatile ANC models (see questions 2 to 5 of the Acid Precipitation and Remediation of an Acid Lake lab). Did the measured ANC values agree with the conservative ANC model?

##Conclusions



##Suggestions/comments
