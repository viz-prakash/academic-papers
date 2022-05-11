Summary of paper [Electronic Monitoring Smartphone
Apps](./Electronic%20Monitoring%20Smartphone%20Apps.pdf).

Owen et al. has conducted a privacy oriented study of Android apps used for Electronic Monitoring (EM) of people on
probation, parole, pretrial release, or people in the juvenile or immigrant detention system.

They state that people  made to use EM apps pay regular fees the app companies, do frequent biometric verifications, and
ensure their devices do not run out of battery. Failure to meet the conditions of one’s release (as determined at least
in part by the app) could lead to reincarceration.

They try to answer following questions in this study by doing static analysis and limited dynamic analysis of 16 apps:

**What are the privacy-related technical properties of the apps, including what permissions they request and what
network endpoints they contact?**

**What are the experiences and concerns of people using these apps?**

**What is the relationship between what is stated in the apps’ privacy policies and the potential risks and harms
surfaced by our first two research questions?**


To answers the first question, they used MobSF (Mobile Security Framework) to do the static analysis to find out
premissions an app requests, third party library an app uses. They also looked for an app's data collection practices
and how it's used afterwards by manual code analysis. They also conducted limted dynamic analysis of the apps to find
out about the apps' behavior, but it's limited because these apps works in conjuction with EM supervisors and need
login.

They found that these apps ask for "dangerous permissions" (as per Android) on top the normal permission. The most
common permission gave apps access to precise location information.  A few apps requested permissions that did not have
widespread use. These permission could lead to EM supervisor reading whom a user talks to.

They also found apps use analytics and ad libraries which could lead to companies behind apps making profit from these
apps. They couldn't find what endpoints collected data was sent to because of limited dynamic analysis, but apps were
using TLS for network communication. They also found that using mitm tools, for some of the apps a passive observer on
the same network could find out if a user is using EM app (privacy concern) based on the domains contacted by the apps.

To answer second qeustion, they manually analyzed the Google app store reviews of these apps to gauge user experiences.
Most of the user experiences were negative, ranging from apps doesn't work properly when user needs to report to the
supervisor, they make loud noises at inappropriate places (work, and church), taking significant resources, complete
phone freeze to potentially jeoprdizing EM requiremnt of keeping the phone always on, to general favorable reviews that
they are covinient compared to ankle monitors. Users also felt that using this apps would lead to more problems with
their EM supervisors and potentially imprisonment.

To answer the third question, they analyzed the privacy of the apps and put the findings from first and second question
in conted of privacy issues and harm they could cause to it's users.  While analyzing the policy authors found that
three apps violated Google playstore policy by not having a privacy policy. They also found that almost all the apps
shared collected data about the users to third parties for marketing and advertising purposes. Apps mentioned
regulations but may consider themselves exempt from complying with certain portions of them.  Authors state that risks
of using these apps are from large number of parties form EM company, Court, to third parties getting access to the
collected personal data about users. Some apps collect too much data and upload it to server which could put financial
burden on poor users. Authors also note that legal precedant is not in favor these app users because of the situation
they are in so they could be coerced into giving unnecessary permission to these apps which could lead to data
collection.


Authors recommend that appstore needs to be stringent with these kind of apps which violates it's policy. They also call
for researcher to take interest and study this kind of apps to make positive impact by increasing transparency, and
accountability. 

Future work for this study is to conduct a through dynamic analysis in conjuction with EM supervisor.

**Questions:** Could there be false positive related to static analysis findings as it's not confirmed with dynamic
analysis?


