from datetime import datetime
import tweepy
import codecs
import time



########################
consumer_key = ""
consumer_secret = ""
access_token = ""
access_token_secret = ""
storePath = ""
project = ""

keywords = ["a", "b", "c"]
########################

auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)

api = tweepy.API(auth)
start = datetime.utcnow()
write = codecs.open(storePath+project+'_'+str(start.year)+'_'+str(start.month)+'_'+str(start.day)+".json",'a','utf-8')
class StdOutListener(tweepy.StreamListener):

    def on_data(self, data):
        global write
        try:
            write.write(str(data))
        except Exception as e:
            print(e)
            print(str(data))

        end = datetime.utcnow()
        global start
        if(end.day != start.day):
            start = end
            write.close()
            write = codecs.open(storePath+project+'_'+str(start.year)+'_'+str(start.month)+'_'+str(start.day)+".json",'a','utf-8')
        return True

    def on_error(self, status):
        print(status)
if __name__ == '__main__':
    l = StdOutListener()
    auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
    auth.set_access_token(access_token, access_token_secret)   
    stream = tweepy.Stream(auth, l)
    while(True):
        try:
            #https://dev.twitter.com/streaming/overview/request-parameters#track
            stream.filter(track = keywords,encoding='utf-8')
        except KeyboardInterrupt:
            stream.disconnect()
            break
        except Exception as e:
            print (time.gmtime())
            print ("severe problem",e)
            continue

