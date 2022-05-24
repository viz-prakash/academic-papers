**Summary of paper [Checking Websites’ GDPR Consent Compliance for Marketing
Emails](./Website%20GDPR%20Consent%20Compliance-22.pdf)**

In this paper authors did a through measurement of compliance of GDPR for marketing emails. In other words, how well
websites comply with GDPR while sending emails -- servicing and makrketing -- to users, and how often they commit
potential violations.

First, they state the GDPR clasuses pertinent to marketing emails and service emails and it's interpretation. They state
that first legal effort agains unsolicited marketing emails was adoption of "opt-in" requirement, and marketing emails
are prohibited in abscence of prior consent. They also state the exception to "opt-in": "it's pressumeed that existing
customers have given consent to receive marketing emails. Personal data for free services don't trigger the previous
exception."

They highlight the definition of consent as per GDPR: any freely given, specific, informed and unambiguous indication of
the data subject’s wishes by which he or she, by a statement or by a clear affirmative action, signifies agreement to
the processing of personal data.

They demarcate between servicing emails and marketing emails. Servicing emails are ad-free and not intended to promote
products or services.  Where as, marketing emails typically advertise specific products or services.  Examples include
product-related newsletters or vouchers. They state that GDPR prohibits *bundling* of consent for both marketing and
servicing emails, means, separate declaration of consent, relating only to marketing emails, is required.

As per GDPR, consent must be unambiguous. In the context of marketing emails, consent must be given through an
affirmative act or declaration.  Websites should also exercise the *double opt-in* to confirm that email owner confirms
to the service and marketing emails, preventing sign ups from user who don't actually own the email address.

To conduct the study, they picked 4000 websites from Alexa top 1 million, 1000 each from dividing 1 million in four
categories: 1000, next 9000, next 90000, and rest. Out of those 4000 websites, they found through crawling only 662
allowed registration as per which is consistent with Chatzimpyrros et. al in "You Shall Not Register!" that states only
a third of websites have registration forms. 

They took help of scientific research assitants with law degree to annotate the properties of the websites as per the
GDPR. They used double validation and resolved the disagreements with a third annotator. They also used *Cohen's K* to
measure the aggreement between annotators. Finally, after fxing crawling misses they had totall 666 annotated websites.
Both the annotator used different email address to sign up for services. In the end, they received at least one email
from 568 websites.

To find potential violations, they analyzed the revceived emails by first categorizing them as marketing or servicing
emails. Out of more than 5000 emails they recived on registered email addresses, 22% were servicing and 78% were
marketing emails. They also look for *double opt-in* practice and found that 59% of total followed the guidelines of
double opt-in. In the service emails, they found ~12% of websites either expose the user password in plain text, auto
generated password in plaintext, or password set/reset link in the first service email.

Another violation they noted was websites sharing user emails to third parties. To check that email is coming from third
party they didn't only rely on matching the second level domain because some websites have two different second level
domains, for e.g., facebook.com and facebookmail.com belongs to Facebook. They analyzed the privacy policy of websites
and T&C to see if there is mention of sharing data with susidiaries. They manually checked if the sender domains are
operated by the same group. They concluded that services share user email addresses within subsidiaries, but they didn't
present a number how prevalent this practice is. They also found a case where a website shared the email with 9
different third parties.

Based on the legal assesment, they also analyzed if websites obtain legal consent to send marketing emails and found
that at least 22% of websites had at least one GDPR violation.

They also explored the potential of automating this auditing. To characterize the legal properties of websites they
extracted features from raw HTML to find prominent features that are influential in deciding if a website satisfies
legalities using logistic regression models. To do this they collect the registration form HTML subtree of successfully
registered websites. They state that classification of entire form is not possible but don't state why. From this form
they extract features from each input, select, and button tags. Specifically, they use HTML tags (tag name and it's
text), HTML attributes (class type, attribute, placeholder, value), Is required?, etc.

They do similar feature extraction from emails: they extract bag of words from email's subject and body in a similar
fashion as emails, along with images and links.

Finally, they train a logistic regression model to check extracted feature usefullness but didn't fully explain how
their model works. They give an example of features, like if password field is present in the form or not and if the
email contains keyworkd "account" or "confirm", give 76% accuracy in classifying signing up for newsletters and
marketing emails. They had good success with classifying emails as servicing or marketing.

They left the automating the auditing to detect potential automations as future work to ensure compliance of websites.

**Questions** How prevalent is practice of email sharing in whole? Why did classification of entire registration form
didn't work? They also could have explained the ML model in detail for reader's understanding.
