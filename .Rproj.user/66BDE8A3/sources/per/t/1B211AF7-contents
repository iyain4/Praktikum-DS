library(twitteR)
library(ROAuth)
library(tm)
library(rtweet)
library(wordcloud2)
library(wordcloud)

api_key<- "tNeo0IAAcnKX0KrufgkSljGEG"
api_secret<- "SnsUPi4rpcCntw2oajh88VvREGgxPW2iPfAdlOisSmdbGaY5zl"
access_token<- "1596758076635246592-8jEl6iLgAm0QTwNCoVpbM3Ki9fEOLJ"
access_token_secret<-"LlWqtPVdlDJy691VSAZof5dNgI7hTTQNnQufPcIMMvgFP"
setup_twitter_oauth(api_key,api_secret,access_token,access_token_secret)

tourism_spot<-searchTwitter("the british museum", n=1000, retryOnRateLimit = 10e3)

#simpan data raw
saveRDS(tourism_spot,file = 'rawdata.rds')

#baca data raw dan rubah ke bentuk dataframe
rawdata<-readRDS('rawdata.rds')
rawdatadf=twListToDF(rawdata)

#pembersihan data
komen<-rawdatadf$text
komenc<-Corpus(VectorSource(komen))

#hapus tanda baca, link url, huruf aneh, dan emoji dapat digunakan untuk pembersihan spam seperti spam link toko online
removeURL <-function(x) gsub("http[^[:space:]]*", "", x)
twitclean <-tm_map(komenc,removeURL)

removeRT<-function(y) gsub("RT", "", y)
twitclean<-tm_map(twitclean,removeRT)

removeUN<-function(z) gsub("@\\w+", "", z)
twitclean<-tm_map(twitclean,removeUN)

remove.all <- function(xy) gsub("[^[:alpha:][:space:]]*", "", xy)
twitclean <- tm_map(twitclean,remove.all)

twitclean<-tm_map(twitclean, removePunctuation)
twitclean<-tm_map(twitclean, tolower)

## simpan data ke dalam file csv
dataframe<-data.frame(text=unlist(sapply(twitclean,'[')),stringsAsFactors = F)
View(dataframe)

write.csv(dataframe , "cleandata.csv")


