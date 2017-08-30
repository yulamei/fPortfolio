# fPortfolio

library(stockPortfolio) # Base package for retrieving returns
library(ggplot2) # Used to graph efficient frontier
library(reshape2) # Used to melt the data
library(quadprog) #Needed for solve.QP

library(Quandl)
library(quantmod)

getSymbols(c(  "SPY",  "EFA",  "IWM",  "VWO",  "LQD",  "HYG"))

SPY_W <- weeklyReturn(SPY)
names(SPY_W) <- "SPY"

EFA_W <- weeklyReturn(EFA)
names(EFA_W) <- "EFA"

IWM_W <- weeklyReturn(IWM)
names(IWM_W) <- "IWM"

VWO_W <- weeklyReturn(VWO)
names(VWO_W) <- "VWO"

LQD_W <- weeklyReturn(LQD)
names(LQD_W) <- "LQD"

HYG_W <- weeklyReturn(HYG)
names(HYG_W) <- "HYG"

returns <- merge(SPY_W,EFA_W,IWM_W,VWO_W,LQD_W,HYG_W)

returns <- na.omit(returns) # omit values with NA values

head(returns)
tail(returns)
summary(returns)

require(timeSeries)
returns = as.timeSeries(returns) 


require(fPortfolio)
# frontier 
Frontier = portfolioFrontier(returns)
Frontier
plot(Frontier)

