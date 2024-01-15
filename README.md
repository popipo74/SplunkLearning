# Splunk Learning

Access the Splunk environment via [https://splunk.samsclass.info](https://splunk.samsclass.info), hosted by Sam https://samsclass.info/50/proj/botsv1.htm.
The question is based on cyberdefend  Boss Of The SOC v1 Blue Team Lab Category: Threat Hunting by Splunk team

To understand the available data, it's crucial to explore the Search & Reporting functionality within Splunk.

One of the most valuable aspects is the use of sourcetypes, especially when utilizing add-ons for Windows logs. These add-ons provide simplified information extracted from Wineventlog.

Here are some key sourcetypes and their corresponding sources:

- **fgt**: Fortigate logs
- **iis**: Microsoft web server logs
- **syslog**: Logs from the Splunk server itself
- **suricatar**: alert from the intrusion detection system
  
When searching in Splunk, the `index="botsv1"` term signifies a specific location.


to search it is better to use field = value. search for all mean splunk will use a lot of resources

the lab excercise Boss of the SOC from splunk team is use in this lab.

we have been task to as security analyst to protect and defend Wayne Enterprise


The following images display the types of data available, along with their associated hosts:

![image](https://github.com/popipo74/SplunkLearning/assets/46301752/b4257874-08da-4147-a3b2-a36a0cdd482d)
![image](https://github.com/popipo74/SplunkLearning/assets/46301752/1143655b-b759-4b48-9bab-9147f3201208)

below is known as field, it is 
![image](https://github.com/popipo74/SplunkLearning/assets/46301752/9dd723da-46d7-4703-acfe-d81373fd25fa)
![image](https://github.com/popipo74/SplunkLearning/assets/46301752/664badb8-c266-4a40-9852-a75922417bea)

![image](https://github.com/popipo74/SplunkLearning/assets/46301752/031fcf07-0146-4e06-b0c3-0665e153b7d3)


To investigate further, you can use the following command and check a few logs:

```bash
sourcetype="stream:http" imreallynotbatman.com
```

In essence, this command reveals that IP address 40.80.148.42 is performing a web vulnerability scan on imnotreallyabatman.com (hosted at 192.168.250.70). Web vulnerability scanners often indicate their activity in the header.

![image](https://github.com/popipo74/SplunkLearning/assets/46301752/7db03dbc-6ec1-487e-bbd9-e44b6f72efa1)

Examining the raw text, we identify the attacker as 40.80.148.42, targeting the web server imnotreallyabatman at 192.168.250.70.
![image](https://github.com/popipo74/SplunkLearning/assets/46301752/f5754e6b-94fb-4e21-b33d-d64c8372c26b)


based on the event happening we can make sure that imreallynotbatman.com is a webserver and it is using Joomla application and performing acunetix web vulnerability scanning.
usually the software will mark on the src_headers to shown itself.
![image](https://github.com/popipo74/SplunkLearning/assets/46301752/bae96ba9-b3b7-43a7-a013-f7677fe2f0b9)
![image](https://github.com/popipo74/SplunkLearning/assets/46301752/1706ffb5-3d75-44e8-a84c-5b816992ff91)
![image](https://github.com/popipo74/SplunkLearning/assets/46301752/d5fd6c87-ccc1-4676-af0b-9c59e1cc8464)

if we got at the field, c_ip mean that there are 2 ip that are served as client. Meaning the ip is performing http request for server.
![image](https://github.com/popipo74/SplunkLearning/assets/46301752/d73f39a9-df56-44a0-9db7-3b8109c1f6b4)

For finding the file, we need to know what network from the webserver to the network. so we using c_ip=192.168.250.70 to specify the network is outbound from the server.
![image](https://github.com/popipo74/SplunkLearning/assets/46301752/e121faa3-0da0-4705-a94d-d03f19241e4d)

by using below command, we can specify which table/log are requested from the webserver.
sourcetype="stream:http" c_ip="192.168.250.70"

based on the raw file below, we can identifier the file downloaded. the address of the attacker malicious server to retrived the file.
![image](https://github.com/popipo74/SplunkLearning/assets/46301752/ef2227d8-0902-477a-8f24-25d8d4a75549)

![image](https://github.com/popipo74/SplunkLearning/assets/46301752/a7dc4f8e-5dcc-4a29-8e88-b02bffc1bd1b)

![image](https://github.com/popipo74/SplunkLearning/assets/46301752/c583637f-b36f-48e9-ac2f-1a5ef54180ee)

Flowchart on how this attack is performed
![image](https://github.com/popipo74/SplunkLearning/assets/46301752/6ea188f4-7089-4cc1-a1b1-3bdc9991786f)

In order to identify brute force attack, we specify the log by picking http method post. this is because in web development we use post method to send the credential to the server in a secure way( we dont expose the credential in URl).
Then, we specify the word passwd & username because it is the variable for the credential.

sourcetype="stream:http" c_ip="23.22.63.114" http_method=POST  "passwd=" "username="
![image](https://github.com/popipo74/SplunkLearning/assets/46301752/55cfe648-218e-4649-aea2-8088405b45eb)

The result show many table that contain "passwd=" and "username=". Hence, we insert into the field "table_time form_data" to simplify the table showed.
sourcetype="stream:http" c_ip="23.22.63.114" http_method=POST  "passwd=" "username=" | table_time form_data
![image](https://github.com/popipo74/SplunkLearning/assets/46301752/b4f6a387-2bbc-4bcb-8cbb-19e7979745c7)

Then we can identify that there is attempted bruteforce by 23.22.63.114
![image](https://github.com/popipo74/SplunkLearning/assets/46301752/e1e7e595-3115-4ba8-bd4a-72365ac59279)

We can determined the executable file by search .exe file. this mean that after the server has been infiltrate. the attacker control the server and requesting the file from malicious server.
sourcetype="stream:http"  *.exe imreallynotbatman.com c_ip="40.80.148.42"


![image](https://github.com/popipo74/SplunkLearning/assets/46301752/a2181ab2-13ee-48aa-8aa2-14c0b5b5a4d1)
![image](https://github.com/popipo74/SplunkLearning/assets/46301752/36a53848-bfa5-4df8-8a04-02e175a2b36d)
![image](https://github.com/popipo74/SplunkLearning/assets/46301752/0b7e045e-b661-4734-a1ea-771b82c57d1a)
