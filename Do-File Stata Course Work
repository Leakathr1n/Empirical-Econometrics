/*1.Getting Started*/
tsset YEAR
/*2.Time Series Plots*/
twoway (tsline IU YU IO YO)
/*3.Scatter Plots*/
twoway (scatter IO YO)
/*4.Simple Regressions*/
reg IO YO
/*5.Residual Inspection*/
predict residualIO, res
twoway (scatter residualIO YO)
hist residualIO
sktest residualIO
/*6.Log-Log Specification*/
generate lnIO = log(IO)
generate lnYO = log(YO)
twoway (tsline lnIO lnYO)
twoway (scatter lnIO lnYO)
reg lnIO lnYO
predict residuallnIO, res
twoway (tsline residuallnIO)
twoway (scatter residuallnIO lnYO)
hist residuallnIO
sktest residuallnIO
/*7.Specification in Log-Differences*/
generate dlnIO = d.lnIO
generate dlnYO = d.lnYO
twoway (tsline dlnIO dlnYO)
twoway (scatter dlnIO dlnYO)
reg dlnIO dlnYO
predict residualdlnIO, res
twoway (tsline residualdlnIO)
twoway (scatter residualdlnIO dlnYO)
hist residualdlnIO
sktest residualdlnIO

/*start of tutorial 2*/
/*1.Inspection of Stationarity*/
twoway (tsline lnIO lnYO)
corrgram lnIO, yw
corrgram lnYO, yw
twoway (tsline dlnIO dlnYO)
corrgram dlnIO, yw
corrgram dlnYO, yw
/*2.Autoregresssive Model for lnIO*/
generate lnIO_1 = L.lnIO
reg lnIO lnIO_1
/*3.Autoregressive Model for dlnIO*/
generate dlnIO_1 = L.dlnIO
reg dlnIO dlnIO_1
/*4.Static Model*/
reg lnIO lnYO
predict residuallnIO, res
twoway (tsline residuallnIO)
corrgram residuallnIO
/*5.Finite Distributed Lag Model*/
generate lnYO_1 = L.lnYO
reg lnIO lnYO lnYO_1
test lnYO = lnYO_1 = 0
/*6.Recap Multiple hypothesis testing*/
generate PY = YU/YO
generate PI = IU/IO
generate lnPI =log(PI)
generate lnPY=log(PY)
generate lnPI_1 = L.lnPI
reg lnIO lnYO lnPI lnPY lnPI_1 lnYO_1 
test lnPI = lnPY = lnPI_1 = 0
test (lnPI + lnPY = 0) (lnPI_1 = 0)
test (lnPI+lnPY+lnPI_1=0)
test (lnPI_1=lnYO_1=0) (lnPI = -1) (lnYO = lnPY)
/*7.ARDL MOdel*/
reg lnIO lnYO lnYO_1 lnIO_1 

/*start of tutorial 3*/
/*1.Visual Inspection of Stationary*/
twoway (tsline lnIO lnYO)
twoway (tsline dlnIO dlnYO)
/*2.Visual INspection of Trends*/
generate t=YEAR-1949
reg lnIO t
predict residuallnIOtrend, res
twoway (tsline residuallnIOtrend)
reg lnYO t
predict residuallnYOtrend, res
twoway (tsline residuallnYOtrend)
/*3.Dickey-Fuller Unit Root Test*/
dfuller lnIO, trend reg
dfuller lnYO, trend reg
/*4.Augmented DF Unit Root Test*/
dfuller lnIO, lags(2) trend reg 
varsoc lnIO
dfuller lnYO, lags(2) trend reg 
varsoc lnYO
/*5. ADF Test (with constant)*/
dfuller lnIO, lags (1) reg
dfuller lnYO, lags (1) reg
/*6.Statis regression for series in log-levels (revisited) and Spurious Regression.*/
reg lnIO lnYO
/*7.Static Regression for the series in first differences and SPuriour Regression*/
reg dlnIO dlnYO
/*8.ARDL models: short-run and long-run effects*/
reg lnIO lnYO lnYO_1 lnIO_1
nl (lnIO=(({theta2=1}-{b2})/(1+{b3=0.5}))*lnYO+{b2}*lnYO_1+{b3}*lnIO_1+{b0}) if YEAR > 1950
nl (lnIO=({theta= 1}*(1-{b3= 0.5}) - {b2})*lnYO+{b2}*lnYO_1+{b3}*lnIO_1+{b0}) if YEAR > 1950

/*start of tutorial 4*/
/*1.Explaining the Set-Up*/
/*2.Cointegrationbetween investment and output with known long-run parameter*/
dfuller lnAPIO, lags (2) reg
generate lnAPIO = lnIO - lnYO
twoway (tsline lnAPIO)
/*1.Cointegration between investment and output with estimated long-run parameter*/
reg lnIO lnYO
predict residuallnIO, res
twoway (tsline residuallnIO)
dfuller residuallnIO, lags(2) reg
/*4.Back to the ARDL Model*/
reg lnIO lnYO lnYO_1 lnIO_1
/*5.Two Distributed Lag Model*/
reg lnIO lnYO lnYO_1
nl (lnIO=(({theta2=1}-{b2})/(1))*lnYO+{b2}*lnYO_1+{b0}) if YEAR > 1950
reg lnIO lnYO lnIO_1
nl (lnIO=(({theta2=1})/(1+{b3=0.5}))*lnYO+{b3}*lnIO_1+{b0}) if YEAR > 1950
/*6. Partial Adjustment Model*/
reg lnIO lnYO lnIO_1
nl (lnIO=(({theta2=1})/(1+{b3=0.5}))*lnYO+{b3}*lnIO_1+{b0}) if YEAR > 1950
reg lnIO lnYO lnIO_1
nl (lnIO=({theta= 1}*(1-{b3= 0.5}) )*lnYO+{b3}*lnIO_1+{b0}) if YEAR > 1950
/*7. Error Correcting Model.*/
reg lnIO lnYO
predict residuallnIO
generate residuallnIO_1=L.residuallnIO
reg dlnIO dlnYO residuallnIO_1
/*8. Error Correcting Model.*/
reg lnIO lnYO lnYO_1 lnIO_1
test (lnYO+lnYO_1+lnIO_1=1)
generate lnAPIO_1 = L.lnAPIO
reg dlnIO dlnYO lnAPIO_1
nlcom (_b[dlnYO]+_b[dlnYO]*_b[lnAPIO_1] -_b[lnAPIO])
reg lnIO lnYO lnYO_1 lnIO_1
test (lnYO_1 + lnYO = 0) (lnIO_1=1)
/*9. Model in growth Rates */
reg dlnIO dlnYO
reg lnIO lnYO lnYO_1 lnIO_1
test lnYO_1 = lnIO_1 = 0
/*10. Static Model*/
reg lnIO lnYO
generate APIO = IO/YO

/*start of tutorial 5*/
/*1. Testing for structural breaks*/
reg lnIO lnYO lnYO_1
estat sbsingle
reg lnIO lnYO lnYO_1 if YEAR < 1982
reg lnIO lnYO lnYO_1 if YEAR > 1981
reg lnIO lnYO lnYO_1
estat sbknown, break(1982)
gen dummy = (YEAR > 1981)
gen lnYOxdummy = lnYO*dummy
gen lnYO_1xdummy = lnYO_1*dummy
reg lnIO dummy lnYO lnYO_1 lnYOxdummy lnYO_1xdummy
/*2.TEsting of the distributional assumptions */
reg lnIO lnYO lnYO_1
predict residuallnIO_5, res
twoway (scatter residuallnIO_5 lnYO)
twoway (scatter residuallnIO_5 lnYO_1)
reg lnIO lnYO lnYO_1
estat imtest, white
reg lnIO lnYO lnYO_1, robust
hist residuallnIO_5
reg lnIO lnYO lnYO_1
/*3. Test of the linearity of the specification */
estat ovtest
generate residuallnIO_5_1=L.residuallnIO_5
twoway (tsline residuallnIO_5)
twoway (scatter residuallnIO_5 residuallnIO_5_1)
/*4. TEstinf for autocorrelation */
reg lnIO lnYO lnYO_1
estat durbinalt
reg lnIO lnYO lnYO_1
estat bgodfrey, nomiss0 lags(2)
/*5.Autocorrelation-robust standard errors */
newey lnIO lnYO lnYO_1, lag(2)

/*start of tutorial 6*/
/*1.Obtaining stationary times series */
twoway (tsline dlnIO)
dfuller dlnIO, lags(2) drift reg
twoway (tsline dlnYO)
dfuller dlnYO, lags(2) drift reg
/*2. Estimating Var(1) */
var dlnIO dlnYO, lags(1)
var dlnIO dlnYO, lags(1)
/*3.Validating Var(1) */
predict residIO, residuals equation(dlnIO)
predict residYO, residuals equation(dlnYO)
twoway (tsline residIO)
corrgram residIO, yw
twoway (tsline residYO)
corrgram residYO, yw
xcorr residIO residYO
/*4.Selecting the order of the VAR */
varsoc dlnIO dlnYO, maxlag(10)
var dlnIO dlnYO, lags (1 2)
predict residIO2, residuals equation(dlnIO)
predict residYO2, residuals equation(dlnYO)
twoway (tsline residIO2)
corrgram residIO2, yw
twoway (tsline residYO2)
corrgram residYO2, yw
xcorr residIO2 residYO2
/*5.Granger Causality */
var dlnIO dlnYO, lags(1)
vargranger
var dlnIO dlnYO, lags (1 2)
vargranger
/*6. Impulse Repsonse functions in VARs*/
irf create shock_dnIO, set(shock_dlnIO) step(10)
irf graph irf, impulse(dlnIO) response (dlnIO dlnYO)
irf create shock_dlnYO, set (shock_dlnYO) step(10)
irf graph irf, impulse(dlnYO) response (dlnIO dlnYO)


/*paper*/
reg lnIO lnYO lnYO_1 lnIO_1
predict residpaper, res
generate residpaper_1=L.residpaper
twoway (tsline residpaper)
twoway (scatter residpaper residpaper_1)
reg residpaper residpaper_1
reg lnIO lnYO lnYO_1 lnIO_1
estat durbinalt
reg lnIO lnYO lnYO_1 lnIO_1
estat bgodfrey, nomiss0 lags(2)

/*Co-integration*/
dfuller residpaper, lags (2) reg

twoway (scatter residpaper lnYO)
twoway (scatter residpaper lnYO_1)
twoway (scatter residpaper lnIO_1)
reg lnIO lnYO lnYO_1 lnIO_1
estat imtest, white

newey lnIO lnYO lnYO_1 lnIO_1, lag (2)
estat ovtest
generate lnYO2= lnYO*lnYO
reg lnIO lnYO2 lnYO_1 lnIO_1
generate lnYO_12= lnYO_1*lnYO_1
reg lnIO lnYO lnYO_12 lnIO_1
estat ovtest

reg lnIO lnYO lnYO_12 lnIO_1
estat bgodfrey, nomiss0 lags(2)
newey lnIO lnYO lnYO_12 lnIO_1, lag(2)

reg lnIO lnYO lnYO_1 lnIO_1
estat sbsingle

/*Table with robust SE*/
reg lnIO lnYO lnYO_1 lnIO_1, vce(robust)
test(lnYO+lnYO_1+lnIO_1=1)
reg lnIO lnYO lnYO_1 lnIO_1, vce(robust)
test (lnYO_1 + lnYO = 0) (lnIO_1=1)
reg lnIO lnYO lnYO_1 lnIO_1, vce(robust)
test lnYO_1 = lnIO_1 = 0
reg lnIO lnYO lnYO_1 lnIO_1, vce(robust)
estat sbsingle
reg lnIO lnYO lnYO_1 lnIO_1, vce(robust)
estat ovtest
reg lnIO lnYO lnYO_1 lnIO_1, vce(robust),if YEAR < 2004
reg lnIO lnYO lnYO_1 lnIO_1, vce(robust),if YEAR > 2003
reg lnIO lnYO lnYO_1 lnIO_1, vce(robust),if YEAR < 2004
nl (lnIO=(({theta2=1}-{b2})/(1+{b3=0.5}))*lnYO+{b2}*lnYO_1+{b3}*lnIO_1+{b0}) if YEAR > 1950
reg lnIO lnYO lnYO_1 lnIO_1, vce(robust),if YEAR < 2004
nl (lnIO=({theta= 1}*(1-{b3= 0.5}) - {b2})*lnYO+{b2}*lnYO_1+{b3}*lnIO_1+{b0}) if YEAR > 1950
reg lnIO lnYO lnYO_1 lnIO_1, vce(robust),if YEAR > 2003
nl (lnIO=(({theta2=1}-{b2})/(1+{b3=0.5}))*lnYO+{b2}*lnYO_1+{b3}*lnIO_1+{b0}) if YEAR > 1950
reg lnIO lnYO lnYO_1 lnIO_1, vce(robust),if YEAR > 2003
nl (lnIO=(({theta2=1}-{b2})/(1+{b3=0.5}))*lnYO+{b2}*lnYO_1+{b3}*lnIO_1+{b0}) if YEAR > 1950


/*VAR paper*/ 
var dlnIO dlnYO, lags(1), if YEAR < 2004
varsoc dlnIO dlnYO, maxlag(10), if YEAR < 2004
var dlnIO dlnYO, lags(1), if YEAR > 2003
varsoc dlnIO dlnYO, maxlag(10), if YEAR > 2003
var dlnIO dlnYO, lags(1),if YEAR < 2004
vargranger
var dlnIO dlnYO, lags(1),if YEAR > 2003
vargranger
irf create shock_dnIO, set(shock_dlnIO) step(10)
irf graph irf, impulse(dlnIO) response (dlnIO dlnYO), if YEAR < 2004
irf graph irf, impulse(dlnIO) response (dlnIO dlnYO), if YEAR > 2003
irf create shock_dlnYO, set (shock_dlnYO) step(10)
irf graph irf, impulse(dlnYO) response (dlnIO dlnYO), if YEAR < 2004
irf graph irf, impulse(dlnYO) response (dlnIO dlnYO), if YEAR > 2003


/* Table*/
/*4.Back to the ARDL Model*/
generate lnCO_1 =L.lnCO
reg lnCO lnYO lnYO_1 lnCO_1
/*5.Two Distributed Lag Model*/
reg lnCO lnYO lnYO_1
nl (lnCO=(({theta2=1}-{b2})/(1))*lnYO+{b2}*lnYO_1+{b0}) if YEAR > 1950
reg lnCO lnYO lnIO_1
nl (lnCO=(({theta2=1})/(1+{b3=0.5}))*lnYO+{b3}*lnCO_1+{b0}) if YEAR > 1950
/*6. Partial Adjustment Model*/
reg lnCO lnYO lnCO_1
nl (lnCO=(({theta2=1})/(1+{b3=0.5}))*lnYO+{b3}*lnIO_1+{b0}) if YEAR > 1950
reg lnCO lnYO lnCO_1
nl (lnCO=({theta= 1}*(1-{b3= 0.5}) )*lnYO+{b3}*lnIO_1+{b0}) if YEAR > 1950
/*8. Error Correcting Model.*/
reg lnCO lnYO lnYO_1 lnCO_1
test (lnYO+lnYO_1+lnCO_1=1)
generate lndiffpaper = lnCO - lnYO
generate lndiffpaper_1 = L.lndiffpaper
reg dlnCO dlnYO lndiffpaper_1
nlcom (_b[dlnYO]+_b[dlnYO]*_b[lndiffpaper_1] -_b[lndiffpaper])



/*9. Model in growth Rates */
reg lnCO lnYO lnYO_1 lnCO_1
test (lnYO_1 + lnYO = 0) (lnCO_1=1)
reg dlnCO dlnYO
/*10. Static Model*/
reg lnCO lnYO lnYO_1 lnCO_1
test lnYO_1 = lnCO_1 = 0
reg lnCO lnYO
generate APIO = IO/YO


reg lnCO lnYO lnYO_1 lnCO_1
estat bgodfrey, nomiss0 lags(2)
newey lnCO lnYO lnYO_1 lnCO_1, lag(2)
newey lnCO lnYO lnYO_1 lnCO_1, lag(2)
test (lnYO+lnYO_1+lnCO_1=1)
newey lnCO lnYO lnYO_1 lnCO_1, lag(2)
test (lnYO_1 + lnYO = 0) (lnCO_1=1)
newey lnCO lnYO lnYO_1 lnCO_1, lag(2)
test lnYO_1 = lnCO_1 = 0

/*test for stationary I(1)*/
generate dlnKO = D.lnKO
dfuller dlnKO, lags (2) reg
twoway (tsline dlnKO)
generate ddlnKO=D.dlnKO
dfuller ddlnKO, lags (2) reg
dfuller ddlnKO, lags (2) trend reg

/*include capital stock in the model*/
twoway (tsline YO IO KO)
twoway (tsline KO)
generate lnKO= log(KO)
generate lnKO_1=L.lnKO
predict residpaperKO, res
generate residpaperKO_1 = L.residpaperKO
reg residpaperKO residpaperKO_1
twoway (tsline residpaperKO)
twoway (scatter residpaperKO residpaperKO_1)
reg lnIO lnYO lnYO_1 lnIO_1 lnKO lnKO_1
estat durbinalt
reg lnIO lnYO lnYO_1 lnIO_1 lnKO lnKO_1
estat bgodfrey, nomiss0 lags(2)
/* dlnKO is not stationary --> not important though*/
/* serial coorelation, so add more lags*/
generate lnKO_2=L.lnKO_1
reg lnIO lnYO lnYO_1 lnIO_1 lnKO lnKO_1 lnKO_2
estat durbinalt
reg lnIO lnYO lnYO_1 lnIO_1 lnKO lnKO_1 lnKO_2
estat bgodfrey, nomiss0 lags(2)
/* test homoskedasticity*/
reg lnIO lnYO lnYO_1 lnIO_1 lnKO lnKO_1 lnKO_2
estat imtest, white
reg lnIO lnYO lnYO_1 lnIO_1 lnKO lnKO_1 lnKO_2, robust
/*test for proper specification*/
reg lnIO lnYO lnYO_1 lnIO_1
estat ovtest
reg lnIO lnYO lnYO_1 lnIO_1 lnKO lnKO_1 lnKO_2, robust
estat ovtest
reg lnIO lnYO lnYO_1 lnYO_2 lnIO_1 lnKO lnKO_1, robust
estat ovtest
reg lnIO lnYO lnYO_1 lnYO_2 lnIO_1 lnIO_2 lnKO lnKO_1 lnKO_2, robust
estat ovtest
/* test for breaks*/
reg lnIO lnYO lnYO_1 lnIO_1 lnKO lnKO_1 lnKO_2, robust
estat sbsingle /*break at 1969*/ 
reg lnIO lnYO lnYO_1 lnIO_1 lnKO lnKO_1 lnKO_2, robust, if YEAR < 1969
reg lnIO lnYO lnYO_1 lnIO_1 lnKO lnKO_1 lnKO_2, robust, if YEAR > 1968
reg lnIO lnYO lnYO_1 lnIO_1 lnKO lnKO_1 lnKO_2, robust
estat sbknown, break (1995)
reg lnIO lnYO lnYO_1 lnIO_1 lnKO lnKO_1 lnKO_2, robust
estat sbknown, break (2008)
reg lnIO lnYO lnYO_1 lnIO_1 lnKO lnKO_1 lnKO_2, robust
estat sbknown, break (2013)

/*get elasticities and SE*/
reg lnIO lnYO lnYO_1 lnIO_1 lnKO lnKO_1 lnKO_2, robust
nlcom (_b[lnYO]+_b[lnYO_1]+_b[lnYO]*_b[lnIO_1])
reg lnIO lnYO lnYO_1 lnIO_1 lnKO lnKO_1 lnKO_2, robust
nlcom ((_b[lnYO]+_b[lnYO_1])/(1-_b[lnIO_1]))
reg lnIO lnYO lnYO_1 lnIO_1 lnKO lnKO_1 lnKO_2, robust
nlcom (_b[lnKO]+_b[lnKO_1]+_b[lnKO]*_b[lnIO_1])
reg lnIO lnYO lnYO_1 lnIO_1 lnKO lnKO_1 lnKO_2, robust
nlcom ((_b[lnKO]+_b[lnKO_1]+_b[lnKO_2])/(1-_b[lnIO_1]))
reg lnIO lnYO lnYO_1 lnIO_1 lnKO lnKO_1 lnKO_2, robust, if YEAR < 1969
nlcom (_b[lnYO]+_b[lnYO_1]+_b[lnYO]*_b[lnIO_1])
reg lnIO lnYO lnYO_1 lnIO_1 lnKO lnKO_1 lnKO_2, robust, if YEAR < 1969
nlcom ((_b[lnYO]+_b[lnYO_1])/(1-_b[lnIO_1]))
reg lnIO lnYO lnYO_1 lnIO_1 lnKO lnKO_1 lnKO_2, robust, if YEAR < 1969
nlcom (_b[lnKO]+_b[lnKO_1]+_b[lnKO]*_b[lnIO_1])
reg lnIO lnYO lnYO_1 lnIO_1 lnKO lnKO_1 lnKO_2, robust, if YEAR < 1969
nlcom ((_b[lnKO]+_b[lnKO_1]+_b[lnKO_2])/(1-_b[lnIO_1]))
reg lnIO lnYO lnYO_1 lnIO_1 lnKO lnKO_1 lnKO_2, robust, if YEAR > 1968
nlcom (_b[lnYO]+_b[lnYO_1]+_b[lnYO]*_b[lnIO_1])
reg lnIO lnYO lnYO_1 lnIO_1 lnKO lnKO_1 lnKO_2, robust, if YEAR > 1968
nlcom ((_b[lnYO]+_b[lnYO_1])/(1-_b[lnIO_1]))
reg lnIO lnYO lnYO_1 lnIO_1 lnKO lnKO_1 lnKO_2, robust, if YEAR > 1968
nlcom (_b[lnKO]+_b[lnKO_1]+_b[lnKO]*_b[lnIO_1])
reg lnIO lnYO lnYO_1 lnIO_1 lnKO lnKO_1 lnKO_2, robust, if YEAR > 1968
nlcom ((_b[lnKO]+_b[lnKO_1]+_b[lnKO_2])/(1-_b[lnIO_1]))

/*VAR*/
generate dlnKO = D.lnKO
twoway (tsline dlnKO dlnIO dlnYO)
dfuller dlnKO, lags (2) reg
twoway (tsline dlnKO)
generate ddlnKO=D.dlnKO
dfuller ddlnKO, lags (2) reg
dfuller ddlnKO, lags (2) trend reg

