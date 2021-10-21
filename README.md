
# iOS 15.0.2 Data Leak
## 10,000+ ISO.org username, first name, last name, and emails leaked as a result of sloppy QA by Apple
### Author: Jonathan Scott @jonathandata1
### Date: October 21st, 2021
![iOS 15.0.2 Data Leak](https://i.postimg.cc/28WT5QPX/Untitled-design-Max-Quality-2021-10-21-T072826-360.jpg)

## Overview
#### As I was preparing material for a lecture I will be giving on the ethics of mobile forensics, I came across a link while running my forensic tools. 

> Background: I decompressed the DMG inside of iOS 15.0.2 (018-78120-011.dmg) the build name is Sky19A404.D63OS

#### The link I found was https://isotc.iso.org/livelink/livelink/Open/16944257

> Locations: 
> Symbiotic Link: /usr/share/zoneinfo/iso3166.tab
> Direct Path: /usr/share/zoneinfo.default/iso3166.tab

## Interest

#### The code comments in these files read as follows:
![iOS 15.0.2 Data Leak](https://i.postimg.cc/tJ43NPTW/Screen-Shot-2021-10-21-at-7-20-28-AM.png)

#### I noticed that going to that URL in a browser I was able to view data that was not available to the public.

> I went back to read the code comments, and I could see that these code comments had nothing to do with the data that I was looking at on iso.org. As I began to traverse the site, I noticed that I was able to access restricted areas that have gone outside of the public domain. 

## PII Exposure

#### Now that I understood what was actually happening, I was concerned because I was able to see a list of over 10,000 ISO.org Usernames, First Names, Last Names, and Email Addresses from all around the world. 

> This list includes international government, and major corporations PII. 

![iOS 15.0.2 Data Leak](https://i.postimg.cc/BZmk9BxW/Screen-Shot-2021-10-21-at-4-25-19-AM.png)

## The Issue
### CWE-200

> the code manages resources that intentionally contain sensitive
> information, but the resources are  **unintentionally made
> accessible** to unauthorized actors. In this case, the information
> exposure is resultant - i.e., a different weakness enabled the access
> to the information in the first place.
**Source:** https://cwe.mitre.org/data/definitions/200.html

#### Although this PII leak was "unintentional," I am making the argument that this could have been prevented if a proper code review had been conducted. Code comments dating back to 2015 that contain reference links, should not be taken as valid 6 years later in 2021 unless properly vetted. In this case, this URL lead to a URI that contained PII of over 10,000 users. 

## UPDATE
#### As expected, people are trying to make the argument that this is not Apple's issue, this is an issue with ISO.org, and there is truth in both...but this heavily lives with Apple

1. ISO.org did not write the code that references their URL endpoint that leads to a URI PII leak, the author Paul Eggert has been affiliated with Apple for years. 
2. ISO.org likely does not even know about their URL endpoint being used as a reference link since they did not provide the code, or the inclusive file packaged into the DMG, later the ipsw.
3. ISO.org does have an issue to fix, but this may be something that they are already aware of, and could possibly already be fixing, this does not give Apple the right to publish code without authenticating the URL endpoints they are referencing, especially if the URL endpoint is 5 years dated and has no direct object reference to the table listed in the iso3166.tab. 



## Purposeful Disclosure

#### My intent by disclosing this is to bring awareness to data privacy concerns, human rights violations as it pertains to data privacy issues, and have not just Apple be more conscience of their actions or inactions, but for everyone to really look at the state of our privacy and security. I refuse to submit vulnerabilites to Vulnerability Disclosure Programs for any company due to NDAs that bind me to silence even if the issue is not addressed and if I speak out about the issue not being fixed, this NDA threatens my freedom. I have been burned more times than I can count. I was the #1 hacker in the USA for the last 90 days on Hackerone.com, and I was kicked out for speaking up about a data leak that was ignored, but yet fixed behind my back.

> I am not personally looking for a bug bounty, but if one is awarded I would like 100% of the bounty to donated to CharityWater.org 

 
