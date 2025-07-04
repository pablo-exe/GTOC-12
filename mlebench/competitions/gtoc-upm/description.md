# The Problem of the 12th Global Trajectory Optimisation Competition
## Sustainable Asteroid Mining

Hexi Baoyin, Fanghua Jiang, Zhong Zhang, Nan Zhang, Xiang Guo, Di Wu, Xuan Xie, Jia Yang
*Laboratory of Astrodynamics, School of Aerospace Engineering, Tsinghua University*

Haiyang Li, Yuming Peng, Wei Wang
*Shanghai Institute of Satellite Engineering*

Released: 19 June 2023
\*

## 1. The Scenario

In about 2035, as commercially sustainable asteroid mining may be put into action\*, humanity will plan to mine asteroids and transport their resources back to the Earth. The asteroid mining technology will be greatly developed and integrated into Sustainable Asteroid Miners to automatically extract and refine valuable minerals. A successful mining to an asteroid requires two successive rendezvous to the asteroid by the same or two different Mining Ships propelled by low-thrust electric propulsion. The first rendezvous is to set up a miner and the second is to retrieve the collected mass. Each asteroid can be mined once at most in a submitted solution (i.e., each asteroid can be rendezvoused twice at most). The maximal collected mass mined from an asteroid is proportional to the duration of stay between two moments of rendezvous with this asteroid. The task in GTOC-12 is to transport as many asteroid resources back to the Earth as possible in 15 years.

A game problem is introduced to encourage early submission of the solution and mining those rarely mined asteroids. There is a bonus coefficient for each asteroid and it will decrease with the total mass of the asteroid already mined by all teams' solutions updated on the Leaderboard. The bonus coefficients are released in real time so that all teams can use them to evaluate their new solutions.

## 2. The Problem

All mission events must take place between January 1, 2035, 00:00:00 TT (64328 MJD) and January 1, 2050, 00:00:00 TT (69807 MJD) for possible launches, asteroid rendezvous, and planets flybys. Each team can use a limited number of Mining Ships. All Mining Ships must be launched from the Earth, rendezvous with targets selected in the sixty thousand asteroids to set up a miner or to retrieve the collected mass, and fly by the Earth to unload the resources. They can be performed possible gravity assists (GAs) as needed at three terrestrial planets Venus, Earth, and Mars. Each Mining Ship is equipped with an electric propulsion thruster with a specific impulse $I_{sp} = 4000 \text{ s}$ and a maximum thrust magnitude $T_{max} = 0.6 \text{ N}$, while the direction of thrust is not constrained. The Mining Ship's mass changes continuously when the thruster is on, and it must be no smaller than the sum of its dry mass and collected mass throughout the mission. The collected mass unloaded on the Earth is counted in the merit function (see Section 3) and constrains the number of Mining Ships (see Section 4.e). Figure 1 illustrates a schematic of asteroid mining by multiple Mining Ships.

**(Figure 1 Schematic of sustainable asteroid mining)**
*   Sun
*   Earth
*   First visit to an asteroid
*   Second visit to an asteroid
*   Earth orbit
*   Asteroid orbits
*   Ship trajectories

The candidate asteroids are listed in the file `GTOC12_Asteroids_Data.txt`. They are characterized by identification numbers (asteroid ID from 1 to 60,000), epochs (the mission's initial time 64328 MJD), and corresponding orbital elements (semi-major axis, eccentricity, inclination, longitude of ascending node, argument of perihelion, and mean anomaly). The new bonus coefficients are released in the file `bonus_coefficients.txt` (the bonus coefficient and total collected mass defined in Section 3) in real time when a new solution is updated on Leaderboard.

## 3. Merit Function

The task of the sustainable asteroid mining in this competition is to maximize the total resource value defined by
$$ J = \sum_{i=1}^{60,000} B_i M_i $$
where $B_i$ is the bonus coefficient of the $i$-th asteroid, and $M_i$, in kilograms, is the collected mass of the $i$-th asteroid, which is, of course, zero if the collected mass is not transported back to the Earth. The bonus coefficient of each asteroid at the beginning of the competition is set to $B_0 = 1 \text{ kg}^{-1}$. A new submission will be scored using $B_i$ expressed by
$$ B_i = \frac{1+2(1+\beta \sum M_i)^\gamma}{3}, \quad i=1,2,\dots,60000 $$
where $\beta = 0.05 \text{ kg}^{-1}$, $\gamma = -0.1$, and $\sum M_i$, in kilograms, denotes the total collected mass mined from the $i$-th asteroid by all solutions ever updated on the Leaderboard before this new submission.

## 4. Constraints

The scenario of the sustainable asteroid mining mission is set with the following constraints.
a. All the mission events (including the launches, thrust on/off, rendezvous, planetary flybys, etc.) must take place between 64328 MJD and 69807 MJD.
b. The position of each Mining Ship at the moment of launch, rendezvous, and planetary flybys must be equal to the position of the Earth, asteroid, and planet at the same time, respectively. The hyperbolic excess velocity of each Mining Ship relative to the Earth must be no larger than 6.0 km/s at the moment of launch and unloading resources. The velocity of each Mining Ship at the moment of rendezvous must be equal to the velocity of target asteroid.
c. The time interval between two successive rendezvous of the same asteroid must be no less than 1 year: $t_{2i} - t_{1i} \ge 1 \text{ yr}$, where $t_{2i}$ and $t_{1i}$ denote the moments of the second and first rendezvous to the $i$-th asteroid, respectively. The collected mass $M_i$ on the $i$-th asteroid is constrained by $M_i \le k(t_{2i} - t_{1i})$ where the rate of mining resources is $k = 10.0 \text{ kg/yr}$.
d. The initial mass of each Mining Ship is constrained by $m_0 = m_d + m_p + I m_s \le 3000 \text{ kg}$, where $m_d = 500 \text{ kg}$ is the constant dry mass, $m_p$ is the propellant mass, $I (\le 20)$ is the number of miners, and $m_s = 40 \text{ kg}$ is the mass of a miner. The final mass of each Mining Ship must be no smaller than the sum of the dry mass 500 kg and collected mass on the ship.
e. The number of Mining Ships used in each solution, $N$, is constrained by
   $$ N \le \min \left[ 100, 2 \exp(\rho \bar{M}) \right], \text{ where } \rho = 0.004 \text{ kg}^{-1}, \text{ and } \bar{M} = \frac{1}{N} \sum_{i=1}^{60000} M_i \text{, in kilograms, is the} $$
   average collected mass transported back to the Earth per Mining Ship in this solution. Illustrative examples for the maximum number of Mining Ships are given in Table 1.

   **Table 1 Maximum number of Mining Ships as a function of the average collected mass**
   | $\bar{M}$ (kg) | 100 | 300 | 500 | 700 | 900 | 1000 |
   |----------------|-----|-----|-----|-----|-----|------|
   | $N_{max}$      | 2   | 6   | 14  | 32  | 73  | 100  |

f. Gravity assists at the planets Venus, Earth, and Mars are allowed. The GA impulse model is given in Section 6.2. If the Mining Ship flies by the Earth with a hyperbolic excess velocity no larger than 6 km/s, all resources carried by this ship will be instantaneously unloaded on the Earth.
g. The distance from the Sun to each Mining Ship must be no less than 0.3 AU: $r(t) \ge 0.3 \text{ AU}$.
h. Tolerances in the position, velocity, and mass of each Mining Ship at all events are 1,000 km, 1.0 m/s, and 0.001 kg, respectively.

## 5. Submission

The registered user of each team can submit the solution file via the competition website https://gtoc12.tsinghua.edu.cn/. The file format is defined in `GTOC12_Submission_Format.pdf`. The solution will be automatically verified immediately after upload. If its format is correct, the number of Mining Ships, the number of mined asteroids, and the total collected mass will be displayed. This solution will be recognized as a **candidate solution**. All solutions will be listed in order of upload time.
The user can choose when to submit (up to 5 times per team per day) any candidate solution of the team, and the score will be evaluated on the website in real time. Once the score of the submitted candidate solution is higher than the team's record, this candidate solution will be recognized as a **valid solution**. The **Leaderboard** and **bonus coefficients** will be updated immediately according to this valid solution. The submission epoch, score, and the numbers of Mining Ships and mined asteroids will be displayed in the **Leaderboard**.

**(Figure 2 Submission process on the website)**
*(A flowchart depicting: Upload Solution File -> Candidate Solution? (Yes -> Submit -> Valid Solution? (Yes -> Update bonus and Leaderboard -> Finish; No -> Display score); No -> Display errors). An arrow from "Update bonus and Leaderboard" also points to "Evaluate subsequent solutions" which feeds back before "Valid Solution?")*

## 6. Appendices

### 6.1 Dynamic Model

In the Sun's central gravitational field, the motions of planets, asteroids, and un-propelled Mining Ships are all governed by
$$ \dot{\mathbf{r}} = \mathbf{v} $$
$$ \dot{\mathbf{v}} = -\frac{\mu}{r^3}\mathbf{r} $$
where $\mathbf{r}$ (with $r = ||\mathbf{r}||$) and $\mathbf{v}$ are the position and velocity in the J2000 heliocentric ecliptic frame, respectively, and $\mu$ is the gravitational parameter of the Sun.
The initial states of planets and asteroids are described by their initial mean anomaly $M_0$ along with their other five constant orbital elements: the semi-major axis $a$, eccentricity $e$, inclination $i$, longitude of ascending node $\Omega$, and argument of perihelion $\omega$. The mean anomaly at time $t$, $M_t$, is computed by
$$ M_t = M_0 + \sqrt{\frac{\mu}{a^3}}(t-t_0) $$
The orbital eccentric anomaly $E$ at time $t$ is obtained by solving the Kepler's equation:
$$ M_t = E - e \sin E $$
The orbital elements are related to the Cartesian position and velocity according to the expressions
$$ \mathbf{r} = r(\mathbf{P}\cos f + \mathbf{Q} \sin f) $$
$$ \mathbf{v} = \sqrt{\frac{\mu}{a(1-e^2)}} [-\mathbf{P}\sin f + \mathbf{Q}(e+\cos f)] $$
where $r = \frac{a(1-e^2)}{1+e\cos f}$, $\tan \frac{f}{2} = \sqrt{\frac{1+e}{1-e}} \tan \frac{E}{2}$, and $f$ is the true anomaly. The vectors $\mathbf{P}$ and $\mathbf{Q}$ are given by
$$ \mathbf{P} = \begin{pmatrix} \cos\omega\cos\Omega - \sin\omega\sin\Omega\cos i \\ \cos\omega\sin\Omega + \sin\omega\cos\Omega\cos i \\ \sin\omega\sin i \end{pmatrix} $$
$$ \mathbf{Q} = \begin{pmatrix} -\sin\omega\cos\Omega - \cos\omega\sin\Omega\cos i \\ -\sin\omega\sin\Omega + \cos\omega\cos\Omega\cos i \\ \cos\omega\sin i \end{pmatrix} $$
Every Mining Ship is propelled by the electric thrust, and its position, velocity, and mass change continuously when the thruster is on:
$$ \dot{\mathbf{r}} = \mathbf{v} $$
$$ \dot{\mathbf{v}} = -\frac{\mu}{r^3}\mathbf{r} + \frac{T}{m}\mathbf{\alpha} $$
$$ \dot{m} = -\frac{T}{I_{sp}g_0} $$
where $T$ ($0 \le T \le T_{max}$) is the magnitude of thrust, $\mathbf{\alpha}$ is the unit vector of thrust direction, $m$ is the instantaneous mass of the Mining Ship, $I_{sp}$ is the specific impulse, and $g_0$ is the gravitational acceleration at sea level. The Mining Ship mass changes instantaneously at the moment of rendezvous as it releases a miner or collects resources:
$$ m(t_{1i}^+) = m(t_{1i}^-) - m_s $$
$$ m(t_{2i}^+) = m(t_{2i}^-) + M_i $$
where $t_{1i}$ and $t_{2i}$ denote the moments of the first and second rendezvous with the $i$-th asteroid, respectively, $m_s$ is the mass of a miner, $M_i$ is the collected mass on the $i$-th asteroid, and $t^-$ and $t^+$ refer to the states immediately before and after the rendezvous, respectively.

### 6.2 GA impulse model

The GA impulse model (i.e., the same GA model used in the previous GTOCs) is used at the planetary flyby moment $t_g$ when the Mining Ship's positions at the moments immediately before and after GA, $\mathbf{r}(t_g^-)$ and $\mathbf{r}(t_g^+)$, respectively, are both equal to the planet's position $\mathbf{r}_p(t_g)$:
$$ \mathbf{r}(t_g^-) = \mathbf{r}(t_g^+) = \mathbf{r}_p(t_g) $$
The time spent inside the planetary influence is neglected. The hyperbolic excess velocity is calculated by the heliocentric velocity of the Mining Ship relative to that of the planet:
$$ \mathbf{v}_\infty(t_g^-) = \mathbf{v}(t_g^-) - \mathbf{v}_p(t_g) $$
$$ \mathbf{v}_\infty(t_g^+) = \mathbf{v}(t_g^+) - \mathbf{v}_p(t_g) $$
where $\mathbf{v}_p$ is the planet's velocity. The magnitude of hyperbolic excess velocity remains invariant, but its direction has an instantaneous change:
$$ ||\mathbf{v}_\infty(t_g^-)|| = ||\mathbf{v}_\infty(t_g^+)|| = v_\infty $$
$$ \mathbf{v}_\infty(t_g^-) \cdot \mathbf{v}_\infty(t_g^+) = v_\infty^2 \cos\theta $$
where the direction change angle $\theta$ is constrained by the minimum pericenter radius $r_{p,min}$
$$ \sin \frac{\theta}{2} = \frac{\mu_p/r_p}{v_\infty^2 + \mu_p/r_p}, \quad r_p \ge r_{p,min} $$
where $r_p$ is the pericenter radius and $\mu_p$ is the gravitational parameter of the planet.
The Mining Ship mass changes instantaneously at the moment of Earth flyby with a hyperbolic excess velocity no larger than 6.0 km/s:
$$ m(t_g^+) = m(t_g^-) - M $$
where $M$ is equal to the total collected mass carried by this ship.

### 6.3 Constants

The planets' parameters and orbital elements at the mission initial time $t = 64328$ MJD are given in Table 2. The values of some constant parameters are provided in Table 3.

**Table 2 The planets' parameters and orbital elements ($t = 64328$ MJD)**

|                                      | Venus                 | Earth                 | Mars                  |
|--------------------------------------|-----------------------|-----------------------|-----------------------|
| Gravitational parameter, km³/s²      | 3.24858592000e5       | 3.98600435436e5       | 4.28283752140e4       |
| Minimum pericenter radius, km        | 6351.0                | 6678.0                | 3689.0                |
| Semi-major axis, km                  | 1.08208010521e8       | 1.49579151285e8       | 2.27951663551e8       |
| Eccentricity                         | 6.72988099539e-3      | 1.65519129162e-2      | 9.33662184095e-2      |
| Inclination, deg                     | 3.39439096544         | 4.64389155500e-3      | 1.84693231241         |
| Longitude of ascending node, deg     | 7.65796397775e1       | 1.98956406477e2       | 4.94553142513e1       |
| Argument of perihelion, deg          | 5.51107191497e1       | 2.62960364700e2       | 2.86731029267e2       |
| Mean anomaly, deg                    | 1.11218416921e1       | 3.58039899470e2       | 2.38232037154e2       |

**Table 3 Values of some constant parameters**

| Parameter | Value             | Unit    |
|-----------|-------------------|---------|
| $\mu$     | 1.32712440018e11  | km³/s²  |
| $g_0$     | 9.80665           | m/s²    |
| AU        | 1.49597870691e8   | km      |
| Day       | 86400.0           | s       |
| Year      | 365.25            | day     |

---
\* Elvis, M. Let's mine asteroids — for science and profit. *Nature* 485, 549 (2012). https://doi.org/10.1038/485549a

    1     0            64328.00000000    -25267390.158699154854    144918560.832322776318       -11774.074663434592          -29.830354405016           -5.218793306247           -0.000385365490         3000.000000000000
    1     0            64328.00000000    -25267390.158699154854    144918560.832322776318       -11774.074663434592          -35.262040532514           -7.689520676679           -0.626717604266         3000.000000000000
    1    -1            64328.00000000            0.000000000000            0.000000000000            0.000000000000
    1    -1            64328.00000000           -0.543168612659           -0.247072737002           -0.062633223867
    1    -1            64329.00000000           -0.543044740245           -0.247252300427           -0.062997697620
    1    -1            64330.00000000           -0.542865763977           -0.247550970393           -0.063366231059
    1    -1            64331.00000000           -0.542634451136           -0.247961915767           -0.063739631702
    1    -1            64332.00000000           -0.542353576956           -0.248478146147           -0.064118704993
    1    -1            64333.00000000           -0.542025929712           -0.249092537658           -0.064504256319
    1    -1            64334.00000000           -0.541654315881           -0.249797856767           -0.064897093325
    1    -1            64335.00000000           -0.541241565270           -0.250586782118           -0.065298028541
    1    -1            64336.00000000           -0.540790535995           -0.251451924349           -0.065707882322
    1    -1            64337.00000000           -0.540304119241           -0.252385843879           -0.066127486117
    1    -1            64338.00000000           -0.539785243748           -0.253381066649           -0.066557686080
    1    -1            64339.00000000           -0.539236879975           -0.254430097764           -0.066999347058
    1    -1            64340.00000000           -0.538662043944           -0.255525433032           -0.067453356980
    1    -1            64341.00000000           -0.538063800734           -0.256659568321           -0.067920631691
    1    -1            64342.00000000           -0.537445267679           -0.257825006681           -0.068402120286
    1    -1            64343.00000000           -0.536809617279           -0.259014263159           -0.068898810999
    1    -1            64344.00000000           -0.536160079891           -0.260219867185           -0.069411737720
    1    -1            64345.00000000           -0.535499946266           -0.261434362415           -0.069941987231
    1    -1            64346.00000000           -0.534832570011           -0.262650303875           -0.070490707259
    1    -1            64347.00000000           -0.534161370092           -0.263860252197           -0.071059115472
    1    -1            64348.00000000           -0.533489833482           -0.265056764732           -0.071648509556
    1    -1            64349.00000000           -0.532821518091           -0.266232383236           -0.072260278547
    1    -1            64350.00000000           -0.532160056145           -0.267379617789           -0.072895915621
    1    -1            64351.00000000           -0.531509158164           -0.268490926527           -0.073557032568
    1    -1            64352.00000000           -0.530872617748           -0.269558690658           -0.074245376257
    1    -1            64353.00000000           -0.530254317390           -0.270575184151           -0.074962847407
    1    -1            64354.00000000           -0.529658235543           -0.271532537321           -0.075711522093
    1    -1            64355.00000000           -0.529088455240           -0.272422693389           -0.076493676459
    1    -1            64356.00000000           -0.528549174560           -0.273237356846           -0.077311815239
    1    -1            64357.00000000           -0.528044719298           -0.273967932231           -0.078168704802
    1    -1            64358.00000000           -0.527579558246           -0.274605451556           -0.079067411596
    1    -1            64359.00000000           -0.527158321536           -0.275140488219           -0.080011347056
    1    -1            64360.00000000           -0.526785822576           -0.275563054681           -0.081004320299
    1    -1            64361.00000000           -0.526467084175           -0.275862480523           -0.082050600243
    1    -1            64362.00000000           -0.526207369548           -0.276027266574           -0.083154989154
    1    -1            64363.00000000           -0.526012218997           -0.276044909684           -0.084322910190
    1    -1            64364.00000000           -0.525887493149           -0.275901691179           -0.085560512115
    1    -1            64365.00000000           -0.525839423762           -0.275582420066           -0.086874795242
    1    -1            64366.00000000           -0.525874673216           -0.275070119391           -0.088273763759
    1    -1            64367.00000000           -0.526000403869           -0.274345640649           -0.089766611090
    1    -1            64368.00000000           -0.526224358482           -0.273387186306           -0.091363946851
    1    -1            64369.00000000           -0.526554952800           -0.272169713999           -0.093078076601
    1    -1            64370.00000000           -0.527001381023           -0.270664186910           -0.094923349101
    1    -1            64371.00000000           -0.527573734102           -0.268836622210           -0.096916590552
    1    -1            64372.00000000           -0.528283129195           -0.266646871700           -0.099077651873
    1    -1            64373.00000000           -0.529141845627           -0.264047043268           -0.101430104149
    1    -1            64374.00000000           -0.530163457199           -0.260979434979           -0.104002130022
    1    -1            64375.00000000           -0.531362940690           -0.257373799440           -0.106827676673
    1    -1            64376.00000000           -0.532756722429           -0.253143675412           -0.109947961263
    1    -1            64377.00000000           -0.534362592137           -0.248181401535           -0.113413455713
    1    -1            64378.00000000           -0.536199353571           -0.242351239315           -0.117286529116
    1    -1            64379.00000000           -0.538285970920           -0.235479739148           -0.121644999245
    1    -1            64380.00000000           -0.540639761618           -0.227342017273           -0.126586947272
    1    -1            64381.00000000           -0.543272785904           -0.217641860625           -0.132237288535
    1    -1            64382.00000000           -0.546184796212           -0.205982351141           -0.138756763026
    1    -1            64383.00000000           -0.549349521667           -0.191821689786           -0.146354167182
    1    -1            64384.00000000           -0.552687774118           -0.174405625604           -0.155302614204
    1    -1            64385.00000000           -0.556013871238           -0.152662775166           -0.165959790158
    1    -1            64386.00000000           -0.558926703159           -0.125042121062           -0.178788725415
    1    -1            64387.00000000           -0.560583691468           -0.089266845728           -0.194363975555
    1    -1            64388.00000000           -0.559226452547           -0.041996267822           -0.213312184698
    1    -1            64389.00000000           -0.551204635623            0.021484871665           -0.236033577776
    1    -1            64390.00000000           -0.529178000505            0.106898910738           -0.261807690003
    1    -1            64390.47583523           -0.510207358738            0.156547118119           -0.274192360904
    1    -1            64390.47583523            0.000000000000            0.000000000000            0.000000000000
    1    -1            64395.07741531            0.000000000000            0.000000000000            0.000000000000
    1    -1            64395.07741531            0.046256181533            0.560842357396           -0.208109749739
    1    -1            64396.07741531            0.143731409689            0.558178006763           -0.166669116859
    1    -1            64397.07741531            0.213047021884            0.544993288668           -0.132639668474
    1    -1            64398.07741531            0.262478351113            0.529074534569           -0.105760351490
    1    -1            64399.07741531            0.298522865399            0.513541965081           -0.084609389640
    1    -1            64400.07741531            0.325540614314            0.499426079346           -0.067800439388
    1    -1            64401.07741531            0.346350939190            0.486927340702           -0.054247503899
    1    -1            64402.07741531            0.362784538844            0.475946722333           -0.043152007561
    1    -1            64403.07741531            0.376053098079            0.466296526774           -0.033935474412
    1    -1            64404.07741531            0.386977946224            0.457780312049           -0.026177374140
    1    -1            64405.07741531            0.396129551370            0.450220444403           -0.019568593532
    1    -1            64406.07741531            0.403913443798            0.443465117539           -0.013878736447
    1    -1            64407.07741531            0.410624142073            0.437387706154           -0.008933550936
    1    -1            64408.07741531            0.416479745298            0.431883627460           -0.004599344375
    1    -1            64409.07741531            0.421644624811            0.426866740395           -0.000772134938
    1    -1            64410.07741531            0.426244635426            0.422266022559            0.002629989058
    1    -1            64411.07741531            0.430377523039            0.418022741379            0.005672321667
    1    -1            64412.07741531            0.434120182754            0.414088131964            0.008407483076
    1    -1            64413.07741531            0.437533810899            0.410421523033            0.010878310125
    1    -1            64414.07741531            0.440667622249            0.406988835385            0.013120002033
    1    -1            64415.07741531            0.443561572750            0.403761381169            0.015161732623
    1    -1            64416.07741531            0.446248381719            0.400714902575            0.017027875606
    1    -1            64417.07741531            0.448755053164            0.397828799924            0.018738945832
    1    -1            64418.07741531            0.451104033952            0.395085509347            0.020312329661
    1    -1            64419.07741531            0.453314105253            0.392469998740            0.021762857056
    1    -1            64420.07741531            0.455401075730            0.389969357480            0.023103253672
    1    -1            64421.07741531            0.457378325673            0.387572460776            0.024344501086
    1    -1            64422.07741531            0.459257237921            0.385269693661            0.025496126049
    1    -1            64423.07741531            0.461047541933            0.383052722896            0.026566434449
    1    -1            64424.07741531            0.462757590611            0.380914307527            0.027562701854
    1    -1            64425.07741531            0.464394584620            0.378848140802            0.028491329673
    1    -1            64426.07741531            0.465964755379            0.376848717646            0.029357973937
    1    -1            64427.07741531            0.467473515253            0.374911223070            0.030167652091
    1    -1            64428.07741531            0.468925581567            0.373031437812            0.030924832030
    1    -1            64429.07741531            0.470325079533            0.371205658221            0.031633506715
    1    -1            64430.07741531            0.471675628137            0.369430627982            0.032297257001
    1    -1            64431.07741531            0.472980412131            0.367703479714            0.032919304777
    1    -1            64432.07741531            0.474242242643            0.366021684841            0.033502558105
    1    -1            64433.07741531            0.475463608429            0.364383010433            0.034049649732
    1    -1            64434.07741531            0.476646719370            0.362785481923            0.034562970058
    1    -1            64435.07741531            0.477793543513            0.361227350815            0.035044695472
    1    -1            64436.07741531            0.478905838731            0.359707066640            0.035496812794
    1    -1            64437.07741531            0.479985179867            0.358223252538            0.035921140422
    1    -1            64438.07741531            0.481032982056            0.356774683954            0.036319346694
    1    -1            64439.07741531            0.482050520837            0.355360270003            0.036692965876
    1    -1            64440.07741531            0.483038949526            0.353979037146            0.037043412126
    1    -1            64441.07741531            0.483999314263            0.352630114861            0.037371991724
    1    -1            64442.07741531            0.484932567061            0.351312723052            0.037679913812
    1    -1            64443.07741531            0.485839577158            0.350026160956            0.037968299852
    1    -1            64444.07741531            0.486721140897            0.348769797372            0.038238191974
    1    -1            64445.07741531            0.487577990344            0.347543062044            0.038490560363
    1    -1            64446.07741531            0.488410800816            0.346345438045            0.038726309810
    1    -1            64447.07741531            0.489220197461            0.345176455047            0.038946285540
    1    -1            64448.07741531            0.490006761015            0.344035683381            0.039151278396
    1    -1            64449.07741531            0.490771032854            0.342922728772            0.039342029480
    1    -1            64450.07741531            0.491513519416            0.341837227687            0.039519234295
    1    -1            64451.07741531            0.492234696086            0.340778843225            0.039683546463
    1    -1            64452.07741531            0.492935010605            0.339747261477            0.039835581068
    1    -1            64453.07741531            0.493614886066            0.338742188310            0.039975917658
    1    -1            64454.07741531            0.494274723546            0.337763346531            0.040105102965
    1    -1            64455.07741531            0.494914904418            0.336810473377            0.040223653346
    1    -1            64456.07741531            0.495535792389            0.335883318310            0.040332057013
    1    -1            64457.07741531            0.496137735283            0.334981641075            0.040430776036
    1    -1            64458.07741531            0.496721066622            0.334105209989            0.040520248177
    1    -1            64459.07741531            0.497286107001            0.333253800447            0.040600888557
    1    -1            64460.07741531            0.497833165309            0.332427193612            0.040673091168
    1    -1            64461.07741531            0.498362539799            0.331625175274            0.040737230266
    1    -1            64462.07741531            0.498874519022            0.330847534857            0.040793661639
    1    -1            64463.07741531            0.499369382659            0.330094064560            0.040842723767
    1    -1            64464.07741531            0.499847402246            0.329364558618            0.040884738895
    1    -1            64465.07741531            0.500308841806            0.328658812668            0.040920014013
    1    -1            64466.07741531            0.500753958415            0.327976623206            0.040948841764
    1    -1            64467.07741531            0.501183002692            0.327317787137            0.040971501275
    1    -1            64468.07741531            0.501596219227            0.326682101388            0.040988258932
    1    -1            64469.07741531            0.501993846964            0.326069362596            0.040999369094
    1    -1            64470.07741531            0.502376119533            0.325479366854            0.041005074756
    1    -1            64471.07741531            0.502743265538            0.324911909502            0.041005608160
    1    -1            64472.07741531            0.503095508819            0.324366784971            0.041001191373
    1    -1            64473.07741531            0.503433068674            0.323843786668            0.040992036816
    1    -1            64474.07741531            0.503756160057            0.323342706891            0.040978347759
    1    -1            64475.07741531            0.504064993756            0.322863336777            0.040960318788
    1    -1            64476.07741531            0.504359776542            0.322405466282            0.040938136237
    1    -1            64477.07741531            0.504640711307            0.321968884178            0.040911978592
    1    -1            64478.07741531            0.504907997188            0.321553378075            0.040882016874
    1    -1            64479.07741531            0.505161829669            0.321158734457            0.040848414995
    1    -1            64480.07741531            0.505402400676            0.320784738738            0.040811330094
    1    -1            64481.07741531            0.505629898667            0.320431175323            0.040770912851
    1    -1            64482.07741531            0.505844508707            0.320097827690            0.040727307788
    1    -1            64483.07741531            0.506046412534            0.319784478468            0.040680653544
    1    -1            64484.07741531            0.506235788626            0.319490909537            0.040631083144
    1    -1            64485.07741531            0.506412812260            0.319216902118            0.040578724249
    1    -1            64486.07741531            0.506577655559            0.318962236881            0.040523699387
    1    -1            64487.07741531            0.506730487550            0.318726694048            0.040466126185
    1    -1            64488.07741531            0.506871474205            0.318510053499            0.040406117576
    1    -1            64489.07741531            0.507000778485            0.318312094885            0.040343781998
    1    -1            64490.07741531            0.507118560385            0.318132597733            0.040279223592
    1    -1            64491.07741531            0.507224976972            0.317971341556            0.040212542376
    1    -1            64492.07741531            0.507320182425            0.317828105965            0.040143834424
    1    -1            64493.07741531            0.507404328072            0.317702670771            0.040073192023
    1    -1            64494.07741531            0.507477562424            0.317594816092            0.040000703835
    1    -1            64495.07741531            0.507540031218            0.317504322458            0.039926455042
    1    -1            64496.07741531            0.507591877444            0.317430970908            0.039850527488
    1    -1            64497.07741531            0.507633241389            0.317374543091            0.039772999817
    1    -1            64498.07741531            0.507664260665            0.317334821360            0.039693947598
    1    -1            64499.07741531            0.507685070248            0.317311588860            0.039613443452
    1    -1            64500.07741531            0.507695802513            0.317304629621            0.039531557163
    1    -1            64501.07741531            0.507696587264            0.317313728642            0.039448355800
    1    -1            64502.07741531            0.507687551777            0.317338671969            0.039363903815
    1    -1            64503.07741531            0.507668820827            0.317379246775            0.039278263152
    1    -1            64504.07741531            0.507640516729            0.317435241435            0.039191493342
    1    -1            64505.07741531            0.507602759369            0.317506445593            0.039103651597
    1    -1            64506.07741531            0.507555666241            0.317592650232            0.039014792904
    1    -1            64507.07741531            0.507499352483            0.317693647735            0.038924970106
    1    -1            64508.07741531            0.507433930911            0.317809231947            0.038834233986
    1    -1            64509.07741531            0.507359512055            0.317939198226            0.038742633351
    1    -1            64510.07741531            0.507276204193            0.318083343501            0.038650215101
    1    -1            64511.07741531            0.507184113388            0.318241466317            0.038557024306
    1    -1            64512.07741531            0.507083343524            0.318413366883            0.038463104275
    1    -1            64513.07741531            0.506973996340            0.318598847113            0.038368496623
    1    -1            64514.07741531            0.506856171464            0.318797710668            0.038273241335
    1    -1            64515.07741531            0.506729966450            0.319009762985            0.038177376828
    1    -1            64516.07741531            0.506595476815            0.319234811320            0.038080940010
    1    -1            64517.07741531            0.506452796068            0.319472664771            0.037983966338
    1    -1            64518.07741531            0.506302015752            0.319723134306            0.037886489872
    1    -1            64519.07741531            0.506143225471            0.319986032793            0.037788543328
    1    -1            64520.07741531            0.505976512932            0.320261175015            0.037690158127
    1    -1            64521.07741531            0.505801963972            0.320548377693            0.037591364444
    1    -1            64522.07741531            0.505619662596            0.320847459505            0.037492191256
    1    -1            64523.07741531            0.505429691011            0.321158241098            0.037392666387
    1    -1            64524.07741531            0.505232129656            0.321480545099            0.037292816549
    1    -1            64525.07741531            0.505027057237            0.321814196131            0.037192667384
    1    -1            64526.07741531            0.504814550759            0.322159020817            0.037092243505
    1    -1            64527.07741531            0.504594685559            0.322514847787            0.036991568533
    1    -1            64528.07741531            0.504367535337            0.322881507683            0.036890665137
    1    -1            64529.07741531            0.504133172187            0.323258833165            0.036789555063
    1    -1            64530.07741531            0.503891666628            0.323646658907            0.036688259175
    1    -1            64531.07741531            0.503643087637            0.324044821600            0.036586797483
    1    -1            64532.07741531            0.503387502676            0.324453159948            0.036485189179
    1    -1            64533.07741531            0.503124977724            0.324871514668            0.036383452662
    1    -1            64534.07741531            0.502855577304            0.325299728483            0.036281605572
    1    -1            64535.07741531            0.502579364516            0.325737646115            0.036179664815
    1    -1            64536.07741531            0.502296401060            0.326185114281            0.036077646591
    1    -1            64537.07741531            0.502006747268            0.326641981683            0.035975566422
    1    -1            64538.07741531            0.501710462132            0.327108098997            0.035873439174
    1    -1            64539.07741531            0.501407603326            0.327583318866            0.035771279083
    1    -1            64540.07741531            0.501098227239            0.328067495890            0.035669099778
    1    -1            64541.07741531            0.500782388996            0.328560486606            0.035566914304
    1    -1            64542.07741531            0.500460142487            0.329062149485            0.035464735140
    1    -1            64543.07741531            0.500131540391            0.329572344912            0.035362574225
    1    -1            64544.07741531            0.499796634200            0.330090935173            0.035260442976
    1    -1            64545.07741531            0.499455474246            0.330617784441            0.035158352305
    1    -1            64546.07741531            0.499108109720            0.331152758762            0.035056312641
    1    -1            64547.07741531            0.498754588701            0.331695726032            0.034954333944
    1    -1            64548.07741531            0.498394958174            0.332246555991            0.034852425726
    1    -1            64549.07741531            0.498029264056            0.332805120194            0.034750597067
    1    -1            64550.07741531            0.497657551216            0.333371292004            0.034648856628
    1    -1            64551.07741531            0.497279863497            0.333944946566            0.034547212669
    1    -1            64552.07741531            0.496896243738            0.334525960796            0.034445673064
    1    -1            64553.07741531            0.496506733794            0.335114213354            0.034344245312
    1    -1            64554.07741531            0.496111374554            0.335709584632            0.034242936555
    1    -1            64555.07741531            0.495710205968            0.336311956733            0.034141753591
    1    -1            64556.07741531            0.495303267055            0.336921213449            0.034040702882
    1    -1            64557.07741531            0.494890595934            0.337537240244            0.033939790571
    1    -1            64558.07741531            0.494472229835            0.338159924236            0.033839022492
    1    -1            64559.07741531            0.494048205117            0.338789154171            0.033738404182
    1    -1            64560.07741531            0.493618557292            0.339424820409            0.033637940891
    1    -1            64561.07741531            0.493183321036            0.340066814901            0.033537637595
    1    -1            64562.07741531            0.492742530208            0.340715031169            0.033437499003
    1    -1            64563.07741531            0.492296217868            0.341369364289            0.033337529569
    1    -1            64564.07741531            0.491844416293            0.342029710863            0.033237733500
    1    -1            64565.07741531            0.491387156991            0.342695969007            0.033138114768
    1    -1            64566.07741531            0.490924470718            0.343368038328            0.033038677115
    1    -1            64567.07741531            0.490456387492            0.344045819900            0.032939424065
    1    -1            64568.07741531            0.489982936610            0.344729216250            0.032840358928
    1    -1            64569.07741531            0.489504146661            0.345418131333            0.032741484813
    1    -1            64570.07741531            0.489020045540            0.346112470514            0.032642804632
    1    -1            64571.07741531            0.488530660463            0.346812140548            0.032544321109
    1    -1            64572.07741531            0.488036017978            0.347517049558            0.032446036784
    1    -1            64573.07741531            0.487536143981            0.348227107019            0.032347954027
    1    -1            64574.07741531            0.487031063728            0.348942223734            0.032250075034
    1    -1            64575.07741531            0.486520801848            0.349662311817            0.032152401845
    1    -1            64576.07741531            0.486005382352            0.350387284673            0.032054936339
    1    -1            64577.07741531            0.485484828652            0.351117056979            0.031957680250
    1    -1            64578.07741531            0.484959163565            0.351851544663            0.031860635163
    1    -1            64579.07741531            0.484428409329            0.352590664885            0.031763802529
    1    -1            64580.07741531            0.483892587613            0.353334336022            0.031667183662
    1    -1            64581.07741531            0.483351719530            0.354082477643            0.031570779749
    1    -1            64582.07741531            0.482805825641            0.354835010497            0.031474591854
    1    -1            64583.07741531            0.482254925976            0.355591856488            0.031378620922
    1    -1            64584.07741531            0.481699040034            0.356352938662            0.031282867783
    1    -1            64585.07741531            0.481138186800            0.357118181186            0.031187333159
    1    -1            64586.07741531            0.480572384749            0.357887509330            0.031092017665
    1    -1            64587.07741531            0.480001651861            0.358660849451            0.030996921815
    1    -1            64588.07741531            0.479426005627            0.359438128974            0.030902046025
    1    -1            64589.07741531            0.478845463058            0.360219276375            0.030807390618
    1    -1            64590.07741531            0.478260040696            0.361004221164            0.030712955828
    1    -1            64591.07741531            0.477669754619            0.361792893868            0.030618741800
    1    -1            64592.07741531            0.477074620453            0.362585226013            0.030524748597
    1    -1            64593.07741531            0.476474653379            0.363381150110            0.030430976204
    1    -1            64594.07741531            0.475869868139            0.364180599635            0.030337424526
    1    -1            64595.07741531            0.475260279048            0.364983509016            0.030244093396
    1    -1            64596.07741531            0.474645899998            0.365789813616            0.030150982577
    1    -1            64597.07741531            0.474026744465            0.366599449715            0.030058091764
    1    -1            64598.07741531            0.473402825522            0.367412354497            0.029965420586
    1    -1            64599.07741531            0.472774155837            0.368228466036            0.029872968610
    1    -1            64600.07741531            0.472140747689            0.369047723274            0.029780735343
    1    -1            64601.07741531            0.471502612970            0.369870066014            0.029688720235
    1    -1            64602.07741531            0.470859763191            0.370695434900            0.029596922680
    1    -1            64603.07741531            0.470212209490            0.371523771405            0.029505342019
    1    -1            64604.07741531            0.469559962640            0.372355017812            0.029413977545
    1    -1            64605.07741531            0.468903033053            0.373189117208            0.029322828499
    1    -1            64606.07741531            0.468241430784            0.374026013461            0.029231894077
    1    -1            64607.07741531            0.467575165542            0.374865651213            0.029141173432
    1    -1            64608.07741531            0.466904246692            0.375707975860            0.029050665671
    1    -1            64609.07741531            0.466228683262            0.376552933545            0.028960369864
    1    -1            64610.07741531            0.465548483947            0.377400471140            0.028870285038
    1    -1            64611.07741531            0.464863657117            0.378250536234            0.028780410187
    1    -1            64612.07741531            0.464174210820            0.379103077121            0.028690744265
    1    -1            64613.07741531            0.463480152789            0.379958042787            0.028601286196
    1    -1            64614.07741531            0.462781490444            0.380815382896            0.028512034868
    1    -1            64615.07741531            0.462078230899            0.381675047779            0.028422989140
    1    -1            64616.07741531            0.461370380970            0.382536988421            0.028334147840
    1    -1            64617.07741531            0.460657947171            0.383401156448            0.028245509770
    1    -1            64618.07741531            0.459940935728            0.384267504119            0.028157073701
    1    -1            64619.07741531            0.459219352577            0.385135984310            0.028068838382
    1    -1            64620.07741531            0.458493203372            0.386006550502            0.027980802535
    1    -1            64621.07741531            0.457762493488            0.386879156776            0.027892964860
    1    -1            64622.07741531            0.457027228022            0.387753757792            0.027805324034
    1    -1            64623.07741531            0.456287411805            0.388630308787            0.027717878714
    1    -1            64624.07741531            0.455543049399            0.389508765558            0.027630627536
    1    -1            64625.07741531            0.454794145101            0.390389084455            0.027543569116
    1    -1            64626.07741531            0.454040702953            0.391271222369            0.027456702054
    1    -1            64627.07741531            0.453282726739            0.392155136720            0.027370024931
    1    -1            64628.07741531            0.452520219991            0.393040785448            0.027283536313
    1    -1            64629.07741531            0.451753185995            0.393928127004            0.027197234750
    1    -1            64630.07741531            0.450981627791            0.394817120340            0.027111118778
    1    -1            64631.07741531            0.450205548179            0.395707724894            0.027025186918
    1    -1            64632.07741531            0.449424949720            0.396599900589            0.026939437679
    1    -1            64633.07741531            0.448639834740            0.397493607816            0.026853869557
    1    -1            64634.07741531            0.447850205336            0.398388807427            0.026768481039
    1    -1            64635.07741531            0.447056063375            0.399285460729            0.026683270597
    1    -1            64636.07741531            0.446257410501            0.400183529468            0.026598236697
    1    -1            64637.07741531            0.445454248134            0.401082975826            0.026513377793
    1    -1            64638.07741531            0.444646577475            0.401983762410            0.026428692331
    1    -1            64639.07741531            0.443834399511            0.402885852242            0.026344178748
    1    -1            64640.07741531            0.443017715014            0.403789208752            0.026259835474
    1    -1            64641.07741531            0.442196524547            0.404693795769            0.026175660932
    1    -1            64642.07741531            0.441370828463            0.405599577511            0.026091653537
    1    -1            64643.07741531            0.440540626913            0.406506518582            0.026007811701
    1    -1            64644.07741531            0.439705919844            0.407414583956            0.025924133826
    1    -1            64645.07741531            0.438866707002            0.408323738974            0.025840618313
    1    -1            64646.07741531            0.438022987940            0.409233949337            0.025757263555
    1    -1            64647.07741531            0.437174762012            0.410145181095            0.025674067943
    1    -1            64648.07741531            0.436322028382            0.411057400638            0.025591029863
    1    -1            64649.07741531            0.435464786023            0.411970574696            0.025508147698
    1    -1            64650.07741531            0.434603033722            0.412884670321            0.025425419828
    1    -1            64651.07741531            0.433736770080            0.413799654889            0.025342844630
    1    -1            64652.07741531            0.432865993515            0.414715496088            0.025260420478
    1    -1            64653.07741531            0.431990702265            0.415632161909            0.025178145745
    1    -1            64654.07741531            0.431110894390            0.416549620644            0.025096018804
    1    -1            64655.07741531            0.430226567772            0.417467840875            0.025014038022
    1    -1            64656.07741531            0.429337720120            0.418386791470            0.024932201769
    1    -1            64657.07741531            0.428444348972            0.419306441574            0.024850508414
    1    -1            64658.07741531            0.427546451696            0.420226760601            0.024768956323
    1    -1            64659.07741531            0.426644025489            0.421147718232            0.024687543863
    1    -1            64660.07741531            0.425737067387            0.422069284406            0.024606269403
    1    -1            64661.07741531            0.424825574258            0.422991429311            0.024525131309
    1    -1            64662.07741531            0.423909542811            0.423914123381            0.024444127951
    1    -1            64663.07741531            0.422988969594            0.424837337291            0.024363257695
    1    -1            64664.07741531            0.422063850996            0.425761041945            0.024282518914
    1    -1            64665.07741531            0.421134183251            0.426685208475            0.024201909977
    1    -1            64666.07741531            0.420199962438            0.427609808234            0.024121429257
    1    -1            64667.07741531            0.419261184484            0.428534812789            0.024041075128
    1    -1            64668.07741531            0.418317845164            0.429460193915            0.023960845966
    1    -1            64669.07741531            0.417369940107            0.430385923591            0.023880740148
    1    -1            64670.07741531            0.416417464791            0.431311973991            0.023800756054
    1    -1            64671.07741531            0.415460414552            0.432238317482            0.023720892066
    1    -1            64672.07741531            0.414498784579            0.433164926618            0.023641146568
    1    -1            64673.07741531            0.413532569921            0.434091774129            0.023561517948
    1    -1            64674.07741531            0.412561765487            0.435018832924            0.023482004594
    1    -1            64675.07741531            0.411586366045            0.435946076080            0.023402604899
    1    -1            64676.07741531            0.410606366230            0.436873476837            0.023323317258
    1    -1            64677.07741531            0.409621760536            0.437801008596            0.023244140070
    1    -1            64678.07741531            0.408632543329            0.438728644909            0.023165071735
    1    -1            64679.07741531            0.407638708839            0.439656359480            0.023086110660
    1    -1            64680.07741531            0.406640251166            0.440584126152            0.023007255252
    1    -1            64681.07741531            0.405637164282            0.441511918911            0.022928503922
    1    -1            64682.07741531            0.404629442032            0.442439711874            0.022849855086
    1    -1            64683.07741531            0.403617078134            0.443367479287            0.022771307162
    1    -1            64684.07741531            0.402600066181            0.444295195519            0.022692858573
    1    -1            64685.07741531            0.401578399645            0.445222835059            0.022614507746
    1    -1            64686.07741531            0.400552071875            0.446150372511            0.022536253111
    1    -1            64687.07741531            0.399521076104            0.447077782587            0.022458093102
    1    -1            64688.07741531            0.398485405441            0.448005040105            0.022380026157
    1    -1            64689.07741531            0.397445052883            0.448932119983            0.022302050719
    1    -1            64690.07741531            0.396400011311            0.449858997234            0.022224165234
    1    -1            64691.07741531            0.395350273491            0.450785646964            0.022146368154
    1    -1            64692.07741531            0.394295832077            0.451712044364            0.022068657933
    1    -1            64693.07741531            0.393236679614            0.452638164710            0.021991033030
    1    -1            64694.07741531            0.392172808537            0.453563983355            0.021913491910
    1    -1            64695.07741531            0.391104211172            0.454489475725            0.021836033041
    1    -1            64696.07741531            0.390030879741            0.455414617317            0.021758654895
    1    -1            64697.07741531            0.388952806360            0.456339383693            0.021681355951
    1    -1            64698.07741531            0.387869983042            0.457263750476            0.021604134688
    1    -1            64699.07741531            0.386782401700            0.458187693347            0.021526989595
    1    -1            64700.07741531            0.385690054144            0.459111188039            0.021449919161
    1    -1            64701.07741531            0.384592932087            0.460034210336            0.021372921884
    1    -1            64702.07741531            0.383491027145            0.460956736064            0.021295996262
    1    -1            64703.07741531            0.382384330837            0.461878741093            0.021219140802
    1    -1            64704.07741531            0.381272834590            0.462800201329            0.021142354012
    1    -1            64705.07741531            0.380156529736            0.463721092712            0.021065634408
    1    -1            64706.07741531            0.379035407518            0.464641391209            0.020988980510
    1    -1            64707.07741531            0.377909459088            0.465561072815            0.020912390840
    1    -1            64708.07741531            0.376778675510            0.466480113547            0.020835863929
    1    -1            64709.07741531            0.375643047762            0.467398489439            0.020759398311
    1    -1            64710.07741531            0.374502566736            0.468316176539            0.020682992524
    1    -1            64711.07741531            0.373357223243            0.469233150906            0.020606645111
    1    -1            64712.07741531            0.372207008009            0.470149388608            0.020530354623
    1    -1            64713.07741531            0.371051911681            0.471064865713            0.020454119612
    1    -1            64714.07741531            0.369891924828            0.471979558290            0.020377938636
    1    -1            64715.07741531            0.368727037941            0.472893442407            0.020301810260
    1    -1            64716.07741531            0.367557241436            0.473806494120            0.020225733052
    1    -1            64717.07741531            0.366382525655            0.474718689478            0.020149705585
    1    -1            64718.07741531            0.365202880866            0.475630004514            0.020073726438
    1    -1            64719.07741531            0.364018297270            0.476540415243            0.019997794194
    1    -1            64720.07741531            0.362828764995            0.477449897661            0.019921907442
    1    -1            64721.07741531            0.361634274104            0.478358427736            0.019846064775
    1    -1            64722.07741531            0.360434814594            0.479265981412            0.019770264792
    1    -1            64723.07741531            0.359230376397            0.480172534599            0.019694506096
    1    -1            64724.07741531            0.358020949385            0.481078063173            0.019618787296
    1    -1            64725.07741531            0.356806523368            0.481982542973            0.019543107007
    1    -1            64726.07741531            0.355587088096            0.482885949796            0.019467463846
    1    -1            64727.07741531            0.354362633264            0.483788259396            0.019391856438
    1    -1            64728.07741531            0.353133148512            0.484689447478            0.019316283411
    1    -1            64729.07741531            0.351898623425            0.485589489698            0.019240743401
    1    -1            64730.07741531            0.350659047538            0.486488361655            0.019165235045
    1    -1            64731.07741531            0.349414410334            0.487386038895            0.019089756988
    1    -1            64732.07741531            0.348164701250            0.488282496900            0.019014307881
    1    -1            64733.07741531            0.346909909678            0.489177711093            0.018938886376
    1    -1            64734.07741531            0.345650024963            0.490071656827            0.018863491135
    1    -1            64735.07741531            0.344385036410            0.490964309388            0.018788120822
    1    -1            64736.07741531            0.343114933283            0.491855643989            0.018712774107
    1    -1            64737.07741531            0.341839704808            0.492745635766            0.018637449666
    1    -1            64738.07741531            0.340559340176            0.493634259780            0.018562146178
    1    -1            64739.07741531            0.339273828542            0.494521491007            0.018486862330
    1    -1            64740.07741531            0.337983159029            0.495407304342            0.018411596812
    1    -1            64741.07741531            0.336687320731            0.496291674592            0.018336348321
    1    -1            64742.07741531            0.335386302714            0.497174576472            0.018261115557
    1    -1            64743.07741531            0.334080094018            0.498055984607            0.018185897228
    1    -1            64744.07741531            0.332768683659            0.498935873524            0.018110692044
    1    -1            64745.07741531            0.331452060632            0.499814217653            0.018035498724
    1    -1            64746.07741531            0.330130213913            0.500690991322            0.017960315990
    1    -1            64747.07741531            0.328803132461            0.501566168755            0.017885142568
    1    -1            64748.07741531            0.327470805219            0.502439724068            0.017809977193
    1    -1            64749.07741531            0.326133221121            0.503311631269            0.017734818603
    1    -1            64750.07741531            0.324790369087            0.504181864252            0.017659665540
    1    -1            64751.07741531            0.323442238033            0.505050396799            0.017584516755
    1    -1            64752.07741531            0.322088816868            0.505917202570            0.017509371002
    1    -1            64753.07741531            0.320730094497            0.506782255107            0.017434227041
    1    -1            64754.07741531            0.319366059829            0.507645527829            0.017359083637
    1    -1            64755.07741531            0.317996701770            0.508506994029            0.017283939560
    1    -1            64756.07741531            0.316622009236            0.509366626872            0.017208793588
    1    -1            64757.07741531            0.315241971146            0.510224399391            0.017133644502
    1    -1            64758.07741531            0.313856576432            0.511080284488            0.017058491089
    1    -1            64759.07741531            0.312465814039            0.511934254926            0.016983332142
    1    -1            64760.07741531            0.311069672925            0.512786283332            0.016908166459
    1    -1            64761.07741531            0.309668142068            0.513636342191            0.016832992846
    1    -1            64762.07741531            0.308261210468            0.514484403847            0.016757810110
    1    -1            64763.07741531            0.306848867146            0.515330440493            0.016682617069
    1    -1            64764.07741531            0.305431101151            0.516174424180            0.016607412543
    1    -1            64765.07741531            0.304007901564            0.517016326805            0.016532195359
    1    -1            64766.07741531            0.302579257496            0.517856120112            0.016456964349
    1    -1            64767.07741531            0.301145158093            0.518693775691            0.016381718353
    1    -1            64768.07741531            0.299705592542            0.519529264974            0.016306456214
    1    -1            64769.07741531            0.298260550071            0.520362559233            0.016231176783
    1    -1            64770.07741531            0.296810019952            0.521193629578            0.016155878916
    1    -1            64771.07741531            0.295353991506            0.522022446954            0.016080561476
    1    -1            64772.07741531            0.293892454104            0.522848982142            0.016005223329
    1    -1            64773.07741531            0.292425397174            0.523673205751            0.015929863352
    1    -1            64774.07741531            0.290952810199            0.524495088221            0.015854480424
    1    -1            64775.07741531            0.289474682726            0.525314599818            0.015779073431
    1    -1            64776.07741531            0.287991004365            0.526131710635            0.015703641267
    1    -1            64777.07741531            0.286501764793            0.526946390586            0.015628182831
    1    -1            64778.07741531            0.285006953763            0.527758609406            0.015552697028
    1    -1            64779.07741531            0.283506561098            0.528568336649            0.015477182770
    1    -1            64779.88548019            0.282290062090            0.529220807723            0.015416140823
    1    -1            64779.88548019            0.000000000000            0.000000000000            0.000000000000
    1 40239            64779.88548019    157757077.689954698086   -318045493.379263401031      3471921.774559988175           15.796718141181            9.855814321207            0.480955544880         2408.890972797003
    1 40239            64779.88548019    157757077.689954698086   -318045493.379263401031      3471921.774559988175           15.796718141181            9.855814321207            0.480955544880         2368.890972797003


Here is a sample solution that produces a score of 0, you MUST NOT copy it, it's just for understanding the problem format.