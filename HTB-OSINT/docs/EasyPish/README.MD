# EasyPish Challenge 1
![Intro](/Images/Intro.png)

From the description we can see that the customers of `secure-startup.com` are getting *convincing* phishing emails.
This points to the idea that the email service may be getting spoofed by attackers allowing them to send emails posing
as the legit domain `@secure-startup.com` this means that it is likely a problem caused by the configuration of the
mail server for the site. 

## Looking into the mail server
A way to scan for the configuration is using a tool built in to most distros of Linux called
`dig` or `**D**omain **I**nformation **G**roper`. After running `dig TXT secure-startup.com` through the CLI to view
the website TXT records where the mail servers are configured it returns what looks to be a partial flag in the 
answer section in the TXT record's input `HTB{RIP_SPF_Always_2nd`.

![Dig](/Images/digScan.png)

This partial flag gives me encouragement that I am looking in the right place, since I now know that I need to look
further into the mail server
