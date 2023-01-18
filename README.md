# MATLAB-Adaptive-Expectations-in-New-Keynesian-Models

Technical Skills: MATLAB (Dynare Library)

This project was done as an assignment for my SFU Undergraduate Class ECON 483  (Special Topics in Economics - Topics in Macroeconomics)

This project simulates stochastic shocks on macro variables of the New Keynesian Model 
and assumes adaptive expectations to show how the economy converges back to steady 
state

The study will look into how the following models converge to steady state
• Pure adaptive expectations (where expected inflation is based on previous years
inflation)
• Trend chasing expectations (where expected inflation is based on past two years of
inflation)
• Using a proportion of population as rational and a proportion as adaptive

![image](https://user-images.githubusercontent.com/122067802/213052905-9c44543b-074a-4a9b-a89c-06dc3082530f.png)

![image](https://user-images.githubusercontent.com/122067802/213052922-49213070-90bb-405b-ae8d-7b1a8386691e.png)

![image](https://user-images.githubusercontent.com/122067802/213052943-b44b8c35-367d-48de-ab29-0e8b2789eed1.png)

![image](https://user-images.githubusercontent.com/122067802/213052960-93ef0073-5a1c-4e20-ae82-9b5bd4b2d69d.png)


Appendix: Code used for Assignment 3

%Block 1
var x pi i u Ex Epi;
varexo epsilon;
parameters beta kappa sigma rhou phipi phix gamma gammaf gammat gammab;

%Block 2
beta=0.99;
kappa=0.3;
sigma=1;
rhou=0.9;
phipi=18.63;
phix=5.77;
gamma=0.71;
gammaf=0.33;
gammab=0.34;
gammat=0.33;

%Block 3
model(linear);
Ex = x(-1);
%Ex = x(+1);%
%Ex = x(-1)+0.5*(x(-1)-x(-2));%
%Ex = gamma*(x(-1))+(1-gamma)*(x(+1));%
%Ex = gammaf*(x(+1))+gammab*(x(-1))+gammat*(x(-1)+0.5*(x(-1)-x(-2)));%
Epi = pi(-1);
%Epi = pi(+1);%
%Epi = pi(-1)+0.5*(pi(-1)-pi(-2));%
%Epi = gamma*(pi(-1))+(1-gamma)*(pi(+1));%
%Epi = gammaf*(pi(+1))+gammab*(pi(-1))+gammat*(pi(-1)+0.5*(pi(-1)-pi(-2)));%
x = Ex - (1/sigma)*(i-Epi)+u;
pi = beta*Epi + kappa*x;
i = phipi*pi + phix*x;
u = rhou*u(-1) + epsilon;

end;

shocks;
var epsilon;
stderr 1;
end;
steady;
stoch_simul;
