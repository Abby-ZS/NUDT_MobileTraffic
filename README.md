# NUDT_MobileTraffic
An anonymized mobile traffic dataset published by Chen's team (National University of Defense Technology, school of computers)

To download the dataset, please send an email to zhaoshuang16@nudt.edu.cn to obtain the download link. Meanwhile, please attach your contact information 
(name, organization) in the email.

Using this dataset indicates that you agree to our data sharing policy. Without our consent, the dataset shall not be shared in part or in whole with 
third parties, nor shall it be used for any purpose other than academic research. At the same time, attempts to discover or restore user privacy in 
traffic are not allowed.

If researches are conducted on our dataset and the results are published, please cite our paper. 

The dataset contains the following files:


|        data        |          file name           |                        description                         |
| :----------------: | :--------------------------: | :--------------------------------------------------------: |
|    traffic data    | data1.tar.gz to data8.tar.gz |     Source traffic files, including pcap and log files.     |
|  app information   |         APPList.csv          |                The information of 350 apps.                |
| device information |        userinfo.csv          | The information of devices involved in traffic collection. |
| Bytes information  |        bytesinfo.csv         |      The byte distribution of truncated HTTP Biflows       |

** Note that data4.tar.gz, data5.tar.gz, data6.tar.gz, and data8.tar.gz are further compressed into multiple files (using 7zip software) and the sub volumes are stored in data4, data5, data6 and data8 folders, respectively.

(1) data1.tar.gz to data8.tar.gz
   
    *  The directory structure of those 8 tar.gz files is as follows:

     ---Outer folder
       |
       ---user_id folder
        |
        ----date folder
          |
          ----pcaps(.pcap), logs(.txt)

    *  The pcap file is named by the time it was collected (netlogdate_hour_minute_second(_ipv6).pcap). 
       IPv6 and IPv4 packets are stored in different pcap files with the same name prefix, and their labels are saved in one log file. 

    *  Each record in the log file contains a timestamp, an app label (in chinese), and the five-tuple information
       (Protocol, SrcIP, SrcPort, DstIP, DstPort) of one Biflow.

    *  Since Netlog uploads traffic every 5-10 minutes, their labels may not be in the log files with the same name. To make full use of data, 
       we suggest reading the log file for a whole day, and then marking the packets of that day.


(2) APPList.csv
    
    * This file provides the information of 350 head apps, including their names (in Chinese/English), categories (in Chinese/English), and descriptions.

    * Note that 6 apps have names with special characters in the recoreds of the log files, including:
       83, Dropbox (Dropbox)
       142, 猎豹安全 (CM Security)
       140, 妲己（Dajibar）
       202, 手机卫士（360mobilesafe）
       328, 贪吃蛇 (Snake)
       335, 宾果消消 （Bingo xiaoxiaoxiao）
       
      As a result, the Chinese names of these 6 apps in the APPList.csv cannot be matched with the labels in log files.  Here, we provide an code example 
      that matches these 6 apps with the labels in the log files(assuming the variable 'label' is the app label obtained from one record in the log files):

         **************************************************************
		     app1 = u'\u624b\u673a\u536b\u58eb'      #(202)
		     app2 = u'\u730e\u8c79\u5b89\u5168'      #(142)
		     app3 = u'\u5bbe\u679c\u6d88\u6d88'      #(335)
		     app4 = 'Dropbox'                        #(83)
		     app5 = u'\u59b2\u5df1'                  #(140)
		     app6 = u'\u8d2a\u5403\u86c7'            #(328)

		     if app1.encode('utf8') in label:
		     	return '360mobilesafe'
		     elif app2.encode('utf8') in label:
		     	return 'CM Security'
		     elif app3.encode('utf8') in label:
		     	return 'Bingo xiaoxiaoxiao'
		     elif app4.encode('utf8') in label:
		     	return 'Dropbox'
		     elif app5.encode('utf8') in label:
		     	return 'Dajibar'
		     elif app6.encode('utf8') in label:
		     	return 'Snake'
	 **************************************************************


(3) userinfo.csv
    
    * This file provides the device information of volunteers, 
      including user id, Phone brand, Phone model, and Android OS version.  


(4) bytesinfo.csv

    *  This file provides the byte distribution of truncated HTTP Biflows. 
       The columns in the file include user_id, filename, srcIP, srcPort, dstIP, dstPort, 
       timestamp (the timestampe of the first packet in the Biflow), 
       number of occurrences per byte (0-255), app_label (in Chinese), app_label (in English). 
