# Getting-and-Cleaning-Data
================================================================================================

Question 1

================================================================================================

# Getting and Cleaning Data
# Coursera
# John Hopkins University

# Raghabandan 
# ragharaam@gmail.com

# Downloading the file from the URL

fileUrl<- "https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06hid.csv"
download.file(fileUrl, destfile= "E:/Ragha/Work/data/AmericanCommunitySurvey.csv")
list.files("./data")


# Reading the data

AmericaData<- read.csv("./data/AmericanCommunitySurvey.csv")
head(AmericaData)


# Tabulate the value variable (VAL)

table(AmericaData$VAL)

# Extracting the value of code 24 (1,000,000+)

table(AmericaData$VAL)[[24]]


or 

sum(!is.na(AmericaData$VAL[AmericaData$VAL==24]))

================================================================================================

Question 2

================================================================================================

AmericaData$FES


================================================================================================

Question 3

================================================================================================


# Download the file from the URL

fileUrl<- "https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2FDATA.gov_NGAP.xlsx"
download.file(fileUrl, destfile= "E:/Ragha/Work/data/NGAprogram.xlsx")
list.files("./data")


# Read the data

NGAprogram<- read.xlsx("./data/NGAprogram.xlsx", sheetIndex= 1, header= TRUE)
head(NGAprogram)

# load the package to read xlsx files

library(xlsx)

# Specify the rows and columns to import

colIndex= 7:15
rowIndex= 18:23

# Read the susbset xlsx file

dat <- read.xlsx("./data/NGAprogram.xlsx", sheetIndex= 1,  colIndex=colIndex, rowIndex=rowIndex)

# Perform the required test

sum(dat$Zip*dat$Ext,na.rm=T)



================================================================================================

Question 4

================================================================================================


# Downloading the file from the URL

fileUrl <- "http://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Frestaurants.xml"

# Reading the data
Restaurant <- xmlTreeParse(fileUrl, useInternal=TRUE)
rootNode <- xmlRoot(doc)

# Extracting the value 

sum(xpathSApply(rootNode, "//zipcode", xmlValue)==21231)


================================================================================================

Question 5

================================================================================================


# Downloading the file from the URL

fileUrl <- "https://d396qusza40orc.cloudfront.net/getdata%2Fdata%2Fss06pid.csv"

download.file(fileUrl, destfile="./data/microdata3.csv")

# Reading the data

DT <- fread("./data/microdata3.csv")

file.info("./data/microdata3.csv")$size

# Check process time

system.time(DT[,mean(pwgtp15),by=SEX])
system.time(mean(DT[DT$SEX==1,]$pwgtp15))+system.time(mean(DT[DT$SEX==2,]$pwgtp15))
system.time(sapply(split(DT$pwgtp15,DT$SEX),mean))
system.time(mean(DT$pwgtp15,by=DT$SEX))
system.time(tapply(DT$pwgtp15,DT$SEX,mean))
system.time(rowMeans(DT)[DT$SEX==1])+system.time(rowMeans(DT)[DT$SEX==2])
