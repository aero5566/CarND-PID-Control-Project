# CarND-Controls-PID

#Describe the effect each of the P, I, D components had in your implementation.  

the P error term is proportional to cross-track error (CET) term and determines the speed of the control system response as the ratio of output response (defined by weight Kp) to the CET signal.  
`p_error = cte; ` 

The D error term is proportional to temporal derivitate of CET, meaning when car has reduce the CET, the car will counter the steers to reduce overshoot. To implement this, I need a value to store prevous CET.  

    d_error = cte - prev_cte_;


The I error term is proportional to the intergal or sum value of CET that observed in the history. And in my implementation, I simply chose sum value.  

    i_error += cte;
And in the end, the steering angle is the combination of P error, I error and D error.  

    double PID::TotalError() {
      /**
       * TODO: Calculate and return the total error
       */
      return -Kp * p_error - Ki * i_error - Kd * d_error;

#Describe how the final hyperparameters were chosen.

I have tried several combination of KP,KI and KD, and finally found this combination makes the behavior more stable.  

    pid.Init(0.114, 0, 3.24);

    msgJson["throttle"] = 0.3;
