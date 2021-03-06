# Satellite_control
![Model](https://github.com/ArthurShih/Satellite_control/blob/master/figure/Model.png)
###### Satellite of mass with thrust in the radial direction u1 and in the tangential direction u2
## Model system:
###### m( d^2(r)/dt^2 - r * d(theta)/dt ) = u1 - km/r^2 + w1
###### m( 2 * dr/dt * d(theta)/dt + r * d^2(theta)/dt^2 ) = u2 + w2
###### .
###### d^2(r)/dt^2 = r * d(theta)/dt - k/r + u1/m + w1/m
###### d^2(theta)/dt^2 = ( -2 * dr/dt * d(theta)/dt )/r + u2/(m*r) + w2/(m*r)
###### .
###### To keep Satellite in circular orbit, let rhat = r - rbar, where rbar is stable radius of satellite
###### And then linearize the system by rhat = 0, drhat/dt = 0, d(theta)/dt = omega
###### A = [[0,0,1,0],[0,0,0,1],[3*omega**2,0,0,2*rbar*omega],[0,0,-2*omega/rbar,0]]
###### Bu = [[0,0],[0,0],[1/m,0],[0,1/(m*rbar)]]
###### Bw = [[0,0],[0,0],[1/m,0],[0,1/(m*rbar)]]
###### Q = I, R = I
###### Initial state = [1,0,0,1]
###### Here, Imma control the satellite in circular orbit by three choices of input
###### .
## LQR controller
#### 1. by u2 only
###### Bu2 = [[0],[0],[0],[1/(m*rabr)]]
##### State plot
![u2 control](https://github.com/ArthurShih/Satellite_control/blob/master/figure/LQR/LQR_u2.png)
##### Properties
![u2 property](https://github.com/ArthurShih/Satellite_control/blob/master/figure/LQR/LQR_u2_property.png)
###### .
#### 2. by u2 only
###### Bu1 = [[0],[0],[1/m],[0]]
###### Notice (A,Bu1) is not controllable!!
##### State plot
![u1 control](https://github.com/ArthurShih/Satellite_control/blob/master/figure/LQR/LQR_u1.png)
##### Properties
![u1 property](https://github.com/ArthurShih/Satellite_control/blob/master/figure/LQR/LQR_u1_property.png)
###### .
#### 3. by u1 and u2
###### Notice cost of controlling by u1 and u2 is much less than controlling by u2 only
##### State plot
![u1u2 control](https://github.com/ArthurShih/Satellite_control/blob/master/figure/LQR/LQR_u1_u2.png)
##### Properties
![u1u2 property](https://github.com/ArthurShih/Satellite_control/blob/master/figure/LQR/LQR_u1_u2_property.png)
###### . 
## Optimal State Estimation
###### For estimating the state of a satellite in circular orbit, we set u1 = u2 = 0.
###### Noise measurement of theta
###### y = Cy*x + v
###### Cy = [0,1,0,0]
###### Dwv = 1
###### Initial state = [1,0,0,1], Initial measurement = [0,0,0,0]
###### .
##### State plot
![State plot](https://github.com/ArthurShih/Satellite_control/blob/master/figure/Estimator/Estimator_state.png)
###### .
##### Error plot
![Error plot](https://github.com/ArthurShih/Satellite_control/blob/master/figure/Estimator/Error.png)
###### .
##### Properties
![property](https://github.com/ArthurShih/Satellite_control/blob/master/figure/Estimator/Estimator_property.png)
###### .
## LQG controller
###### Combinning LQR and Optimal state estimator, we have our system:
###### xdot = A*x + Bu*u + Bw*w
###### y = Cy*x + v
###### z = Cz*x + u
###### Cz = [[1,0,0,0],[0,1,0,0],[0,0,1,0],[0,0,0,1],[0,0,0,0],[0,0,0,0]]
###### Dzu = [[0,0],[0,0],[0,0],[0,0],[1,0],[0,1]]
###### Initial state = [1,0,0,1]
###### Initial measurement = [0,0,0,0]
###### .
##### Error plot
![LQG plot](https://github.com/ArthurShih/Satellite_control/blob/master/figure/LQG/LQG_error.png)
###### .
##### K and F
![K&F](https://github.com/ArthurShih/Satellite_control/blob/master/figure/LQG/LQG_K_F.png)
###### .
#### Cost
###### J1 = trace(Cz*Y*Cz')
###### J2 = trace(Bbar*X*Bbar), where Bbar = Y*Cy'(Dyw*W*Dyw')^-0.5
##### J = J1 + J2
![Cost](https://github.com/ArthurShih/Satellite_control/blob/master/figure/LQG/LQG_cost.png)
###### .
#### Poles and Zeros plot
##### for u1
![u1 pz](https://github.com/ArthurShih/Satellite_control/blob/master/figure/LQG/pz_u1.png)
##### for u2
![u2 pz](https://github.com/ArthurShih/Satellite_control/blob/master/figure/LQG/pz_u2.png)
##### Poles and Zeros value
![u1u2 pz](https://github.com/ArthurShih/Satellite_control/blob/master/figure/LQG/pz_value.png)
