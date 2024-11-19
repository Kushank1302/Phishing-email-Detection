# Phishing-email-Detection
This project showcases a dynamic security Phishing detection  using Splunk, a powerful platform for log management and analysis. The dashboard provides all the emails which  trying to attempt the phishing attack.
This project demonstrates how to detect phishing attempts in email data using Splunk. The project ingests email logs (in CSV format) and analyzes the content for phishing-related keywords. The system then flags emails that contain multiple phishing keywords and provides insights into the senders involved in phishing activities. It also offers potential for further enrichment with threat intelligence data for better detection.

1. Features
Keyword-based Detection: Detects phishing emails by matching specific phishing-related keywords in the email body (e.g., "verify", "urgent", "account", etc.).
a. Multiple Keyword Detection: Filters emails that contain more than one phishing keyword.
b. Sender Analysis: Provides a count of phishing emails grouped by sender to help identify potentially malicious actors.
c. Real-time Analysis: The solution can be configured to run in real-time for continuous monitoring or scheduled searches for periodic reporting.
d. Visualization: Generates insights and statistics on phishing email trends, such as phishing emails by sender and email keywords.

2. Requirements
To get started with this project, you need:
a. Splunk (with Splunk Universal Forwarder for data ingestion)
b. CSV Files with email logs (or simulated phishing email data)
c. Basic knowledge of Splunk Search Processing Language (SPL)
d. A Splunk instance (cloud or on-premise) with appropriate indexing and sourcetype configuration

3. splunk spl code :
   source="SpamAssasin (1).csv" host="Phishing_email" index="main" sourcetype="csv" body=* sender=*
   | eval contains_phishing_words=if(match(body, "(?i)(verify|urgent|click here|account|password)"), "Yes", "No")
   | search contains_phishing_words="Yes" | sort IN ("date" , "contains_phishing_words")
   | stats count as contains_phishing_words BY sender,date
