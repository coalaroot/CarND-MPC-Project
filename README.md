# CarND-Controls-MPC
Self-Driving Car Engineer Nanodegree Program

---

## Model


I used the model presented in the lessons where update step is:
```math
x<sub>n+1</sub> = x<sub>n</sub> - (x<sub>n</sub> + v<sub>n</sub> * cos(psi<sub>n</sub>) * dt);
yn+1 = yn - (y<sub>n</sub> + v<sub>n</sub> * sin(psi<sub>n</sub>) * dt);
psi<sub>n+1</sub> = psi<sub>n</sub> - (psi<sub>n</sub> - v<sub>n</sub>/Lf * angle * dt);
v<sub>n+1</sub> = v<sub>n</sub> - (v<sub>n</sub> + a * dt);
cte<sub>n+1</sub> = cte<sub>n</sub> - ((f<sub>n</sub> - y<sub>n</sub>) + (v<sub>n</sub> * sin(epsi<sub>n</sub>) * dt));
epsi<sub>n+1</sub> = epsi<sub>n</sub> - ((psi<sub>n</sub> - psides<sub>n</sub>) - v<sub>n</sub>/Lf * angle * dt);
```
## N and dt values

I tried values in N between 10 and 25 and I chose 10 because I saw it as more efficient than anything above with not noticable cost in precision. With `dt` value I tried the range from 0.05 to 0.3 and ended up on 0.1 as a golden mean.

## Latency

I handle latency by predicting where the vehicle will be in time after latency (100ms) (line #152-#130 in `main.cpp`) and then passes it to MCP::Solve.

## Overall opinion

I think it was challenging to understand every value (variable) and what role it played in creating optimal steering angle and throttle but it was worth the time.