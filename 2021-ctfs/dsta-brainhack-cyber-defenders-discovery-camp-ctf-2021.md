---
description: >-
  DSTA BrainHack Cyber Defenders Discovery Camp CTF 2021 is a 48-hour
  Jeopardy-style Capture-The-Flag competition held from 23-25 June 2021.
---

# DSTA BrainHack Cyber Defenders Discovery Camp CTF 2021

This competition allowed up to 4 members to form a team but I participated solo in this CTF competition with the team name: Team N0T34MN4M3.&#x20;

This CTF competition was not very well organized as there were many infrastructure issues that arised during the competition, which led to huge delays.&#x20;

Apparently, based on a statement made by DSTA CDDC team after the competition, there was an outage in their vendor's competition platform. This resulted in the competition being delayed by 24 hours and upon launch of the competition, the platform was unstable and slow.

In addition, there were vulnerabilities and bugs in some missions and troubleshooting of these missions during the competition had affected our experience.

Finally, the technical support was also not responsive enough during the conduct of the competition.

In this competition, I solved one challenge only. After facing huge delays and intermittent disruptions throughout the competition, I decided to call it a day.

## CERTIFICATE OF PARTICIPATION

![](<../.gitbook/assets/image (65).png>)

## Hidden Secret

For this challenge, it was web related but I lost the challenge description. Basically, the challenge provided us with a link to connect and these were the steps I took to solve the challenge:

1. Navigate to the link provided and inspect the code.
2. I realised one portion of JavaScript code in the JS file looks URL encoded, hence I copy paste the code into [CyberChef](https://gchq.github.io/CyberChef/) to decode it.

![](<../.gitbook/assets/image (36).png>)

3\. Once the string has been decoded, we can just print what the `String.fromCharCode` evaluates to with the browser’s console:&#x20;

![](<../.gitbook/assets/image (10).png>)

Flag: CDDC21{\_ De0bfu$cated-F!aG\_}

