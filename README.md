# Network-moniting-using-nagios
my project

#### Nagios plays a vital role in safeguarding the health and performance of IT systems in today’s highly connected digital environment, regardless of an organization’s size. 
#### Built by Ethan Galstad and the Nagios community, Nagios Core provides a comprehensive framework for monitoring network services, host resources, and overall system availability.
#### Its proactive detection capabilities help identify and address issues before they escalate. Key features include configuration via text files, extensibility through plugins, and detailed reporting for actionable insights.
#### The book aims to equip IT professionals with the knowledge and practical skills needed to deploy, configure, and manage Nagios effectively, covering installation, advanced setup, and troubleshooting to ensure organizational reliability and efficiency.
# Primary Terminologies:
Nagios Core: The core monitoring engine that actually performs the monitoring of hosts and services.

Host: A server, router, switch, device, or any other system that can be monitored with Nagios.

Service: A single, specific characteristic of a host being monitored by Nagios, like HTTP, FTP, or SSH.

Check Command: It defines a way of checking the status of a particular service; for example, check_http would be used for HTTP service.

Notification: The alerts sent by Nagios when a problem or recovery occurs based on predefined conditions.

Plugin: An executable piece of code through which Nagios would check the status of a host or a service, like the monitoring of CPU usage.

Configuration Files: Configuration settings for Nagios, hosts, services, and notifications are defined in text-based files.

Hostgroup: A logically grouped set of hosts that eases the configuration and management in Nagios.

Servicegroup: This is the same as hostgroups, but it applies to services rather than hosts. It groups related services for better management.

Event Handler: A script or command that Nagios is launching as a result of a change in state—for example, that it's trying to start a service after failing one.

Contact: A person or entity that receives a notification from Nagios.

Contact Group: A collection of contacts through which it becomes an easy task to send a single notification to multiple contacts at a time.

Time Period: Defines when checks and notifications are active, which results in making possible the creation of maintenance windows.

Downtime: It lets monitoring checks of hosts or services be dropped, useful for when maintenance is occurring.
Status Information: This includes descriptive information that Nagios reports about the status of hosts and services at a particular moment in time.
<p style="text-align: center;"><img width="180" height="119" alt="image" src="https://github.com/user-attachments/assets/575d79dd-c4ae-4500-985c-2911ad8eeb64" />
</p>
To setup up the monitor : two types of setup options

#### Agent-based: 
Independent agents are installed on servers to collect data, which is then sent to the Nagios server.

#### Agentless:
Uses existing protocols to gather data without installing additional software on servers. Both methods monitor critical system metrics like file system usage, CPU performance, and service status.


#### Dashboards and Alerts: The Nagios dashboard offers a real-time overview of key parameters, making it easy to track system health. 
When predefined thresholds, such as high CPU usage or low disk space, are crossed, Nagios sends alerts via email or SMS.
This ensures administrators can respond quickly to issues, minimizing downtime.

#### Plugins and Scripts: Nagios runs as a service on a server and uses small scripts or plugins to check the status of hosts and services in your network. 
These plugins, written in languages like Perl or shell script, are executed at regular intervals. 
Results are collected and stored for review. 
If a significant change is detected, additional scripts are triggered, and further actions or notifications are initiated.

#### Integration with AWS:
Nagios integrates seamlessly with AWS environments.
When installed on AWS, it provides scalable and secure monitoring for cloud infrastructure. 
The collected data is accessible through the Nagios web interface, allowing administrators to monitor both local and cloud systems in real-time. 
We discuss this installation process in more detail in the section below

# Monitoring Process:
#### Nagios Web Interface (GUI):
The Nagios Web Interface is a user-friendly dashboard where administrators can see the real-time status of all monitored resources. It helps users quickly check the status of different services, get alerts, and track performance over time. Accessible through any modern web browser, this interface is crucial for real-time monitoring and fixing issues easily.

#### Alert Notifications (SMS and Email):
One of Nagios' key features is its ability to alert administrators when something critical happens. These alerts can be sent through SMS or email, based on the settings. If a resource or service reaches a critical point, like low disk space or a service going down, Nagios quickly sends a notification to ensure the issue gets addressed right away

<img width="180" height="119" alt="image" src="https://github.com/user-attachments/assets/f9dc14ad-2aa0-4a14-adf4-5e6963145278" />

## plugins for Nagios:

Nagios plugins are small programs or scripts that check the health and performance of systems, services, or applications. 
These plugins help Nagios monitor critical resources like disk space, CPU usage, running services, and network connectivity, ensuring everything runs smoothly in your infrastructure.

## Types of Nagios Plugins:
Official Plugins:
These are built and maintained by the Nagios team, included in the standard Nagios package.
They cover common monitoring needs like CPU, memory, disk usage, and network status for popular services like HTTP, FTP, and SMTP. They are stable, frequently updated, and fully compatible with Nagios.

Custom Plugins: 
Developed by users to address specific monitoring needs not covered by official plugins, custom plugins are written in any scripting language (Python, Bash, Perl).
They offer flexibility for monitoring unique applications or specialized metrics, tailored to an organization’s requirements.
Third-Party Plugins: Created by external developers or vendors, third-party plugins provide specialized functionality for enterprise applications or hardware not supported by official plugins.
They are often shared within the Nagios community or offered commercially.

Agent-Based Plugins: 
These require installing an agent on remote systems to collect detailed metrics like CPU load and disk space.

NRPE (Nagios Remote Plugin Executor): 
NRPE is an agent-based plugin that monitors local metrics on remote servers. It runs checks on systems not directly accessible by the Nagios server, ideal for in-depth monitoring within internal networks.

Agentless Plugins: 
These plugins use standard protocols like SNMP, SSH, or WMI to collect data from remote systems without needing an agent.
Ideal for monitoring network devices or cloud-based resources.

NRDP (Nagios Remote Data Processor):
NRDP allows remote systems to send data to Nagios via HTTP/HTTPS, useful when direct access or agent installation isn’t possible, such as in cloud environments or behind firewalls.

# Step-by-Step Process for Installing and Configuring Nagios:
-------------------------------------------------------------

Step 1: 
Log in to AWS Management Console
Go to the AWS Management Console and login with credentials
Navigate to EC2 Dashboard and launch ec2 instance

<img width="1024" height="164" alt="image" src="https://github.com/user-attachments/assets/ab7ab664-fabb-45d0-879f-e011c935462f" />

Step 2: Install Required Dependencies
Install Apache
Now install apache by using following commands
---------------------------------------------
| steps |      1st  commend           |  -- end |
|------ |:------------------------:|--------:|
|  2    | sudo yum install httpd -y| done✅ |
----------------------------------------------

<img width="517" height="307" alt="image" src="https://github.com/user-attachments/assets/f9b20cc5-9082-4646-b347-51d6e4bf01cd" />

-----------------------------------------------
| steps |     2nd   commend         |     end |
|------ |:-------------------------:|--------:|
|  2 (1)|sudo systemctl start httpd | done✅ |
|  2(2) |sudo systemctl enable httpd| done✅ |
----------------------------------------------
<img width="672" height="39" alt="image" src="https://github.com/user-attachments/assets/d65f82c3-bb7d-4346-bdbb-f7117361bb65" />

### install php
now,

----------------------------------------------------------------
| steps |                   2nd   commend            |  -- end |
|------ |:------------------------------------------:|--------:|
|  2 (1)|sudo amazon-linux-extras install php7.4 -y  | done✅ |
|  2(2) |     sudo systemctl restart httpd           | done✅ |
----------------------------------------------------------------

<img width="1060" height="365" alt="image" src="https://github.com/user-attachments/assets/b01e75ae-f923-4e0a-b5f5-4c14ec92e4b4" />

## Install GCC and other dependencies:


---------------------------------------------------------------------------------------------------------------------
|         steps |                   -          3nd   commend                                              |  -- end |
|---------------|:---------------------------------------------------------------------------------------:|--------:|
|  3(1)        |sudo yum install gcc glibc glibc-common wget unzip httpd php gd gd-devel perl postfix -y | done✅ |
--------------------------------------------------------------------------------------------------------------------

<img width="655" height="312" alt="image" src="https://github.com/user-attachments/assets/0076b2bb-1f24-4ab2-9d40-5cf8baebbd12" />

Step 3: Install Nagios Core
Create Nagios User and Group:

----------------------------------------------------------------
| steps |                   2nd   commend            |  -- end |
|------ |:------------------------------------------:|--------:|
|  3(1)|     sudo useradd nagios                    | done✅ |
|  3(2) |   sudo usermod -a -G nagios apache         | done✅ |
----------------------------------------------------------------

### cd /tmp
wget https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.4.6.tar.gz
tar -zxvf nagios-4.4.6.tar.gz
cd nagios-4.4.6

<img width="1048" height="421" alt="image" src="https://github.com/user-attachments/assets/34db4344-35c2-4d4b-afb0-186bdfb4ccc6" />

Compile and Install Nagios:



----------------------------------------------------------------------------
| steps |                   3nd   commend                        |  -- end |
|------ |:-------------------------------------------------------|--------:|
|  3(1)|  sudo ./configure --with-command-group=nagios           | done✅  | 
|       |  sudo make                                             | done✅  | 
|       |  sudo make install                                     | done✅  | 
|       |  sudo make install-init                                | done✅  | 
|       |  sudo make install-commandmode                         | done✅  | 
|       |  sudo make install-config                              | done✅  | 
|       |  sudo make install-webconf                             | done✅  |                                                 
----------------------------------------------------------------------------

<img width="986" height="396" alt="image" src="https://github.com/user-attachments/assets/4724897a-c713-4674-a684-f7db2e82d1ee" />

## Set Up Web Interface:

-----------------------------------------------------------------------------------------
| steps |                                            3nd   commend            |  -- end |
|------ |:-------------------------------------------------------------------:|--------:|
|  3 (1)|   sudo htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin | done✅ | 
----------------------------------------------------------------------------------------

## Here Set your password

<img width="875" height="81" alt="image" src="https://github.com/user-attachments/assets/8227fe0b-0672-4c5b-8828-6c153b2128ea" />

## Step 4: Install Nagios Plugins

 Download and Extract Plugins:

--------------------------------------------------------------------------------------
| steps |                       4nd   commend                              |  -- end |
|------ |:----------------------------------------------------------------:|--------:|
|  4(1) |    cd /tmp                                                                 |
|       |   wget https://nagios-plugins.org/download/nagios-plugins-2.3.3.tar.gz     |
|  4(2) |    tar -zxvf nagios-plugins-2.3.3.tar.gz                                   |
|  4(3) |    cd nagios-plugins-2.3.3                                                 |
--------------------------------------------------------------------------------------

<img width="1046" height="406" alt="image" src="https://github.com/user-attachments/assets/1007b145-f4de-4222-b589-558bb825acad" />

## Compile and Install Plugins:


-----------------------------------------------------------------
| steps |                   4nd   commend            |   end    |
|------ |:------------------------------------------:|---------:|
|       |     sudo ./configure                       |          |
| 4(1)  |      sudo make                             | done✅  |
| 4(2)  |    sudo make install                       | done✅  |              
-----------------------------------------------------------------

<img width="755" height="322" alt="image" src="https://github.com/user-attachments/assets/4e60ee9e-879b-44fc-8144-f5bbe85dd876" />

## Step 5: Start and Verify Nagios

Enable and Start Nagios Service:

-----------------------------------------------------------------
| steps |                   4nd   commend            |   end    |
|------ |:------------------------------------------:|---------:|
| 5(1)  |     sudo systemctl enable nagios           | done✅  |
| 5(1)  |     sudo systemctl start nagios            | done✅  |                       
-----------------------------------------------------------------

<img width="1096" height="73" alt="image" src="https://github.com/user-attachments/assets/15bdf9c7-28c1-41b5-9b68-4471216fac35" />
## Verify Nagios

Open your web browser and navigate to http://your-instance-public ip/nagios and log in with the username nagiosadmin and the password you set.

<img width="729" height="322" alt="image" src="https://github.com/user-attachments/assets/7cda0ec2-ea2a-4af1-af4e-6c0fd8d7719d" />

## In below figure we see official page of nagios

 <img width="775" height="322" alt="image" src="https://github.com/user-attachments/assets/8b7b5f34-4d7a-4409-b672-b667d2943642" />

### Step 6: Configure Nagios to Monitor a Host

Define a Host

Edit the hosts configuration file

--------------------------------------------------------------------------------------
| steps |                           4nd   commend                          |   end    |
|------ |:----------------------------------------------------------------:|---------:|
| 6(1)  |      sudo vi /usr/local/nagios/etc/objects/localhost.cfg         | done✅  |
---------------------------------------------------------------------------------------

Here is a complete example of the localhost.cfg file

## Define a host for the local machine

define host {

    use                     linux-server

    host_name       localhost

    alias                   localhost

    address             127.0.0.1 #replace with your IP Address

}

## Define a service to check the load on the local machine

define service {

    use                                  generic-service

    host_name                    localhost

    service_description      HTTP

    check_command          check_http

}

## Define a hostgroup for Linux servers

define hostgroup {

    hostgroup_name   linux-servers

    alias                           Linux Servers

    members                 localhost

}

<img width="755" height="375" alt="image" src="https://github.com/user-attachments/assets/b6d1570f-5c7a-4f13-9227-5b137b29c9ac" />


### Restart Nagios

Now restart Nagios to apply all host and service details

--------------------------------------------------------------------------------------
| steps |                           4nd   commend                          |   end    |
|------ |:----------------------------------------------------------------:|---------:|
| 6(1)  |                 sudo systemctl restart nagios                    | done✅  |
---------------------------------------------------------------------------------------


## Step7: Verify

If your server's IP address is 172.31.46.7, you would access Nagios by entering http://172.31.46.7/nagios in your web browser's address bar.

# Services

<img width="987" height="387" alt="image" src="https://github.com/user-attachments/assets/62ce8a09-1879-47cc-b407-286f85510d57" />





Host Details

<img width="775" height="322" alt="image" src="https://github.com/user-attachments/assets/0f0f871e-bdc7-4b4d-b91e-343ee0493b2c" />

## Benefits of Nagios

In-Depth Infrastructure Oversight: Nagios delivers detailed tracking of hosts, services, applications, networks, and critical components, offering complete visibility and proactive issue detection.

Effective Alerting System: Features reliable notifications with escalation options, multiple channels (email, SMS, etc.), and timely warnings to enable rapid resolution and minimize disruptions.

Extensive Extensibility: Built on a robust plugin ecosystem with thousands of community contributions, allowing tailored checks for virtually any system or custom requirement.

Proven Reliability and Efficiency: Known for stability, low resource usage, and high performance, even on modest hardware, making it suitable for long-term deployments.

Vibrant Open-Source Ecosystem: Backed by a dedicated global community providing ongoing plugins, updates, and resources, ensuring adaptability to new technologies.

Insightful Analytics and Visualization: Includes trend graphs, performance charts, and reporting tools to support forecasting, capacity management, and informed decisions.

## Drawbacks of Nagios

Challenging Initial Deployment: Requires manual configuration via files and command-line expertise, which can be time-consuming and demanding for beginners.

Potential Performance Impact: Intensive polling schedules may consume system resources, especially in large-scale environments with frequent checks.

Significant Skill Requirement: Features a notable learning curve, particularly for customization, integration, and effective troubleshooting.

Legacy Web Experience: The standard interface appears outdated and less polished compared to contemporary tools with intuitive, modern designs.

Scheduled Check Model: Relies primarily on polling intervals rather than push-based or instant metrics, potentially delaying detection in highly dynamic setups.

Plugin Dependency Management: Core features often require third-party plugins, which may vary in quality, maintenance, or compatibility over time.


# Conclusion
Nagios stands as a robust and widely adopted open-source monitoring tool designed to maintain reliability and performance across IT infrastructures. 
Its comprehensive monitoring capabilities, combined with powerful alerting and notification systems, empower organizations to detect and address potential issues proactively, thereby minimizing downtime and enhancing operational efficiency.

Although Nagios excels in customization, scalability, and benefits from a vibrant community with extensive plugin support, it does come with certain challenges, including a complex setup process, a steep learning curve for newcomers, and potential resource overhead on monitored systems. These aspects highlight the need for careful planning and configuration expertise to fully leverage its strengths.

Overall, Nagios remains an excellent choice for organizations seeking a flexible, extensible, and cost-effective monitoring solution suited to diverse IT environments. By utilizing its detailed insights and timely alerts, teams can stay ahead of infrastructure issues and ensure consistent, high-performance service delivery.
















