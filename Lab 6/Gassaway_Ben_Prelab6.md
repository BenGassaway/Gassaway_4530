#Prelab 6: Gas Transfer
### Ben Gassaway

######1) Calculate the mass of sodium sulfite needed to reduce all the dissolved oxygen in 4 L of pure water in equilibrium with the atmosphere and at 30°C.

```python
DO_30 = 7.558 * u.mg/u.L #from dissolved oxygen tables in fundamentals of environmental measurements
NaSulfite_mass_perO2 = 7.875 * u.mg/u.mg
DO_mass = (4 * u.L) * DO_30
Sulfite_Needed = DO_mass * NaSulfite_mass_perO2
print('The mass of sodium sulfite needed to reduce all of the dissolved oxygen is', Sulfite_Needed, '.')
```

######2)	Describe your expectations for dissolved oxygen concentration as a function of time during a reaeration experiment.  Assume you have added enough sodium sulfite to consume all of the oxygen at the start of the experiment. What would the shape of the curve look like?

During the period of reaeration, I expect the dissolved oxygen concentration to rise until reaching a steady state concentration. The shape of the curve will be contingent upon the value of equation 1.5, but it should resemble a logarithmic curve:

Equation 1.5: $\ln(\frac{C^{\star}-C}{C^{\star}-C_{0}})=-k(t-t_{0})$

As the concentration increases, the curve will increasingly taper and will present asymptotic behavior as the system approaches steady state.

######3)	Why is $\small\widehat{k}_{v,l}$ not zero when the gas flow rate is zero? How can oxygen transfer into the reactor even when no air is pumped into the diffuser?

$\small\widehat{k}_{v,l}$ is not zero when the gas flow rate is zero because $\small\widehat{k}_{v,l}$ depends on surface area, aqueous volume, $\small O_2$ Diffusion Coefficient, and the laminar boundary layer thickness $\delta$ through which the gas must diffuse before the much faster turbulent mixing process can disperse the dissolved gas throughout the reactor.

######4)	Describe your expectations for $\small\widehat{k}_{v,l}$  as a function of gas flow rate. Do you expect a straight line? Why?

Equation 1.8: ($\small MW_{O_{2}}Q_{air}P_{air}f_{O_{2}}(OTE)=\widehat{k}_{v,l}(C^{\star}-C)\star{VRT}$) represents a linear relationship between $\small\widehat{k}_{v,l}$ and Q so the curve for $\small\widehat{k}_{v,l}$ with respect to gas flow will present a straight line for the curve.


######5)	A dissolved oxygen probe was placed in a small vial in such a way that the vial was sealed. The water in the vial was sterile. Over a period of several hours the dissolved oxygen concentration gradually decreased to zero. Why? (You need to know how dissolved oxygen probes work to answer this!)

The DO probe operates by using a semipermeable membrane which allows oxygen to pass through the membrane due to a fixed voltage, but prevents water and other materials from passing through. The dissolved oxygen passing through the membrane is reduced to $\small H_{2}O$, therefore the overall oxygen concentrations will decrease as the oxygen levels are reduced over time.
