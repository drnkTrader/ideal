# ideal
ideal kodlarım

http://www.davenewberg.com/Trading/TS_Code/Ehlers_Indicators/Cycle_Period_Calculator.html

{Cycle Period Measurement from Cybernetic Analysis for Stocks and Futures by John Ehlers - code compiled by dn}
Inputs: Price((H+L)/2), alpha(.07);
Vars: Smooth(0),Cycle(0),Q1(0),I1(0),DeltaPhase(0),MedianDelta(0),DC(0),InstPeriod(0),Period(0),I2(0),Q2(0);
Smooth = (Price + 2*Price[1] + 2*Price[2] + Price[3])/6;
Cycle = (1 - .5*alpha)*(1 - .5*alpha)*(Smooth - 2*Smooth[1] + Smooth[2]) + 2*(1-alpha)*Cycle[1] - (1 - alpha)*(1-alpha)*Cycle[2];
If currentbar < 7 then Cycle = (Price - 2*Price[1] + Price[2])/4;
Q1 = (.0962*Cycle + .5769*Cycle[2] - .5769*Cycle[4] - .0962*Cycle[6])*(.5+.08*InstPeriod[1]);
I1 = Cycle[3];
If Q1 <> 0 and Q1[1] <> 0 then DeltaPhase = (I1/Q1 - I1[1]/Q1[1]) / (1 + I1*I1[1]/(Q1*Q1[1]));
If DeltaPhase < 0.1 then DeltaPhase = 0.1;
If DeltaPhase > 1.1 then DeltaPhase = 1.1;
MedianDelta = Median(DeltaPhase,5);
If MedianDelta = 0 then DC = 15 else DC = 6.28318 / MedianDelta + .5;
InstPeriod = .33*DC + .67*Instperiod[1];
Period = .15*InstPeriod + .85*Period[1];
Plot1 (Period,"Period",blue);
{This indicator allows the cycle measurement to be determined in very few bars.
It sums the cycle phases until it reaches 360 degrees - a full circle.
The lag in measuring the Dominant Cycle Period is about 8 bars.}

![image](https://user-images.githubusercontent.com/116917602/209720274-89a11177-b7e2-4e16-8d5c-37135daf3dc4.png)
