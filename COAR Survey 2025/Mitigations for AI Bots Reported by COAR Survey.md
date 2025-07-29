---
tags: 
---

Respondents reported a variety of approaches to mitigating the deleterious impact of bots. It should be noted that these are not generally focussed on "AI bots" in particular, but are rather applied to any remote software process which might cause the repository's service to be impaired thorough excessive contact.

These are outlined below. Notes about effectiveness are not based on any analysis beyond that reported by the survey respondents.

## Robots.txt

Most repositories implement some version of the "robots.txt" file, and several respondent mentioned this. This file provides a way for any web system (including repositories) to express machine-readable "rules" about which types of external service may access which of their resources. Well-intentioned remote services will be configured to read and respect these rules, but there is no inherent mechanism for enforcing them, and less scrupulous systems may simply ignore them.

One respondent described how, in 2019, they had suffered a service outage due to traffic from the Google's official web crawler. They were able to prevent this from recurring by carefully configuring their robots.txt file, and their expectation is that they will be able to do the same for the latest generation of "AI bots".

Another respondent mentioned using a service called *[Dark Visitors](https://darkvisitors.com/agents)* which provides a publicly curated list of known "artificially intelligent agents" and which can also help to semi-automatically prepare a robots.txt files.

Other respondents mentioned already configuring robots.txt files to block access by bots from well-known AI services. However, one such also commented:

> For now, those are blocked permanently as a necessary measure to keep our sites stable. These are not sustainable or desirable measures for us or our members.

## Firewalls and IP addresses blocking

Firewalls are defensive software processes designed to protect systems or, more usually, local networks. As such they are not normally managed within a repository, but more usually by whoever is managing the network infrastructure underpinning the repository system. This may be a host institution, a commercial supplier offering a hosted repository service, or an external network intermediary such as Content Delivery Network (CDN).

Firewalls work by blocking incoming network connections from external systems, where the latter can be identified by various criteria. A common way to identify external systems is to simply note their IP addresses. In the most basic case, the firewall is informed by a simple list of IP addresses to block.

More sophisticated implementations of this approach use IP address lists which are dynamically generated based on the observed behaviour of remote services. One well-known mechanism mentioned by several respondents is *Fail2ban*, which monitors log files for "suspicious" activity and blocks associatedIP addresses. Other, similar mechanisms mentioned by respondents include components for popular web server software, such as the *mod\_evasive* module for *Apache*.

In addition to blocking specific, known IP addresses, some go further by blocking ranges of IP addresses. For example, they may block all IP addresses belonging to a particular "cloud" infrastructure provider. One respondent notes a "... slight risk could block other services".

In an even more extreme measure, some respondents reported blocking all IP addresses from entire countries, where those counties were perceived as being the source of a significant volume of unwelcome bot activity. One also reported relaxing such restrictions later, once they were more able to focus their IP addresses restrictions.

## Rate limiting

Rate limiting is a counter-measure which is generally configured to set a threshold for the maximum number of requests per second from any given IP address. If this threshold is exceeded then, usually, additional connection requests are silently dropped and ignored.

This measure is normally applied at the level of the repository, rather than the network infrastructure. 

Again, there are some components which can be added to popular web server software. One respondent mentioned using a system called Splunk to provide rate limiting for their DSpace repository.

## Reducing resource-intensive repository functionality

Only one respondent mentioned this approach, of:

> Disabling resource-intensive functionality like queries, as bot activity on these features are more likely to bring down the site.

However several respondent mentioned specifically disallowing such resource-intensive pages in their robots.txt files, which is a really what robots.txt was designed for.

## White-listing "friendly" bots

Although most of the measures described by respondents to the survey based on "blacklisting" undesirable bots - identified either by name or IP address - some respondents have also started to maintain "whitelists" of bots to which they are willing to allow access to the repository. Such lists can be used to complement most of the measures described here.

## Content Delivery Networks (CDN)

CDNs are used by several respondents, with Cloudflare mentioned in particular. CDNs may provide IP addresses filtering. Furthermore, CDNs such as Cloudflare may add their own measures, such as introducing a CAPTCHA challenge between the repository and remote users or systems. This has the effect of blocking any unrecognised remote system - benign or otherwise - unless that remote system is actively trying to defeat such measures. In other words, such interventions block *all* benign systems, while only blocking *some* (perhaps *most*) malign systems.

Another more recent measure introduced by Cloudflare, mentioned by one respondent, is the *[AI Labyrinth](https://blog.cloudflare.com/ai-labyrinth/)*, which recognises when an AI bot has started accessing a website and then uses its own AI process to generate plausible but meaningless content, wasting the time and bandwidth of the crawling system. This approach is also sometimes called a honeypot, because it attracts AI bots, where human visitors would more quickly realise that the content was bogus.
