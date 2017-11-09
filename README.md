# meta-analysis-code
R code for meta-analysis study published in biology letters by Nianxun et al. 2017


##statistics

library(metafor)

data=read.csv("...../data.csv")

es=escalc(data=data,measure="ROM",m1i=Xe,sd1i=SDe,n1i=Ne,m2i=Xc,sd2i=SDc,n2i=Nc,append=T)

res=rma.mv(yi, vi, mods = ~ log(Richness), random = ~ 1| study, struct="HAR", data=es)



##publication bias

library(metafor)

data <- read.csv("...../data.csv")

es=escalc(data=data,measure="ROM",m1i=Xe,sd1i=SDe,n1i=Ne,m2i=Xc,sd2i=SDc,n2i=Nc,append=T)

random=rma(yi,vi,data=es,method="REML")

regtest(random)

res=trimfill(random,estimator="R0")

res

funnel(res,xlab="Response Ratio")

fsn(yi, vi, data=es,type="Rosenthal",alpha=.05, digits=4)
