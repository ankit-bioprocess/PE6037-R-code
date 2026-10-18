# PE6037-R-code
R code for PE6037 Experimental Design and Data Analysis in Bioprocess Engineering (UCC): hypothesis testing with one-way ANOVA and Tukey’s HSD test.
  rm(list=ls())
  install.packages("readxl")
  library(readxl)
  data <- read_excel("/Users/ankitthakor/Downloads/Thakor, Ankitkumar Ramjibhai_aov_data.xlsx")
  data$group <- as.factor(data$group)
  table(data$group)
  aggregate(measurement ~ group, data = data, FUN = mean)
  model <- aov(measurement ~ group, data = data)
  summary(model)
  shapiro.test(residuals(model))
  bartlett.test(measurement ~ group, data = data)
  tukey <- TukeyHSD(model)
  print(tukey)
  graphics.off
  dev.new(width=8,height=6)
  par(mar = c(5, 10, 4, 2))
  plot(tukey, las = 1) 
  png("tukey_plot.png",width=800,height=600)
  par(mar = c(5, 10, 4, 2))
  plot(tukey, las = 1) 
  dev.off 
  getwd 
