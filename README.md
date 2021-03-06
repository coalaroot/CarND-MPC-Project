# CarND-Controls-MPC
Self-Driving Car Engineer Nanodegree Program

---

## Model


I used the model presented in the lessons where update step is:

x<sub>n+1</sub> = x<sub>n</sub> - (x<sub>n</sub> + v<sub>n</sub> * cos(psi<sub>n</sub>) * dt)

yn+1 = yn - (y<sub>n</sub> + v<sub>n</sub> * sin(psi<sub>n</sub>) * dt)

psi<sub>n+1</sub> = psi<sub>n</sub> - (psi<sub>n</sub> - v<sub>n</sub>/Lf * angle * dt)

v<sub>n+1</sub> = v<sub>n</sub> - (v<sub>n</sub> + a * dt)

cte<sub>n+1</sub> = cte<sub>n</sub> - ((f<sub>n</sub> - y<sub>n</sub>) + (v<sub>n</sub> * sin(epsi<sub>n</sub>) * dt))

epsi<sub>n+1</sub> = epsi<sub>n</sub> - ((psi<sub>n</sub> - psides<sub>n</sub>) - v<sub>n</sub>/Lf * angle * dt)

## Transforming waypoints and fitting polynomial

Since waypoint are given in a map's coordinate system, we have to transform it to car's coordinates. I do that in lines #106-#116 in file `main.cpp`. I used equations from the lesson.

## N and dt values

I started with thinking about value of time horizon `N*dt`. As said in lessons, no more than a few seconds is needed and that showed my research when I tried values in N between 10 and 25 and I chose 10 because bigger N added computational time but did not provide any more accuracy because the path planning was ahead enough.

With `dt` value I tried the range from 0.05 to 0.3 and ended up on 0.1 as a golden mean. 0.05 was calculating too often especially that we deal with latenty ~100ms so it makes no sense to set `dt` to smaller value. With higher values the car seemed like it was "lagging" and had a slow reaction time. 

## Latency

I handle latency by predicting where the vehicle will be in time after latency (100ms) (line #152-#130 in `main.cpp`) and then passes it to MCP::Solve.

## Overall opinion

I think it was challenging to understand every value (variable) and what role it played in creating optimal steering angle and throttle but it was worth the time.