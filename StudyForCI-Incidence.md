
/*=========================================================================================================================
Project: Replication of "The time trend of Cognitive Impairment incidence among 
                               older Chinese people in the community:    
                            based on the CLHLS cohorts from 1998 to 2014"
Author: Guannan Li
Software: Stata 15
Date: Sep 2018 - present
=========================================================================================================================*/

/*Variables List
> C11 C12 C13 C14 C15 C16 C21A C21B C21C C31A C31B C31C 
> C31D C31E C32 C41A C41B C41C C51A C51B C52 C53A C53B C53C  *CMMSE
> 'YEAR9899' ID PROV  *Levels: wave ID Province
> A1 TRUEAGE F1  *Demographics: Gender Age Education
> RESIDENC F41  *Socioeconomic and Network: Residence MaritalStatus
> D32 D91  *Health Practice: VegeFrequency Exercice
> D11A D11B D11C D11D D11E D11F D11G   *Physical&Cognitive Activities Note: for wave1: D10.. _> D11..
> G15D1 G1 H1  *Health Codition: Stroke&cvd Visual Hearing Note: for wave1: H1A -> H1
> E1 E2 E3 E4 E5 E6  *ADL
> B21 B23 B24 B26 B27  *for deletion: blindnessG1==4 deafnessH1==4 Depression */


///////////////////////// Data Cleaning and Merging ///////////////////////////

*First Wave
use "/Users/guannan/Desktop/CLHLS/STATA 1998-2014/DS0001/36692-0001-Data.dta", clear

gen Wave = 1998
order Wave, after(ID)

ren D10A D11A
ren D10B D11B
ren D10C D11C
ren D10D D11D
ren D10E D11E
ren D10F D11F
ren D10G D11G
recode D11A D11B D11C D11D D11E D11F D11G (2=4) (3=5)

ren G17D1 G15D1
ren H1A H1

drop D91
ren D81 D91

keep Wave C11 C12 C13 C14 C15 C16 C21A C21B C21C C31A C31B C31C C31D C31E C32 C41A ///
C41B C41C C51A C51B C52 C53A C53B C53C ID PROV A1 TRUEAGE F1 RESIDENC F41 D32 D91 ///
D11A D11B D11C D11D D11E D11F D11G G15D1 G1 H1 E1 E2 E3 E4 E5 E6 B21 B23 B24 B26 B27

recode RESIDENC 2=3
label drop RESIDENC

save "/Users/guannan/Desktop/time1.dta", replace

*Second Wave
use "/Users/guannan/Desktop/CLHLS/STATA 1998-2014/DS0002/36692-0002-Data.dta", clear
gen Wave = 2000
order Wave, after(ID)
keep Wave C11 C12 C13 C14 C15 C16 C21A C21B C21C C31A C31B C31C C31D C31E C32 C41A ///
C41B C41C C51A C51B C52 C53A C53B C53C ID PROV A1 TRUEAGE F1 RESIDENC F41 D32 D91 ///
D11A D11B D11C D11D D11E D11F D11G G15D1 G1 H1 E1 E2 E3 E4 E5 E6 B21 B23 B24 B26 B27

recode D11A D11B D11C D11D D11E D11F D11G (2=4) (3=5)

save "/Users/guannan/Desktop/time2.dta", replace

*Third Wave
use "/Users/guannan/Desktop/CLHLS/STATA 1998-2014/DS0003/36692-0003-Data.dta", clear
gen Wave = 2002
order Wave, after(ID)
keep Wave C11 C12 C13 C14 C15 C16 C21A C21B C21C C31A C31B C31C C31D C31E C32 C41A ///
C41B C41C C51A C51B C52 C53A C53B C53C ID PROV A1 TRUEAGE F1 RESIDENC F41 D32 D91 ///
D11A D11B D11C D11D D11E D11F D11G G15D1 G1 H1 E1 E2 E3 E4 E5 E6 B21 B23 B24 B26 B27
save "/Users/guannan/Desktop/time3.dta", replace

*Fourth Wave
use "/Users/guannan/Desktop/CLHLS/STATA 1998-2014/DS0004/36692-0004-Data.dta", clear
gen Wave = 2005
order Wave, after(ID)
keep Wave C11 C12 C13 C14 C15 C16 C21A C21B C21C C31A C31B C31C C31D C31E C32 C41A ///
C41B C41C C51A C51B C52 C53A C53B C53C ID PROV A1 TRUEAGE F1 RESIDENC F41 D32 D91 ///
D11A D11B D11C D11D D11E D11F D11G G15D1 G1 H1 E1 E2 E3 E4 E5 E6 B21 B23 B24 B26 B27
save "/Users/guannan/Desktop/time4.dta", replace

*Fifth Wave
use "/Users/guannan/Desktop/CLHLS/STATA 1998-2014/DS0005/36692-0005-Data.dta", clear
gen Wave = 2008
order Wave, after(ID)
keep Wave C11 C12 C13 C14 C15 C16 C21A C21B C21C C31A C31B C31C C31D C31E C32 C41A ///
C41B C41C C51A C51B C52 C53A C53B C53C ID PROV A1 TRUEAGE F1 RESIDENC F41 D32 D91 ///
D11A D11B D11C D11D D11E D11F D11G G15D1 G1 H1 E1 E2 E3 E4 E5 E6 B21 B23 B24 B26 B27
save "/Users/guannan/Desktop/time5.dta", replace

*Sixth Wave
use "/Users/guannan/Desktop/CLHLS/STATA 1998-2014/DS0006/36692-0006-Data.dta", clear
gen Wave = 2011
order Wave, after(ID)
keep Wave C11 C12 C13 C14 C15 C16 C21A C21B C21C C31A C31B C31C C31D C31E C32 C41A ///
C41B C41C C51A C51B C52 C53A C53B C53C ID PROV A1 TRUEAGE F1 RESIDENC F41 D32 D91 ///
D11A D11B D11C D11D D11E D11F D11G G15D1 G1 H1 E1 E2 E3 E4 E5 E6 B21 B23 B24 B26 B27
recode G15D1 8=3
label define G15D1 3"don not know", modify
save "/Users/guannan/Desktop/time6.dta", replace

*Seventh Wave
use "/Users/guannan/Desktop/CLHLS/STATA 1998-2014/DS0007/36692-0007-Data.dta", clear
gen Wave = 2014
order Wave, after(ID)
keep Wave C11 C12 C13 C14 C15 C16 C21A C21B C21C C31A C31B C31C C31D C31E C32 C41A ///
C41B C41C C51A C51B C52 C53A C53B C53C ID PROV A1 TRUEAGE F1 RESIDENC F41 D32 D91 ///
D11A D11B D11C D11D D11E D11F D11G G15D1 G1 H1 E1 E2 E3 E4 E5 E6 B21 B23 B24 B26 B27
recode G15D1 8=3
label define G15D1 3"don not know", modify
save "/Users/guannan/Desktop/time7.dta", replace

*Append all datasets
cd "/Users/guannan/Desktop/"
use "time1.dta", clear

append using "/Users/guannan/Desktop/time2.dta" "/Users/guannan/Desktop/time3.dta" ///
"/Users/guannan/Desktop/time4.dta""/Users/guannan/Desktop/time5.dta""/Users/guannan/Desktop/time6.dta" ///
"/Users/guannan/Desktop/time7.dta"

save "/Users/guannan/Desktop/timeAll.dta", replace

///////////////////////////////////////////////////////////////////////////////////////

/// Triming & Composing Variables ///

use timeAll.dta, clear

//CMMSE

recode C11 8=0 9=.
recode C12 8=0 9=.
recode C13 8=0 9=.
recode C14 8=0 9=.
recode C15 8=0 9=.
recode C21A 8=0 9=.
recode C21B 8=0 9=.
recode C21C 8=0 9=.
recode C31A 8=0 9=.
recode C31B 8=0 9=.
recode C31C 8=0 9=.
recode C31D 8=0 9=.
recode C31E 8=0 9=.
recode C32 8=0 9=.
recode C41B 8=0 9=.
recode C41A 8=0 9=.
recode C41C 8=0 9=.
recode C51A 8=0 9=.
recode C51B 8=0 9=.
recode C52 8=0 9=.
recode C53A 8=0 9=.
recode C53B 8=0 9=.
recode C53C 8=0 9=.
recode C16 (7/85=7) (88=0) (90 91 96=7) (99=.), copyrest

//gen CMMSEreal = C11 + C12 + C13 + C14 + C15 + C16 + C21A + C21B + C21C + C31A + C31B ///
+ C31C + C31D + C31E + C32 + C41B + C41A + C41C + C51A + C51B + C52 + C53A + C53B + C53C
//recode CMMSEreal 0/17=1 18/30=0, gen(CMMSEbi)
//label define CMMSEbi 1"onset CI" 0"no CI"

///////////////////// Multiple Imputation (of C32) and CMMSEbi producing ///////////////////////

//mi misstable sum, all
*misstable sum C32, gen(miss_C32)
*logit miss_C32 C11 C12 C13 C14 C15 C16 C21A C21B C21C C31A C31B C31C C31D C31E ///
C41B C41A C41C C51A C51B C52 C53A C53B C53C

mi set mlong

mi register imputed C32
mi register regular C11 C12 C13 C14 C15 C16 C21A C21B C21C C31A C31B C31C C31D C31E ///
C41B C41A C41C C51A C51B C52 C53A C53B C53C Wave A1 Age6 F1 Residence F41 D32 D91 PhyAct CogAct G15D1 G1 H1 ADL                                   
/*mi misstable patterns
mi misstable nested*/
mi impute chained (regress) C32 = C11 C12 C13 C14 C15 C16 C21A C21B C21C C31A C31B ///
C31C C31D C31E C41B C41A C41C C51A C51B C52 C53A C53B C53C Wave A1 Age6 F1 Residence ///
F41 D32 D91 PhyAct CogAct G15D1 G1 H1 ADL, add(5) rseed(1234) force       
                            
mi xeq: gen CMMSEreal = C11 + C12 + C13 + C14 + C15 + C16 + C21A + C21B + C21C + ///
C31A + C31B + C31C + C31D + C31E + C32 + C41B + C41A + C41C + C51A + C51B + C52 + C53A + C53B + C53C
mi xeq: recode CMMSEreal 0/17=1 18/30=0, gen(CMMSEbi)
mi xeq: label define CMMSEbi 1"onset CI" 0"no CI"

*mi describe

/*findit midiagplots
midiagplots C32, m(1/5) combine*/


//////////////////////////////////////////// Covariates ///////////////////////////////////////

recode Wave 1998 1999=0 2000=1 2002=2 2005=3 2008 2009=4 2011 2012=5 2014=6
label define Wave 0 "1998" 1 "2000" 2"2002" 3"2005" 4"2008-2009" 5"2011-2012" 6"2014"

label define PROV 46"hainan", add

*Gender
recode A1 1=0 2=1
label drop A1
label define A1 0"male" 1"female"

*Age
recode TRUEAGE 39/59=-1 60/69=0 70/79=1 80/89=2 90/99=3 100/105=4 106/124=5, gen(Age6)
label define Age6 -1"59 or younger" 0"60-69" 1"70-79" 2"80-89" 3"90=99" 4"100-105" 5"106 or oler"

*Education
recode F1 (7/26=0) (1/6=1) (0=2) (88 99=.)
label drop F1
label define F1 0"7+ years" 1"1-6 years" 2"0 years"

*Residence
label drop RESIDENC
ren RESIDENC Residence
recode Residence (1 2=0) (3=1)
label define Residence 0"urban(city and town)" 1"rural"

*Marital Status
label drop F41
recode F41 8 9=. 1=0 2/5=1
label define F41 0"married" 1"other"

*VegetableFrequency
label drop D32
recode D32 8 9=. 1 2=0 3 4=1
label define D32 0"often" 1"seldom"

*Exercise
recode D91 1=0 2=1 8 9="."
label define D91 0"yes" 1"no", modify


*PhysicalActivities & *CongnitiveActivities
//higher score less active

recode D11A D11B D11C D11D D11E D11F D11G (1=0) (2=1) (3=2) (4=3) (5=4) (8 9=.)

label define D11A 0"almost everyday" 1"not daily but once a week" ///
2"not weekly but at least once amonth" 3"sometimes" 4"never"
label define D11B 0"almost everyday" 1"not daily but once a week" ///
2"not weekly but at least once amonth" 3"sometimes" 4"never"
label define D11C 0"almost everyday" 1"not daily but once a week" ///
2"not weekly but at least once amonth" 3"sometimes" 4"never"
label define D11D 0"almost everyday" 1"not daily but once a week" ///
2"not weekly but at least once amonth" 3"sometimes" 4"never"
label define D11E 0"almost everyday" 1"not daily but once a week" ///
2"not weekly but at least once amonth" 3"sometimes" 4"never"
label define D11F 0"almost everyday" 1"not daily but once a week" ///
2"not weekly but at least once amonth" 3"sometimes" 4"never"
label define D11G 0"almost everyday" 1"not daily but once a week" ///
2"not weekly but at least once amonth" 3"sometimes" 4"never"

gen PhyAct = D11A + D11B + D11C + D11E
gen CogAct = D11D + D11F + D11G

//PhysicalActivities 0/10 = 0 /*"more"*/ 11/16 =1 /*less*/, mean = 10.01 higher score less activities
//CongnitiveActivities 0/8 = 0 9/12 =1, mean = 8.37 higher score less activities

recode PhyAct 0/10=0 11/16=1
recode CogAct 0/8=0 9/12=1
la define PhyAct 0"more" 1"less"
la define CogAct 0"more" 1"less"


*Stroke
recode G15D1 (0 8 9=.) (2=0)
label define G15D1 0"No" 1"Yes", replace

*VisualFunction
recode G1 8 9="."

*HearingFunction
recode H1 8 9="."

*ADL
recode E1 8 9=. 1=0
recode E2 9=. 1=0
recode E3 8 9=. 1=0
recode E4 9=. 1=0
recode E5 9=. 1=0
recode E6 9=. 1=0
gen ADL = E1 + E2 + E3 + E4 + E5 + E6
recode ADL 2/18=1
label define ADL 0"no ADL" 1"ADL"

*Depression
recode B21 B27 (5=4) (4=3) (3=2) (2=1) (1=0) (8 9=.)
recode B23 B24 B26 (5=0) (4=1) (3=2) (2=3) (1=4) (8 9=.)
gen Dep = B21 + B23 + B24 + B26 + B27

/////////////////////////////////////////////////////////////////////////////////


*Exluce cases that are blind, deaf or depression AND AGE<60 AND Wave=1998
*Sum: 85905/74074 respondents

drop if G1 ==4 //456 Blind
drop if H1 ==4 //4425 Deaf
drop if Dep ==20 //8 potential Depression

drop if Age6 == -1 //154 60 years old or lesser, no obs in the first four waves
//drop if Age6 == 0 //60-69 no obs in wave1 and wave2
drop if Age6 == 5 //1105 (optional) 105 years old or more
*74772 left

/////////////////////////////////////////////////////////////////////////////////


*Incidence Rate enter total

/*ltable Wave CMMSEbi, noadjust
ltable Wave CMMSEbi, hazard noadjust

stset Wave, failure(CMMSEbi==1) id(ID)
stvary
stptime, per(1000) at(0(1)6) by(A1) //by Gender
stptime, per(1000) at(0(1)6) //Total*/


*Incidence Wave by Wave

clonevar Wave01 = Wave if Wave==0|Wave==1
stset Wave01, failure(CMMSEbi==1) id(ID)
stptime, per(1000) by(A1) //Wave01

clonevar Wave12 = Wave if Wave==1|Wave==2
stset Wave12, failure(CMMSEbi==1) id(ID)
stptime, per(1000) by(A1) //Wave12

clonevar Wave23 = Wave if Wave==2|Wave==3
stset Wave23, failure(CMMSEbi==1) id(ID)
stptime, per(1000) by(A1) //Wave23

clonevar Wave34 = Wave if Wave==3|Wave==4
stset Wave34, failure(CMMSEbi==1) id(ID)
stptime, per(1000) by(A1) //Wave34

clonevar Wave45 = Wave if Wave==4|Wave==5
stset Wave45, failure(CMMSEbi==1) id(ID)
stptime, per(1000) by(A1) //Wave45

clonevar Wave56 = Wave if Wave==5|Wave==6
stset Wave56, failure(CMMSEbi==1) id(ID)
stptime, per(1000) by(A1) //Wave56

* Longitudianl Poisson

//drop if Wave==0 //8118

xtset ID PROV

xtpoisson CMMSEbi i.Wave i.Gender i.AgeGroups i.EducationalGroups 
i.Residence i.MaritalStatus i.VegetableFrequency i.Exercise i.PhyAct i.CogAct i.G15D1 i.G1 i.H1 i.ADL, normal irr


*Two-level Poisson Model

xtset ID Wave

xtpoisson CMMSEbi i.Wave i.A1 i.Age6 i.F1 i.Residence i.F41 i.D32 i.D91 i.PhyAct ///
i.CogAct i.G15D1 i.G1 i.H1 i.ADL, normal irr

xtpoisson CMMSEbi i.Wave i.A1 i.Age6 i.F1 i.Residence i.F41 i.D32 i.D91 i.PhyAct i.CogAct, normal irr

xtpoisson CMMSEbi i.Wave i.A1 i.Age6 i.F1 i.Residence i.F41, normal irr

xtpoisson CMMSEbi i.Wave i.A1 i.Age6 i.F1, normal irr

xtpoisson CMMSEbi i.Wave i.A1 i.Age6, normal irr

xtpoisson CMMSEbi i.Wave, normal irr

mi estimate: xtpoisson CMMSEbi i.Wave i.A1 i.Age6 i.F1 i.Residence i.F41 i.D32 i.D91 i.PhyAct i.CogAct i.G15D1 i.G1 i.H1 i.ADL, normal irr



//////////////////////////Graphing//////////////////////////

* Crude Incidence Rate with 95% CI

import delimited /Users/guannan/Desktop/incidencewithCI.csv, clear

label define gender 1"Male" 2"Total" 0"Female"
recode wave 2000=1 2002=2 2005=3 2008=4 2011=5 2014=6
label define wave 1"2000" 2"2002" 3"2003" 4"2008" 5"2011" 6"2014"

twoway ///
(connected incidence wave if gender==0, lcolor(black) lwidth(thin) lpattern(solid) msize(tiny)) ///
(connected incidence wave if gender==1, lcolor(black)lwidth(thin) lpattern(shortdash) msize(tiny)) ///
(connected incidence wave if gender==2, lcolor(black)lwidth(thin) lpattern(dot) msize(tiny)) ///
(rcap upper lower wave, vertical lcolor(black) lwidth(vthin)) ///
, ytitle("incidence of CI") xtitle("gender by waves") ytick(0(10)250) scheme(s1color) ///
title("Crude CI Incidence with 95% Confidence Interval") subtitle("by Gender") caption("Data Source: CHLHS") ///
legend (label(1 "Female") label(2 "Male") label(3 "Total") order(1 2 3) ring(0) pos(2)) 
///
ylabel( ,grid glwidth(thin) glcolor(gs1)) xlabel( ,grid glwidth(thin) glcolor(gs2))

graph set window fontface "Times New Roman"

anova incidence i.wave i.gender


exit,clear     
