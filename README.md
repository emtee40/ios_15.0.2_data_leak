


# UPDATE: iOS 15.2 Still contains everything described here

## iOS Firmware Leaking 10,000+ Emails, Usernames, First, Last Names on ISO.org due to lack of QA when embedding open source libraries 

> Author: Jonathan Scott 
> Twitter: [https://www.twitter.com/jonathandata1](https://www.twitter.com/jonathandata1)
> Date Published: October 21st,
> 2021 Date Updated: December 17th, 2021

![iOS 15.0.2 Data Leak](https://i.postimg.cc/yYc9wKFY/Untitled-design-Max-Quality-2021-12-17-T143357-309.jpg)

## Overview
#### As I was preparing material for a lecture I will be giving on the ethics of mobile forensics, I came across a link while running my forensic tools. 

> Background: I decompressed the DMG inside of iOS 15.0.2 (018-78120-011.dmg) the build name is Sky19A404.D63OS

#### The link I found was [https://isotc.iso.org/livelink/livelink/Open/16944257](https://isotc.iso.org/livelink/livelink/Open/16944257)

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

> the code manages resources that intentionally contain sensitive information, but the resources are  **unintentionally made accessible** to unauthorized actors. In this case, the information exposure is resultant - i.e., a different weakness enabled the access to the information in the first place.
Source: [https://cwe.mitre.org/data/definitions/200.html](https://cwe.mitre.org/data/definitions/200.html)

### After further analysis I am able to prove this link referenced in the code is a backdoor that bypasses ISO.org's Pay Wall. 

> The argument can be made that this is not Apple's issue, this is an issue with ISO.org, and there is truth in both, but this data leak is 100% due to Apple backdooring data and intentionally exposing endpoints that are only available after properly paying for the data.

1. #### ISO.org did not write the code that references their after payment URL endpoint that leads to a URI PII leak, the author Paul Eggert has been affiliated with Apple for years. 
2. #### ISO.org likely does not even know about their pay wall is being bypassed publicly and is being used as a reference link since they did not provide the code, or the inclusive file packaged into the DMG, later the ipsw.
3. #### ISO.org does have an issue to fix, but this may be something that they are already aware of, and could possibly already be fixing, this does not give Apple the right to publish code that bypasses ISO.orgs pay wall exposing a vulnerability in ISO.org's systems.  
4. #### The data that is referenced in the iso3166.tab is paid data that lives behind a PAY WALL from ISO.org, reference:  [https://www.iso.org/standard/72483.html](https://www.iso.org/standard/72483.html) 

# ISO 3166-1:2020 - DATA BEHIND PAYWALL

![iOS 15.0.2 Data Leak](https://i.postimg.cc/C1zQYJ9r/Screen-Shot-2021-10-21-at-9-51-18-AM.png)

# ISO 3166-2:2020 - DATA BEHIND PAYWALL


![iOS 15.0.2 Data Leak](https://i.postimg.cc/VsFYdkhq/Screen-Shot-2021-10-21-at-9-49-16-AM.png)

# ISO 3166 PAID DATA BYPASSED & BACKDOOR EXPOSED BY APPLE THROUGH CODE COMMENT
6. I mentioned in my Twitter feed...Apple is back-dooring this data, bypassing ISO.org's paywall, and by back-dooring the data is knowingly exposing this URL endpoint
![iOS 15.0.2 Data Leak](https://i.postimg.cc/Kc980Y5Z/Screen-Shot-2021-10-21-at-9-45-30-AM.png)

## Apple's ISO Compliance Guarantee 

> #### According to Apple's own compliance Statements, they hold the following ISO Certifications. 27001 and ISO 27018. 
> 
> #### ISO 27018 specifically addresses the following points
> 
>  - Accuracy and quality
>  - Accountability
>  - Information Security
>  - Privacy Compliance

### Apple's own compliance statement puts them as the responsible party that published a vulnerable URL that lead to a URI in which 10,000+ ISO.org users data were exposed. 

![iOS 15.0.2 Data Leak](https://i.postimg.cc/PfWMQhMr/Screen-Shot-2021-10-21-at-8-09-49-PM.png)


> https://support.apple.com/en-us/HT210897
> Apple's ISO Certifications 

![iOS 15.0.2 Data Leak](https://i.postimg.cc/pVCFddZ8/Screen-Shot-2021-10-21-at-8-10-06-PM.png)

### Sources
[https://www.bsigroup.com/en-GB/our-services/certification/certificate-and-client-directory/search-results/?searchkey=licence%253d649475%2526company%253dApple&licencenumber=IS%2520649475](https://www.bsigroup.com/en-GB/our-services/certification/certificate-and-client-directory/search-results/?searchkey=licence%253d649475%2526company%253dApple&licencenumber=IS%2520649475)

[https://www.bsigroup.com/en-GB/our-services/certification/certificate-and-client-directory/search-results/?searchkey=licence%253d673269%2526company%253dApple&licencenumber=PII%2520673269](https://www.bsigroup.com/en-GB/our-services/certification/certificate-and-client-directory/search-results/?searchkey=licence%253d673269%2526company%253dApple&licencenumber=PII%2520673269)



# Remediation

> Open Source code deserves just as much scrutiny as closed. Relying on code that was last updated in 2018 at best is irresponsible, dangerous, and harmful to the community. This lack of quality assurance has lead to a massive data breech, and leak. Open source usage and responsibility falls within Apple's ISO compliance standards, and if they were only to follow these standards, we would not be in this situation. The Log4J exploit has shown that open source code needs to be examined on a much higher level that is happening right now. 

#### I recognize that others in the community are using the exact same iso3166.tab file. Highlighting this global issue only makes matters more urgent to correct. If a company like Apple is skipping their compliance standards, how is the general public supposed to maintain trust in any of their products and services?

## Open Source Licensing Impacts the Integrity of Your Software Supply Chain

Supply chain attacks are top of mind for many IT teams, and an important piece of the puzzle is ensuring its integrity. Compliance is a key part of this, and as a result, organizations like the Linux Foundation sought a solution. The  [OpenChain Project](https://www.openchainproject.org/)  was created as an effective certification for open source license compliance in the software supply chain. What it essentially does is strengthen the whole chain and ensure each section can be trusted and meets the standard of compliance set to earn the certification. The most recent OpenChain Specification is the  [ISO/IEC 5230:2020](https://www.iso.org/standard/81039.html)  which “specifies the key requirements of a quality open source license compliance program in order to provide a benchmark that builds trust between organizations exchanging software solutions comprised of open source software.”

Reference: [https://www.trendmicro.com/pt_br/research/21/g/navigating-open-source-licensing-risk.html](https://www.trendmicro.com/pt_br/research/21/g/navigating-open-source-licensing-risk.html)

## Purposeful Disclosure

#### My intent by disclosing this is to bring awareness to data privacy concerns, human rights violations as it pertains to data privacy issues, and to have Apple and other be more conscience of their actions or inactions when publishing code with open source projects embedded. 

> #### I have been reporting this since iOS 15.0.2

## I have emailed Apple security and they say the following, November 8th, 2021
![iOS 15.0.2 Data Leak](https://i.postimg.cc/MGc7TQCq/apple-communications.png)

> "After examining your report we do not see any actual security
> implications with Apple products or services. This link is included in
> open source code as part of the ISO standard."


- #### I have sent direct messages to ISO.org on Twitter - No Response
- #### I have sent emails to ISO.org - No Response
- #### Media has reached out to Apple and ISO.ORG - No Response

## I am a mobile security engineer, and most recently have been acknowledged by LG Mobile for discovering a backdoor that affects all LG Mobile Devices In the World. 

![iOS 15.0.2 Data Leak](https://i.postimg.cc/sxzH7mzp/Screen-Shot-2021-12-17-at-2-26-59-PM.png)


### Source: [https://lgsecurity.lge.com/bulletins/mobile#updateDetails](https://lgsecurity.lge.com/bulletins/mobile#updateDetails)

## Media Articles Written About This Issue

[https://leonlagreyentry.blog/apples-backdoor-security-15-0-2-exposed-iso-standard-leak/](https://leonlagreyentry.blog/apples-backdoor-security-15-0-2-exposed-iso-standard-leak/)
[https://cooltechzone.com/news/bad-qa-of-ios-15-0-2-led-to-comprehensive-exposure-of-iso-org](https://cooltechzone.com/news/bad-qa-of-ios-15-0-2-led-to-comprehensive-exposure-of-iso-org)


## I was the #1 hacker in the USA for the last 90 days on Hackerone.com, and I was kicked out for speaking up about a data leak that was ignored, but yet fixed behind my back.

### Source: [https://hackerone.com/leaderboard?year=2021&quarter=3](https://hackerone.com/leaderboard?year=2021&quarter=3)

 
