<H3>Name : SOUVIK KUNDU</H3>
<H3>Register no : 212221230105</H3>
<H3>EX. NO.5</H3>
<H3>DATE : 16.03.2024</H3>
<H2 ALIGN =CENTER> Implementation of Kalman Filter</H2>

## Aim:
To Construct a Python Code to implement the Kalman filter to predict the position and velocity of an object.

## Algorithm:

Step 1: Define the state transition model F, the observation model H, the process noise covariance Q, 
the measurement noise covariance R, the initial state estimate x0, initial error covariance P0.<BR>
Step 2:  Create a KalmanFilter object with these parameters.<BR>
Step 3: Simulate the movement of the object for a number of time steps, generating true states.<BR>
Step 4: For each measurement, predict the next state using kf.predict().<BR>
Step 5: Update the state estimate based on the measurement using kf.update().<BR>
Step 6: Store the estimated state in a list.<BR>
Step 7: Plot the true and estimated positions.<BR>

##Program:

```
import numpy as np
class KalmanFilter:
  def __init__ (self,F,H,Q,R,x0,P0):
    self.F = F #state transition model
    self.H = H # observation model
    self.Q = Q # process noise covariance
    self.R = R # measurement noise covariance
    self.x = x0 # initial state extimate
    self.P = P0 # initial error covariance
  def predict(self):
    self.x = np.dot(self.F, self.x)
    self.P = np.dot(np.dot(self.F, self.P),self.F.T) + self.Q
  def update(self, z):
    y = z - np.dot(self.H, self.x)
    S = np.dot(np.dot(self.H, self.P),self.H.T) + self.R
    K = np.dot(np.dot(self.P, self.H.T), np.linalg.inv(S))
    self.x = self.x + np.dot(K, y)
dt = 0.1 # time step
F = np.array([[1, dt], [0, 1]]) 
H = np.array([[1, 0]]) 
Q = np.diag([0.1, 0.1]) 
R = np.array([[1]]) 
x0 = np.array([0, 0])
P0 = np.diag([1, 1]) 
kf = KalmanFilter(F,H,Q,R,x0,P0)
true_states=[]
measurements=[]
for i in range(100):
  true_states.append([i*dt, 1]) 
  measurements.append(i*dt + np.random.normal(scale=1)) 
est_states = []
for z in measurements:
    kf.predict()
    kf.update(np.array([z]))
    est_states.append(kf.x)
import matplotlib.pyplot as plt
plt.plot([s[0] for s in true_states], label='true')
plt.plot([s[0] for s in est_states], label='estimate')
plt.legend()
plt.show()
```

<H3>Output:</H3>

![image](https://github.com/SaiDarshan2003/Ex-5--AAI/assets/94692595/453d5860-4cfe-4f58-961b-eb51949aec79)



<H3>Results:</H3>
Thus, Kalman filter is implemented to predict the next position and velocity in Python



