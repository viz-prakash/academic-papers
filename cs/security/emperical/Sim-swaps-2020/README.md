Summary of paper [An Empirical Study of Wireless Carrier Authentication for SIM Swaps](./Sim-Swaps.pdf)

In this paper Lee et al. have studied the authentication practice used by US telecom network providers for SIM swapping.
They found vulnerability in all the carriers where an attacker with victims name and phone number was able to swap the
SIMs, in other words move the number from victim's SIM to a SIM owned by attacker. They also study the downstream
effects of these vulnerability on websites using phone numbers for authentication and account recovery. They found
various websites are double insecure, which means they could be compromised by just SIM swap attack.

To perfom the attack, they bought 10 prepaid SIMs from all the providers. They used the SIM for normal activities for
some time. Then they acted as an attacker who knows only the number and name of the SIM owner and tried to swap the SIM
to a SIM in their control by calling the customer service representetive (CSR) and answering question asked by them.
Their script to do so was pretend to be the victim who has lost the phone and is trying to swap the SIM. When asked
about the authentication question deal try to answer them in various ways.

To compromise the authentication practices used by carriers for SIM swap, techniques they used were follwoing. They are
grouped, and if the method could be compromised it's described.

*) Personal information: Street address, email address, date of birth. All these information about victim could be found
on data aggregators websites.

*) Account information: Last 4 digits of payment card number, activation date, last payment date and amount. Last 4
digits of card could be found on physical or electronic receipts. Activation date could be found on data aggregator
websites. Last payment date and amount could be found by refilling the phone number with prepaid card which doesn't
require any verfication, only phone number.

*) Device information: IMEI (device serial number) and ICCID (SIM serial number). Both of which could be acquired by
malicous apps, and IMEIs could also be acquired by radio devices.

*) Usage information: Recent numbers called. This could be acquired by tricking the victim to make a call to a number
controlled by attacker by giving them a miss call.

*) Knowledge:  PIN or password, answers to security questions. PIN or passwords are secure but answers to security
questions could be guessed. 

*) Possession: SMS one-time passcode, email one-time passcode. These both are secure ways of authentication.

Using above ways to answer the question asked by CSR they were able to swap SIM of all the carriers, which included
Verizion, T-Mobile, AT&T, TracFone, and US Mobile. They also found some times during the verfication CSR didn't ask any
verification questions, and sometimes they revealed the answers to the questions without asking or even allowed multiple
attempts to answering questions. A lot of them moved on to answer different questions when attacker provided wrong
answers and claimed they don't actually remember the correct answer.

To study the downstream effects they used TwoFactorAuth.org as data source and picked 145 websites that used SMS as 2FA.
Out of these 145, 17 are double insecure; 14 use SMS as sole MFA. 

They also analyzed the industry MFA solutions. They found Duo to be vulnerable to SIM swap attacks because they defulted
to SMS 2FA despite being able to support other secure ways. They found Okta to be secure agains SIM swap attacks.

Recommendations:

Network carriers: they should use strong authentication mechanisms, enable MFA for SIM swap attempts, CSR should respond
to wrong answers immediately, restrict the access to user information before user answers the question, document the
consistent authentication behaviors, and train the CSRs.

Websites: discontinue SMS based 2FA, use at least one secure MFA, and improve threat model to include SIM swap and
vulnerability disclosure process.

Questions: What are the practices of authentication for SIM swap outside US?
