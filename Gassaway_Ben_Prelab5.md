```python
from aide_design.play import*
```

## Laboratory 5 Pre Lab Questions
### Ben Gassaway

1) Calculate the volume of a 40 g/L red dye stock that would need to be added to 1L of water to produce 0, 5, 10, 15, 20, 25, and 30 mg/L calibration points.

Sample calculation below:
```python
V_solution = 1*u.L
C_stock = 40*u.g/u.L
C_desired = 5*u.mg/u.L
V_stock = V_solution*C_desired/C_stock
print(V_stock.to(u.mL))
```
So to produce the following:

| Desired | Volume Needed |
| ------- | ------------- |
| 0 mg/L  |     0.0 mL          |
| 5 mg/L  |     0.125 mL          |
| 10 mg/L |   0.250 mL            |
| 15 mg/L |      0.375 mL        |
|    20 mg/L     |       0.500 mL       |
|   25 mg/L      |    0.625 mL         |
|   30 mg/L      |      0.750 mL        |

2)	Calculate the change in hydraulic grade line between baffled sections of a reactor with a flow rate of 380 mL/min. The reactor baffles are perforated with 24 holes 1 mm in diameter.

```python
Q_orifice = 380 * u.mL/u.min
K = 0.6
diam=1*u.mm
num_holes = 24
A_orifice = pc.area_circle(diam)
headloss = ((Q_orifice/(K*num_holes*A_orifice))**2)/(2*pc.gravity)
headloss.to(u.cm)
print('The hydraulic grade line between baffled sections of this reactor changes by', headloss.to(u.cm))
)
```

3)	On a single graph, plot the exit age distribution (E(t*)) for a reactor with a volume of 2.25 L and a flow rate of 380 mL/min that operates as a 1-dimensional advection-dispersion reactor with Peclet numbers of 1, 10, and 100 (there will be three lines on the graph). The x-axis should be t* from 0.0 to 3.0. Comment on the shapes of the curves as a function of Pe.

```python
V_Reactor = 2.25 * u.L
Q_reactor = 380*u.mL/u.min
t = np.linspace(0.1,3,20)
Pe_1 = 1
Pe_2 = 10
Pe_3 = 100
Et_1 = ((Pe_1/(4*np.pi*t))**(.5))*np.exp(((-(1-t)**2)*Pe_1)/(4*t))
Et_2 = ((Pe_2/(4*np.pi*t))**(.5))*np.exp(((-(1-t)**2)*Pe_2)/(4*t))
Et_3 = ((Pe_3/(4*np.pi*t))**(.5))*np.exp(((-(1-t)**2)*Pe_3)/(4*t))
x = t
y1 = Et_1
y2 = Et_2
y3 = Et_3

plt.figure()

plt.plot(x,y1, '-b', label = '1 Peclet')
plt.plot(x, y2, '-r', label = '10 Peclet')
plt.plot(x, y3, '-g', label = '100 Peclet')
plt.xlabel('Time')
plt.ylabel('E(t*)')
plt.legend(loc='upper left')
plt.show()
```
**As Peclet increases, there is less time for dispersion and so the tracer concentration is not fully mixed throughout. It acts more like a PFR.**
