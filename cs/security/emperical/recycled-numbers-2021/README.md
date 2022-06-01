Summary of paper [Security and Privacy Risks of Number Recycling](./recycled-numbers-latest.pdf).

In this paper authors have put light on the issues arising from phone number recycling in the US. They have pointed out
8 different kind of attacks against previous and new users of a recycled phone number. They have explored the attacks
against the previous users in depth in this papaer. They point out the downside of using phone numbers as identity, and
SMS based authentication and recovery for online services.

Authors have targeted two major telecom providers Verizon and T-Mobile in this study. Both of these network carriers
allow their existing customer to choose a new number from their web portal with proper authentication.  AT&T was not
included in this study because it doesn't offer this feature to their customers.

Authors have exploted the feature available to existing customers that allows them to browse available numbers and
switch to a available number from web portal. Because both the telecom providers allow browsing available numbers that a
user could pick, they harvested a list of number from the web portal of both the vendors and used heuristics to guess
which number is probably recycled (means previous assigned to another customer but it's available again to the
subscribers). Their idea is to pick numbers which don't have 10 available number between them; they assume that if
numbers are not seperated by 10 numbers they are probably never assigned to any customer.

Based on this heuristics they collected numbers from both Verizon and T-Mobile. To verify if their hypothesis is correct
they used public available PII (Personal Identifiable Information) indexing websites. On these websites they checked if
there is information present about the numbers they harvested. They found out their hypotheisis is not completely
correct as they find out that numbers from both categories as per their hypothesis are present on PII indexing sites.
Nonetheless, this technique helps them in finding out recycled numbers. From these website they could also find out
email associated with the number. Combining the email and phone number of the users could be used highjack the accounds
of previous owners of the numbers.

They also analyzed the recycled numbers by monitoring their activity for a week in a safe way so that previous owners
don't get harmed in any form. They found out that these recycled numbers still receive calls and text with sensitive
personal information about the previous ownders.

They also highlight how these attacks could be used to IPV (Intimate partner violence) victims as the abuser could get
access to the number of victim after finding out that victim has changed the number to avoid having contact by methods
browsing the numbers available to subscriber on telecom provider website.

Their suggestion to the carriers is that there should strict number of days a number should be aged before putting it
back in market; they should limit the number of inquiry for changing the numbers for existing customers; warn the users
about the risks of changing numebers; and place a limit number of times a user could change numbers. User should use
number parking if they want to change numbers, means reserver the number and not use it instead of just switching to a
new number. They also suggest that websites should not use SMS based 2FA and password recovery, and should use other
means for 2FA.

Questions: Are these issues just related to US based telcom carriers or rest of the world as well?
