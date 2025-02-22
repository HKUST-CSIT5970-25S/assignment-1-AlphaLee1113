[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: Lee Wai Kiu
### Student Id: 20769482
### Email: wkleeak@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    >To evaluate CPU and memory performance, Phoronix Test Suite is used as the measurement tool in this lab. The tool is installed by using "sudo dpkg -i phoronix*.deb" and the configuration is kept to default. I decided to keep the configuration default because this config is good enough for finding the CPU and memeory performance.
    > For CPU test, i will collect the average compressing rating to evaluate the CPU performance. To get the value, the command "phoronix-test-suite run pts/compress-7zip" is used.
    > For memory test, i will collect the average copy memory per second to evaluate the memory performance. To get the value, the command "phoronix-test-suite run pts/ramspeed" is used.
    > 
    > For networking performance, iperf is used.
    > For TCP performance, I will set the parameter to 256K because it can allow me to collect the performance data in a shorter time. The bandwidth between the server and client will be collected to evaluate the TCP performance. The command used to collect this data is "iperf -s -w 256K" and "iperf -c [Server IP address] -w 256K".
    >
    >For measuring RTT, ping is used since it is a built-in command and easy to use. To evaluate the RTT performance, i will set the parameter to simply sending 1 packet so that i can collect the result quickly. The RTT for transmitting and receiving 1 packet will be collected to evaluate the RTT performance. The command used is "ping -c 1 [Server IP address]".

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` |                 |                    |
    | `t2.medium`  |                 |                    |
    | `c5d.large` |                 |                    |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` |                |          |
    | `m5.large` - `m5.large`   |                |          |
    | `c5n.large` - `c5n.large` |                |          |
    | `t3.medium` - `c5n.large` |                |          |
    | `m5.large` - `c5n.large`  |                |          |
    | `m5.large` - `t3.medium`  |                |          |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      |                |          |
    | N. Virginia - N. Virginia |                |          |
    | Oregon - Oregon           |                |          |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
