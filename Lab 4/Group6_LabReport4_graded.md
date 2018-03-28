```python
from aide_design.play import*
```
### Group 6 (Ben Gassaway, Anna Lawrence, Christopher Galantino)
## Lab Report 4

<div class="alert alert-block alert-success">
good job 94/100
</div>


##Introduction and Objectives
Our firm was hired in order to study why a specific fish species' population was dropping off. We have observed that there has been increased rainfall in the area so we believe the decrease in the fish's numbers has something to do with the pH of surrounding water. Acid precipitation is caused by a chemical reaction that begins when compounds like sulfur dioxide and nitrogen oxide are released into the air. These substances rise into the atmosphere where they mix and react with water, oxygen, and other chemicals to form more acidic pollutants, such as acidic precipitation. The natural buffer against the influx of acid is the carbonate system, which can be summarized by a summation of their concentrations:

$C_T = [H_2CO_3] + [HCO_3^-] + [CO_3^{-2}]$

In natural systems, it is difficult to have a quantified representation of the natural buffer capability of a large body of water. The first step in understanding these systems is to calculate the preexisting acid-neutralizing capacity of a lake, which can be done using the formal definition of ANC (total acid neutralizing capacity):

$ANC = [HCO_3^{-}] + 2[CO_3^{-2}] + [OH^{-}] - [H^{+}]$

 The ecological effects of acid rain can be seen in aquatic environments, such as streams, lakes, and marshes where it can be harmful to certain ecosystems. We hypothesized that the acid rain will have a non-negligible impact on the natural pH of the lake. The team sought to quantify the scope with which the natural pH is impacted by influx of acid rain. Lakes are most vulnerable to acidification due to their downwind location, insoluble bedrock surroundings, high runoff to infiltration ratio and low watershed to lake surface area. Acid neutralizing capacity, or ANC, measures a lakes susceptibility to acidification. In the presence of acid rain input, lakes with a high ANC will maintain a neutral pH whereas lake with ANC lower than the acid input will not maintain a neutral pH.

 The primary objective of these experiments were to determine the most accurate representation of the interactions of an acidic species into a natural body of water. This was done by simulating a number of conditions. The ANC was measured in a conservative system, a closed system, and an open system. The conservative system can be summarized by the following relationship:

$ANC_{out} = ANC_{in} * (1-e^{-t/\theta}) + ANC_0 * e^{-t/\theta}$

The next system to be assessed during the experiment was a closed system, or a nonvolatile system.

 $ANC = C_T(\alpha_1 + 2\alpha_2) + K_w/[H^{+}] - [H^{+}]$

The final system to be analyzed in terms of its acid neutralizing capacity was in the context of an open system, or a volatile system.

 $ANC = (P_{CO_2}K_H)/a_0)(\alpha_1 + \alpha_2) + K_W/[H^+] - [H^+]$

In order to assess the validity of the experimental data, we applied a Gran plot in order to determine whether or not the ANC calculated in an experimental setting would hold true with our hypotheses for a real-life body of water. The tightness of fit produced in the Gran plot was calculated through linear regression. The first Gran function can be defined by F1 in the following relationship:

$F_1 = \frac{V_s + V_t}{V_s}[H^{+}]$

We were able to relate an equivalent volume to the calulated ANC value in order to provide a measure of validity in our estimations. The following equation summarizes the methodology to do so:

$ANC = V_{eq}\times{titrant_{normality}}/V_{sample}$

<div class="alert alert-block alert-success">
Good job 10/10
</div>

##Procedures

The experimental apparatus used consisted of an acid rain storage reservoir, peristaltic pump, and lake. The pH of the lake was monitored using a pH probe connected to a signal-conditioning box that was connected to the ProCoDA II hardware and software. We set up our experiment by first, making sure all of the parameters inputted into ProCoDA II software were correct and second, setting up the pH probe by rinsing it with DI water and calibrating it. Three buffer solutions with a known pH were used to calibrate the pH probe, red=4.0, yellow=7.0, and blue=10.0. After rinsing the pH probe, it was placed first into the red buffer and stirred gently while waiting for pH on the ProCoDA II to stabilize. Once stabilized, the probe was rinsed DI water and the process was repeated for the yellow and blue buffer solutions. Once calibration was done, the experiment was set up. This was set up specifically so that the “acid rain” is pumped directly into the lake. The pump was preset to give desired flow rate of 267 mL/min based on the size of pump tubing selected. The tubing sized used was #17, so RPM was set to (267 mL/min) / (2.8 mL/rev) = 95.4 RPM. Outflow was also set to approximately 4 L. Once all of the set up was done, the lake was filled with reverse osmosis water and placed on top of a magnetic stirrer with a stir bar.  1 mL of bromocresol green indicator solution was added to the lake. 623 mg of NaHCO3 was then added to the lake. After the lake was well stirred, a 100 mL sample was taken from the lake labeled with the time of the sample (which = 0 min). The pH of the effluent was continuously measured. This was repeated 4 times at 5, 10, 15 and 20 minutes and labeled respectively. After the 20‑minute sample, the flow rate was measured by collecting effluent in a beaker for 30 seconds and then measuring the volume collected by using the mass of the water in the lake. This entire experiment was repeated, however, the lake was not mixed.

Using our samples collected from the Acid Lake Remediation lab the prior week along with ProCoDA II software, we determined ANC for all samples (t=0, t=5, t=10, t=15, t=20). To do this, we first added 50mL from the t=0 sample to a 100mL beaker and placed the beaker on a magnetic stirrer. Once the pH probe was placed into the solution, we used the ProCoDA II software to record the initial pH before adding any titrant. Then, using a digital pipette, we added .100 mL increments of 0.05 N of HCl. The data collected by the program was used to plot a titration curve. This titration curve was used to verify that the Gran plot technique accurately measured ANC of the sample.

<div class="alert alert-block alert-danger">
Make sure to only include important things from the lab manual and so they would make sense to a reader, like what is the significance of 623 mg. 8/10
</div>

##Results and Discussion

The first step in analyzing the lake's response to incoming acid rain was simulating the lake in a laboratory setting. As seen in the plot below, it is clear that the carbonates in the lake provided resistance against incoming acid. pH decreased first logarithmically and then dramatically switched to exponential decay.

```python
file = pd.read_csv('/Users/jillianwhiting/github/CEE4530TA/Grading/Lab 4/Group6_LabReport4/Lab3AcidRain_bestdata.csv')
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
#plt.savefig('./Photos/HydraulicResTimevspH.png')
plt.show()
```

<div class="alert alert-block alert-success">
Good job 5/5
</div>

The next steps in analyzing the lake's response to acid rain was determining which ANC model most accurately represented the reality of the situation the lake had experienced. ANC can be expressed in the three ways explained in the Introduction of the report: conservative, closed, and open.

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
#plt.savefig('./Photos/ANC_plot_Lab4.png')
plt.show()
```


From the graph above, it is clear that an open ANC model fails to model the initial resistance of the lakes, while a conservative and closed ANC model more accurately depict the lake's capacity to counter a pH shift. Clearly, the lake does not represent a volatile system for gaseous exchange with the atmosphere when compared with the general pH graph, further confirming the hypothesis that ANC influenced more so by the incoming acid.

Additional investigation of the lake led the team to determine the effects of sufficient mixing on the lake's ability to resist pH fluctuations. Perhaps the drop in fish population is due to stagnation rather than pH.

<div class="alert alert-block alert-danger">
Ct should be dependent on pH not a constant 13/15
</div>

```python
file = pd.read_csv('/Users/jillianwhiting/github/CEE4530TA/Grading/Lab 4/Group6_LabReport4/Lab3AcidRain_baddata.csv')
array = np.array(file)
V = 4*(u.L)
Q = 267*(u.mL/u.min)
theta = V/Q
theta=theta.to(u.sec)
time = array[1:1223,1]*(u.sec)
restime = time/theta
pH = array[1:1223,2]
plt.figure()
plt.plot(restime,pH)
plt.xlabel('Hydraulic Residence Time', fontsize=15)
plt.ylabel('pH', fontsize=15)
plt.show()
```
From this graph, stagnation does not seem to have a large affect on when pH could no longer be resisted. The pH, compared to the well-mixed lake simulation earlier, reaches a little under 6 as compared to a pH of around 3. However, it seems to show that pH, superficially, is not experiencing fluctuation at first but then undergoes a dramatic shift of 3 pH units. This may play a role in the fish population where the species is not given ample time to adjust to the hasty alteration of the lake's acidity.



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
#plt.savefig('./Photos/Group6_badANCplot.png')
plt.show()
```
Because it wasn't mixed properly, the pH trend did not track as tightly as the effect should have been displayed. This was due to the uneven distribution of the carbonate in the reservoir.

<div class="alert alert-block alert-success">
Good job 5/5
</div>


From here, the team wished to confirm the ANC trend of the lake. The first steps were creating a titration curve of the t=0 sample with the gradually added 0.05 HCL. As represented in the ANC and pH plots of the well-mixed data, one can observe the series of reactions that take place between the solution and the added acid.

```python
file = pd.read_csv('/Users/jillianwhiting/github/CEE4530TA/Grading/Lab 4/Group6_LabReport4/lab4_t0_trial1and2.csv')
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
plt.axvline(x=0.0, color = 'g', label = 'Reaction 1')
plt.axvline(x=0.1, color = 'g')
plt.axvline(x=0.11, color = 'blue', label = 'Reaction 2')
plt.axvline(x=0.2, color = 'blue')
plt.axvline(x=0.21, color = 'pink', label = 'Reaction 3')
plt.axvline(x=1, color = 'pink')
plt.axvline(x = Ve, color = 'yellow' , label = 'Equivalent Volume' )
plt.legend(loc='upper right')
plt.legend(bbox_to_anchor=(0.95, 1), borderaxespad=1.)
plt.plot
plt.xlabel('Volume of titrant added (mL)')
plt.ylabel('pH')
plt.savefig('./Photos/Group6_titrationcurve.png')
plt.show()
```
The pH does not drop immediately in the increments of acid in Reaction 1 and Reaction 2. However, the third region represents the direct relationship between the added pH since no more significant reactions are occurring. This is due to the added hydrogen ions contributing directly to pH change.

<div class="alert alert-block alert-success">
Good job 10/10
</div>


From the titration curve data, a Gran plot may be executed. This was done through linear regression analysis on the linear region of the graph (Reaction 3).

```python
from scipy import stats

V_titrant = array[6:17,0]
V_sample = 48.964500
pH_array = np.zeros(11)
V_array = np.zeros(11)

for i in range(0,11):
  pH_array[i] = float(pH[i])

pH_array
for i in range(0,11):
  V_array[i] = float(V_titrant[i])

V_array

Hconc_array = 10**(-pH_array)
Hconc_array
def F1(V_sample,V_titrant,pH):
  return (V_sample + V_titrant)/V_sample*Hconc_array

F1_data = F1(V_sample,V_array,pH_array)
N_good_points = 4
slope, intercept, r_value, p_value, std_err = stats.linregress(V_array[-N_good_points:],F1_data[-N_good_points:])
intercept = intercept*u.mole/u.L
slope = slope*(u.mole/u.L)/u.mL
V_eq = -intercept/slope
V_titrant = V_array*u.mL
x=[V_eq.magnitude,V_titrant[-1].magnitude]
y=[0,(V_titrant[-1]*slope+intercept).magnitude]
plt.plot(V_titrant, F1_data,'o', color = 'purple')
plt.plot(x, y,'r')
plt.xlabel('Titrant Volume (mL)')
plt.ylabel('Gran function (mole/L)')
plt.legend(['data'])
#plt.savefig('./Photos/Group6_granplot.png')
plt.show()

```
<div class="alert alert-block alert-success">
good job 5/5
</div>

The equivalent volume calculated by ProCoDA was 0.739305 mL. This linear regression analysis produced a value of .71067 mL. These numbers are exceptionally similar as expected.

**Note:** The reason the equivalent volumes are not directly equal is because we had not taken a sample at t=0 during the first week of the lab, and instead needed to take another group's t=0 sample to be in accordance with the laboratory procedures. The results are still very close though!

With this equivalent volume, the ANC can then be plotted and compared to the original well-mixed reactor data.

```python
file = pd.read_csv('/Users/jillianwhiting/github/CEE4530TA/Grading/Lab 4/Group6_LabReport4/Lab3AcidRain_bestdata.csv')
array = np.array(file)
V = 4*(u.L)
Q = 267*(u.mL/u.min)
theta = V/Q
theta=theta.to(u.sec)
time = array[1:1255,1]*(u.sec)
restime = time/theta
pH = array[1:1255,3]
K1 = 10**-6.3
K2 = 10**-10.3
Hconc = 10**(-1*pH)
ao = 1/(1+(K1/Hconc)+((K1*K2)/(Hconc**2)))
a1 = 1/((Hconc/K1)+1+(K2/Hconc))
a2 = 1/(((Hconc**2)/(K1*K2))+(Hconc/K2)+1)
Kh = 10**-1.5
P_CO2 = 10**-3.5
Kw = 10**(-14)
V_eq = 0.739305*u.mL
titrant_normality = 0.1*u.mole/u.L
V_sample = 48.964500*u.mL
ANC = (V_eq*titrant_normality/V_sample).magnitude
ANC
ANCo = .001854
ANCin = -(10**(-3))
ANCcons = ANCin*(1-np.exp(restime*(-1)))+ANCo*np.exp(restime*(-1))
cT4 = ANCo
ANCclosed = ANCo*(a1+2*a2)+(Kw/Hconc)-Hconc
cT5 = (P_CO2*Kh)/ao
ANCopen = cT5*(a1+2*a2)+(Kw/Hconc)-Hconc
ANCmeasured = ANCin*(1-np.exp(restime*(-1)))+ANC*np.exp(restime*(-1))

x = restime
y1 = ANCcons
y2 = ANCclosed
y3 = ANCopen
y4 = ANCmeasured

plt.figure('ax',(10,8))
plt.plot(x,y1, '-b', label = 'Conservative ANC')
plt.plot(x, y2, '-r', label = 'Closed ANC')
plt.plot(x, y3, '-g', label = 'Open ANC')
plt.plot(x, y4, 'k', label = 'Measured ANC')
plt.xlabel('Hydraulic Residence Time', fontsize=15)
plt.ylabel('ANCout (mol/L)', fontsize=15)
plt.legend(loc='upper left')
#plt.savefig('./Photos/ANC_compared.png')
plt.show()
```
The measured ANC value and its respective decay is comparable to that of the conservative ANC graph as expected, indicating that the initial calculations are a good approximation of the neutralizing capacity of a species prior to running a reaction.

<div class="alert alert-block alert-success">
good job 10/10
</div>

Style points
<div class="alert alert-block alert-info">
If there are errors in your data please give explanations of why they are occuring every time. Why do you think the conservative ANC is slightly higher than the measured ANC? 13/15
</div>


##Conclusions
The team simulated the lake system as a completely mixed flow reactor to observe the effects of acid input on chemical composition and capability to remain a hospitable environment. From the ANC analysis, where a conservative model most accurately depicted reality as confirmed by the gran plot analysis, the team's hypothesis was confirmed. Acid rain, although not producing immediate change to a body of water's chemical makeup, has drastic effects on a lake's ability to sustain life. These findings, in addition to potential stagnation of water within the lake, serve as potential explanations for the drop off in the fish species' population.

<div class="alert alert-block alert-success">
good job 15/15
</div>
