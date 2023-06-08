# 如何通过标签计算时间

## 变量

|变量   |单位    |范围  |含义  |
|:-----:|:-----:|:-----|:-----|
|$x_s$     |$quarter$          |$x_s\geq 0$        |当前标签所在节拍            |
|$x_e$     |$quarter$          |$x_e>x_s\geq 0$    |下一标签所在节拍            |
|$t_s$     |$s$             |$t_s\geq 0$        |当前标签所在时间            |
|$t_e$     |$s$             |$t_e>t_s\geq 0$    |下一标签所在时间            |
|$T_s$     |$qpm$           |$T_s>0$            |当前标签曲速                |
|$T_e$     |$qpm$           |$T_e>0$            |下一标签曲速                |
|$\delta$  |$\frac{1}{min}$ |$\delta\neq 0$     |$\frac{T_e-T_s}{x_e-x_s}$  |


## TypeA  
$T(x)=T_s$

1. 由 $x_s$, $T_s$, $t_s$计算 $t(x)$, $x\in[x_s,x_e)$  
   
   $$\Delta x=x-x_s \tag{quarter}$$

   $$\Delta t'=\frac{\Delta x}{T_s} \tag{min}$$

   $$\Delta t=\Delta t'\cdot 60 \tag{s}$$

   $$t(x)=t_s+\Delta t \tag{s}$$

   $$\therefore t(x)=\frac{x-x_s}{T_s}\cdot 60+t_s$$

2. 由 $x_s$, $x_e$, $T_s$, $t_s$计算 $t_e$   
   
   $$t_e=\frac{x_e-x_s}{T_s}\cdot 60+t_s$$

3. 由 $t_s$, $T_s$, $x_s$计算 $x(t)$, $t\in[t_s,t_e)$  
   
   $$\Delta t=t-t_s \tag{s}$$

   $$\Delta t'=\frac{\Delta t}{60} \tag{min}$$

   $$\Delta x=\Delta t'\cdot T_s \tag{quarter}$$

   $$x(t)=x_s+\Delta x \tag{quarter}$$

   $$\therefore x(t)=\frac{t-t_s}{60}\cdot T_s+x_s$$ 

## TypeB  
$T(x)=(x-x_s)\cdot\delta+T_s$  

1. 由 $x_s$, $x_e$, $T_s$, $T_e$, $t_s$计算 $t(x)$, $x\in[x_s,x_e)$  
   
   $$\Delta x=x-x_s \tag{quarter}$$

   由 $T(x)$可得 $T'(\Delta x)=\delta\cdot\Delta x+T_s$.  
   则对于 $\forall\Delta x_0\in[0,x_e-x_s)$, 有  

   $${\rm d}t=\frac{{\rm d}\Delta x}{T'(\Delta x_0)}$$

   则对 $\Delta x$积分有  

   $$\Delta t'_0=\int_{0}^{\Delta x_0}{\frac{1}{T'(\Delta x)}}\,{\rm d}\Delta x=\frac{\ln{|\delta\cdot\Delta x+T_s|}}{\delta}|_{0}^{\Delta x_0}=\frac{\ln{\frac{|\delta\cdot\Delta x_0+T_s|}{T_s}}}{\delta} \tag{min}$$

   $\because \Delta x_0\in[0,x_e-x_s)$且$T_s, T_e>0$. $\therefore \delta\cdot\Delta x_0+T_s>0$.  

   $$\therefore \Delta t'=\frac{\ln{\frac{\delta\cdot\Delta x+T_s}{T_s}}}{\delta} \tag{min}$$

   $$\Delta t=\Delta t'\cdot 60 \tag{s}$$

   $$t(x)=t_s+\Delta t \tag{s}$$

   $$\therefore t(x)=\frac{\ln{\frac{\delta\cdot(x-x_s)+T_s}{T_s}}}{\delta}\cdot 60+t_s$$

2. 由 $x_s$, $x_e$, $T_s$, $T_e$, $t_s$计算 $t_e$  
   
   $$t_e=\frac{\ln{\frac{\delta\cdot(x_e-x_s)+T_s}{T_s}}}{\delta}\cdot 60+t_s$$

3. 由 $t_s$, $t_e$, $T_s$, $T_e$, $x_s$计算 $x(t)$, $t\in[t_s,t_e)$  
   
   $$\Delta t=t-t_s \tag{s}$$

   $$\Delta t'=\frac{\Delta t}{60} \tag{min}$$

   由  

   $$\Delta t'=\frac{\ln{\frac{\delta\cdot\Delta x+T_s}{T_s}}}{\delta} \tag{min}, \Delta x\in[0,x_e-x_s)$$

   可得  

   $$\Delta x=\frac{T_s\cdot e^{\delta\cdot\Delta t'}-T_s}{\delta} \tag{quarter}$$
   
   $$x(t)=x_s+\Delta x \tag{quarter}$$

   $$\therefore x(t)=\frac{T_s\cdot e^{\delta\cdot\frac{t-t_s}{60}}-T_s}{\delta}+x_s$$