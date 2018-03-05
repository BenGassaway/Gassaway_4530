```python
from aide_design.play import*
```
### Group 6 (Ben Gassaway, Anna Lawrence, Christopher Galantino)
## Laboratory 3 Lab Report


####1
*Plot measured pH of the lake versus hydraulic residence time (t/theta).*

```python
file = pd.read_csv(r'''C:\Users\JYK\github\test\CEE4530TA\Grading\Lab 3\Group6_Lab3AcidRain_bestdata.csv''')
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
plt.savefig(r'''C:\Users\JYK\github\test\CEE4530TA\Grading\Lab 3\HydraulicResTimevspH.png''')
plt.show()
```
<div class="alert alert-block alert-success">
Good job!
</div>
<div class="alert alert-block alert-danger">
please add a legend box to your graph
</div>

####2
*Calculate ao, a1, and a2 based on the pH measured at each time point. Recall that each a represents the fraction of a particular carbonate system species at that pH. As such, the sum of the alphas at each measured pH should be 1.0!*

```python
K1 = 10**-6.3
K2 = 10**-10.3
Hconc = 10**(-1*pH)
ao = 1/(1+(K1/Hconc)+((K1*K2)/(Hconc**2)))
a1 = 1/((Hconc/K1)+1+(K2/Hconc))
a2 = 1/(((Hconc**2)/(K1*K2))+(Hconc/K2)+1)
```
<div class="alert alert-block alert-success">
Good job!
</div>

####3, 4, and 5
In graphing conservative, closed, and open ANC on the same plot...

```python
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
plt.savefig(r'''C:\Users\JYK\github\test\CEE4530TA\Grading\Lab 3\ANC_plot_Lab4.png''')
plt.show()
```
<div class="alert alert-block alert-success">
Good job!
</div>

####6, 7, and 8
Deriving and plotting an equation for cT as a function of time (conservative), cT as a function of ANC and pH (closed), and equilibrium concentration of cT as a function of pH (equilibrium). All points plotted against hydraulic residence time.

```python
cTCons=ANCin*(1-np.exp(restime*(-1)))+ANCo*np.exp(restime*(-1))

cTclosed = (ANCcons+Hconc-(Kw/Hconc))/(a1+2*a2)

cTequil = (P_CO2*Kh)/ao

y1 = cTCons
y2 = cTclosed
y3 = cTequil

plt.figure('ax',(10,8))
plt.plot(x,y1, '-b', label = 'Conservative cT')
plt.plot(x,y2, '-r', label = 'Closed cT')
plt.plot(x,y3, '-g', label = 'Equilibrium cT')

plt.xlabel('Hydraulic Residence Time', fontsize=15)
plt.ylabel('cT', fontsize=15)
plt.legend(loc='upper left')
plt.show()
```
<div class="alert alert-block alert-success">
Good job!
</div>

####9
*Compare the two plots and determine whether the lake is best modeled as a volatile or non volatile system. What changes could be made to the lake to bring the lake into equilibrium with atmospheric CO2?*

The lake is best modeled as a non volatile because it more closely reflects the changes in pH, with a moderate resistance to the changes across residence times. The volatile system does not represent the changes in pH due to the steady resistance and then dramatic decrease in ANC after one residence time.

<div class="alert alert-block alert-success">
Good job!
</div>

####10

*Analyze the data from the 2nd experiment and graph the data appropriately. What did you learn from the 2nd experiment?*

```python
file = pd.read_csv(r'''C:\Users\JYK\github\test\CEE4530TA\Grading\Lab 3\Group6_Lab3AcidRain_baddata.csv''')
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
Because it wasn't mixed properly, the pH trend did not track as tightly as the effect should have been displayed. This was due to the uneven distribution of the carbonate in the reservoir. The ANC appeared to be buffering the solution well, but after one residence time, pH dropped dramatically.

<div class="alert alert-block alert-success">
Good job!
</div>
###Questions

#####1.	*What do you think would happen if enough NaHCO3 were added to the lake to maintain an ANC greater than 50 µeq/L for 3 residence times with the stirrer turned off? How much NaHCO3 would need to be added?*

Since the lake is unstirred, the NaHCO3 and the respective ANC could perform either for the best or for the worst. This is due to the variability in where the carbonate resides in the solution. In a well stirred environment, a great amount of NaHCO3 would be required to achieve the ANC necessary to combat an influx of pH 3 for three residence times. However, in an unstirred environment, the amount required may be only a little more or a lot more and may not have the expected affect depending on where incoming pH lays, where the compound is added, and where the exit is.

<div class="alert alert-block alert-success">
Good job!
</div>

#####2.	*What are some of the complicating factors you might find in attempting to remediate a lake using CaCO3?*

One of the primary complicating factors in attempting to remediate a lake using CaCO3 is the degree with which the lake will be mixed. It is difficult to quantify the efficacy of CaCO3 in remediation because the uneven mixing within the lake so the CaCO3 will have a more random effect in remediating the acid. The system has less predictability than what can be assumed in a benchtop experiment.

##Conclusions
The ANC of any reservoir serves as a relatively effective buffer to resist differing influent pH. However, as the ANC is consumed and completely reacted with the influent pH, its efficacy will see a sharp decline as the pH will uninhibitedly impact the pH of the reservoir absent of the ANC.

<div class="alert alert-block alert-success">
Good job!
</div>

##Suggestions/comments
