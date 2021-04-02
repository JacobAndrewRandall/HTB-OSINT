# EasyPish Challenge 1
![Intro](https://github.com/JacobAndrewRandall/HTB-OSINT/blob/main/HTB-OSINT/docs/EasyPish/Images/Intro.png)

From the description we can see that the customers of `secure-startup.com` are getting *convincing* phishing emails.
This points to the idea that the email service may be getting spoofed by attackers allowing them to send emails posing
as the legit domain `@secure-startup.com`. This means that it is likely a problem caused by the configuration of the
mail server for the site. 

## Looking into the mail server
A way to scan for the configuration of the mail server is using a tool built in to most distros of Linux called
`dig` or **D**omain **I**nformation **G**roper. After running `dig TXT secure-startup.com` through the CLI to view
the website TXT records where the mail servers are configured it returns what looks to be a partial flag in the 
answer section in the TXT record's input `HTB{RIP_SPF_Always_2nd`.

![Dig](https://github.com/JacobAndrewRandall/HTB-OSINT/blob/main/HTB-OSINT/docs/EasyPish/Images/digScan.png)

This partial flag gives me encouragement that I am looking in the right place, since I now know that I need to look
further into the mail server. After doing some more digging I ran a scan on the DMARC to view the DNS record for email policies, this is because if something is misconfigured in the policies of the mail server it may create a vulnerable attack surface for spoofing emails. An example of this is mistaking the `p=none` field for a field that protects against data that failed authentication when in reality all it does is notifies the domain owner wether the data failed or passed, data still gets send through regaurdless of a pass or fail which isn't good if you asume it rejects the failed data. After running
`dig TXT _dmarc.secure-startup.com` it returns the second half of the flag in the TXT field for DMARC

![dmarc](https://github.com/JacobAndrewRandall/HTB-OSINT/blob/main/HTB-OSINT/docs/EasyPish/Images/digDmarc.png)

I appended the two halfs and submitted the flag which won me the challenge! (I'm not allowed to show the full code due to the terms and conditions on Hack The Box)

