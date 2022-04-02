# BeeScan（Display side）

## Introduction

BeeScan is a cyberspace asset detection tool based on Go language. Tools are divided into display side and scanning side. This is the display end, and the scanning end is at [BeeScan-scan](https://github.com/jiaocoll/BeeScan-scan). The separation of the display end and the scanning end can realize distributed deployment of the scanning end, thereby improving the efficiency of scanning.

The display side uses the back-end service written by the gin framework. The author's front-end is relatively poor, so the front-end does not use Vue and other technologies (after I have time to learn and then refactor), the overall project is relatively small, and what the user gets is a binary program, all static files have been packaged into the program middle.

## Process Design

![](img/Beescan.png)

## Features

- Full text keyword search
    - title=""
    - body=""
    - header=""
    - domain=""
    - ip=""
    - app=""
    - servername=""
    - port=""
    - country=""
    - city=""
    - org=""
    - province=""
    - region=""
    - ······More search syntax waiting for you to explore

- Integrate statistical assets and associate the bound domain name assets of each IP
- Distributed scanning of scanning nodes, greatly improving efficiency
- Call nuclei vulnerability scanning, let users use their own grammar rules to search for corresponding assets from the database for vulnerability scanning
- Monitor the running status of each scanning node in real time

## Display side functions

### Asset display

It is mainly used to display the results that have been scanned by the scanning terminal, and to perform statistics on the scanned results, including country statistics, port statistics, and service statistics. Since the database is using the elasticsearch database. Keyword full-text search is available. In addition to the first time, it also provides the function of asset export, which can export the detected assets.

> Partial search syntax：
>
> title=""
>
> body=""
>
> header=""
>
> domain=""
>
> ip=""
>
> app=""
>
> servername=""
>
> port=""
>
> country=""
>
> city=""
>
> province=""
>
> region=""
>
> Syntaxes can be combined with && (and) and || (or)

### Task Release

The task can be published by entering the target on the task publishing page. The user needs to input the target (domain name, ip, URL), port (optional), specified node (select an idle node), and task name.

### Node Status

On the task release page, you can view the current real-time running status of each node, Free (idle), Invaild (invalid), Running (running)

### Vulnerability Scan

On the vulnerability scanning page, enter the corresponding asset search grammar rules, enter the task name, and you can call nuclei for vulnerability scanning (currently only call nuclei, and other vulnerability scanning modules will be added later. Since POC maintenance is not easy, the call here is It has a relatively complete ecological vulnerability scanning tool.) The results of the scan are stored in the database, and then the related vulnerabilities can be viewed on the vulnerability scanning page, and the vulnerability can be searched at the same time.

### Log View

You can view the logs of the display side and the running logs of each node. In this way, you can understand what operations the nodes have performed, or make mistakes.

### Local Information

Output the detailed information of the host currently running the display terminal, including (system, framework, storage space, memory usage, real-time network card network speed monitoring)

## Scanner Function

### Host Alive

- multi-mode detection（ICMP、Ping、HTTP）

### Port Detection

- tcp/udp

### Service Identification

- Multi-module detection
- Different fingerprints of different services are compared to reduce repeated package issuance and improve efficiency
- Detection using browser crawler
- Rich fingerprint library

## Display side page

### Login page

![image-20220402204446012](img/image-20220402204446012.png)

### Local information page

![image-20220402204515914](img/image-20220402204515914.png)

![image-20220402204532715](img/image-20220402204532715.png)

### Asset display page

![image-20220402204625380](img/image-20220402204625380.png)

### Task Publishing and Node Status Pages

![image-20220402204640687](img/image-20220402204640687.png)

![image-20220402204653187](img/image-20220402204653187.png)

### Vulnerability Scanning Page

![image-20220402204704351](img/image-20220402204704351.png)

### Log page

![image-20220402204718595](img/image-20220402204718595.png)

![image-20220402204749724](img/image-20220402204749724.png)

## How to use

### 1.Deploy the database

For users, redis and elasticsearch databases need to be deployed

### 2.Download binaries

Then download the running package of the corresponding system from the release, and then run the binary program. The first run will generate a config configuration file in the directory where the tool is located, and then modify the address and port of the database in the configuration file. Then run the binary program directly. Of course, maybe you need to know the configuration information in config, because it contains the information of the node.

## Disclaimer

This tool is only for **legally authorized** enterprise security construction behavior. If you need to test the usability of this tool, please build a target environment by yourself.

When using this tool for detection, you should ensure that the behavior complies with local laws and regulations and has obtained sufficient authorization. **Do not scan unauthorized targets.**

If you have any illegal behavior in the process of using this tool, you shall bear the corresponding consequences by yourself, and we will not bear any legal and joint responsibility.

Before installing and using this tool, please **must read carefully and fully understand the contents of each clause**. Restrictions, disclaimers or other clauses involving your significant rights and interests may be bolded or underlined to remind you to pay attention . Unless you have fully read, fully understood and accepted all the terms of this agreement, please do not install and use this tool. Your use behavior or your acceptance of this agreement in any other express or implied manner shall be deemed that you have read and agreed to be bound by this agreement.

## Todo

- [ ] Improve front-end pages and use vue for reconstruction
- [ ] Improve node monitoring, and consider using mature message queues in the future
- [ ] Improve the scanning logic and scanning effect of the scanning terminal, and add a fingerprint database of your own
- [ ] Improve the vulnerability detection function, call the POC of nuclei and xray instead of calling nuclei or xray (the focus of the project is not on vulnerability detection, but on asset detection and service identification, and will focus on exploring more underlying asset detection technologies, not just calling fingerprint library)