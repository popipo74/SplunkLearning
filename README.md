# SplunkLearning

I just access it via imreallynotbatman.com

need to know what data u had.

most important thing to investigate in splunk is the search & Reporting

the most usefull is sourcetypes.
addon for log windows. much more simple info from wineventlog

fgt stand for log from fortigate

iis is for microsft webserver

syslog for the splunk server itself

index="botsv1" stand for location


below also show the type of data we have and its host.
![image](https://github.com/popipo74/SplunkLearning/assets/46301752/b4257874-08da-4147-a3b2-a36a0cdd482d)
![image](https://github.com/popipo74/SplunkLearning/assets/46301752/1143655b-b759-4b48-9bab-9147f3201208)


![image](https://github.com/popipo74/SplunkLearning/assets/46301752/9dd723da-46d7-4703-acfe-d81373fd25fa)


![image](https://github.com/popipo74/SplunkLearning/assets/46301752/664badb8-c266-4a40-9852-a75922417bea)

## using below command and we will check few log to find out.
`` sourcetype="stream:http" imreallynotbatman.com

bassically it mean that the 40.80.148.42	is performing web vulnerablity on imnotreallyabatman.com 192.168.250.70		
usually web vulnerability scanner will determine in it header it is performicne the activity.
![image](https://github.com/popipo74/SplunkLearning/assets/46301752/7db03dbc-6ec1-487e-bbd9-e44b6f72efa1)

if we show it in raw text
now we identified that attacker is 40.80.148.42 while the webserver imnotreallyabatman is 192.168.250.70
