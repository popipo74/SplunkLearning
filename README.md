# Splunk Learning

Access the Splunk environment via [https://splunk.samsclass.info](https://splunk.samsclass.info), hosted by Sam.

To understand the available data, it's crucial to explore the Search & Reporting functionality within Splunk.

One of the most valuable aspects is the use of sourcetypes, especially when utilizing add-ons for Windows logs. These add-ons provide simplified information extracted from Wineventlog.

Here are some key sourcetypes and their corresponding sources:

- **fgt**: Fortigate logs
- **iis**: Microsoft web server logs
- **syslog**: Logs from the Splunk server itself
- **suricatar**: alert from the intrusion detection system
- 
When searching in Splunk, the `index="botsv1"` term signifies a specific location.

The following images display the types of data available, along with their associated hosts:

![image](https://github.com/popipo74/SplunkLearning/assets/46301752/b4257874-08da-4147-a3b2-a36a0cdd482d)
![image](https://github.com/popipo74/SplunkLearning/assets/46301752/1143655b-b759-4b48-9bab-9147f3201208)
![image](https://github.com/popipo74/SplunkLearning/assets/46301752/9dd723da-46d7-4703-acfe-d81373fd25fa)
![image](https://github.com/popipo74/SplunkLearning/assets/46301752/664badb8-c266-4a40-9852-a75922417bea)

To investigate further, you can use the following command and check a few logs:

```bash
sourcetype="stream:http" imreallynotbatman.com
```

In essence, this command reveals that IP address 40.80.148.42 is performing a web vulnerability scan on imnotreallyabatman.com (hosted at 192.168.250.70). Web vulnerability scanners often indicate their activity in the header.

![image](https://github.com/popipo74/SplunkLearning/assets/46301752/7db03dbc-6ec1-487e-bbd9-e44b6f72efa1)

Examining the raw text, we identify the attacker as 40.80.148.42, targeting the web server imnotreallyabatman at 192.168.250.70.
