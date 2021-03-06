<h2> Analytic expressions for the Dekel-Zhao profile </h2>

<p align="justify">
This python program enables to compute the analytical expressions of the Dekel-Zhao dark matter density profile. It is mainly based on the following article: 
</p>

<p align="justify">
<a href="https://ui.adsabs.harvard.edu/abs/2020arXiv200408395F"  style="text-decoration:none" class="type1"><b>The Dekel-Zhao profile: A mass-dependent dark-matter density profile with flexible inner slope and analytic potential, velocity dispersion, and lensing properties</b></a> 
<a href="https://ui.adsabs.harvard.edu/link_gateway/2020arXiv200408395F/EPRINT_PDF" style="text-decoration:none" class="type1"> [PDF] </a>
</p>

<h4 align="justify">
Quantities expressed analytically: 
</h4>
<ul>
       <li>The density </li>
       <li>The average density</li>
       <li>The enclosed mass</li>
       <li>The orbital velocity</li>
       <li>The logarithmic density slope</li>
       <li>The gravitational potential</li>
       <li>The velocity dispersion</li>
</ul>       

<p align="justify">
For the velocity dispersion, it provides both an expression in terms of incomplete beta functions (<a href="https://ui.adsabs.harvard.edu/abs/2020arXiv200408395F/abstract"  style="text-decoration:none" class="type1">Freundlich et al. 2020b</a>, Eq. 19) and two expressions in terms of finite sums (<a href="https://ui.adsabs.harvard.edu/abs/1996MNRAS.278..488Z/abstract"  style="text-decoration:none" class="type1">Zhao 1996</a>, Eq. 19, and <a href="https://ui.adsabs.harvard.edu/abs/2020MNRAS.491.4523F/abstract"  style="text-decoration:none" class="type1">Freundlich et al. 2020a</a>, Eqs. B8 and B10). Some of the quantities are also defined for other profiles (NFW, Einasto, Di Cintio+, generalised NFW with flexible inner slope). 
</p>

<h4 align="justify">
Quantities integrated numerically: 
</h4>
<ul>
       <li>The distribution function</li>
       <li>The projected surface density</li>
       <li>The projected mass</li>
       <li>The lensing convergence</li>
       <li>The lensing shear</li>
</ul> 

<p align="justify">
Except the distribution function, these quantities can be expressed analytically in terms of Fox H functions and series expansions (<a href="https://ui.adsabs.harvard.edu/abs/2020arXiv200408395F/abstract"  style="text-decoration:none" class="type1">Freundlich et al. 2020b</a>, Section 2.3 and Appendix E). 
</p>

<p align="justify">
The program also implements the <b>mass-dependent prescriptions</b> for the Dekel-Zhao and the Di Cintio+ profiles, and provides functions to convert the shape parameters (a,c) into an inner slope s1 and a concentration c2 and vice-versa. 
</p>

<p align="justify">
<a href="./Fitting_functions.py"  style="text-decoration:none" class="type1">Fitting_functions.py</a> provides simple functions to fit simulated density profiles with the Dekel-Zhao profile. The fits are constrained to avoid positive inner slopes. 
</p>

<h4 align="justify">
       Example:  
</h4>

<pre><code>
import numpy as np
import matplotlib.pyplot as plt
import Dekel_profile as prf

s1,c1=(1.,15.)
s2,c2=(1.,5.)
s3,c3=(0.,15.) 
s4,c4=(0.,5.)

rvir=1.
mvir=1.
rhovir=3.*mvir/(4.*np.pi*rvir**3)

p1=prf.params_from_s1c2(s1,c1,0.01*rvir,rvir,mvir)
p2=prf.params_from_s1c2(s2,c2,0.01*rvir,rvir,mvir)
p3=prf.params_from_s1c2(s3,c3,0.01*rvir,rvir,mvir)
p4=prf.params_from_s1c2(s4,c4,0.01*rvir,rvir,mvir)

color1='r'
color2='orangered'
color3='b'
color4='navy'
dashes2=(9,6)
dashes3=(5,4)
dashes4=(2,2)

x=np.linspace(-2,0,100)
y1=np.log10(prf.rho_function(10**x,p1,'dekel')/rhovir)
y2=np.log10(prf.rho_function(10**x,p2,'dekel')/rhovir)
y3=np.log10(prf.rho_function(10**x,p3,'dekel')/rhovir)
y4=np.log10(prf.rho_function(10**x,p4,'dekel')/rhovir)

plt.figure()
plt.plot(x,y1,color=color1,lw=2,label=r'$s_1=%.0f$, $c_{2}=%.0f$'%(s1,c1))
plt.plot(x,y2,color=color2,ls='--',dashes=dashes2,lw=2,label=r'$s_1=%.0f$, $c_{2}=%.0f$'%(s2,c2))
plt.plot(x,y3,color=color3,ls='--',dashes=dashes3,lw=2,label=r'$s_1=%.0f$, $c_{2}=%.0f$'%(s3,c3))
plt.plot(x,y4,color=color4,ls='--',dashes=dashes4,lw=2,label=r'$s_1=%.0f$, $c_{2}=%.0f$'%(s4,c4))

plt.legend(frameon=False,loc='lower left')
plt.xlabel(r'$\log(r/R_{\rm vir})$')
plt.ylabel(r'$\log(\rho/\overline{\rho_{\rm vir}})$')
plt.axis([-2,0,-1,4])
</code></pre>

<p align="center">
 <img src="images/examples_rho.jpg"  width=30%>
 <img src="images/examples_s.jpg"  width=30%>
 <img src="images/examples_U.jpg"  width=30%>
 
 <img src="images/examples_V.jpg"  width=30%>
 <img src="images/examples_sigma.jpg"  width=30%>
 <img src="images/examples_f_log.jpg"  width=30%>
 
 <img src="images/examples_surfdens_truncated.jpg"  width=30%>
 <img src="images/examples_alpha.jpg"  width=30%>
 <img src="images/examples_gamma.jpg"  width=30%>
</p>

