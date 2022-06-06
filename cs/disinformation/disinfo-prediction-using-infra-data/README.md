Summary of the paper [Identifying Disinformation Websites Using Infrastructure
Features](Disinfo-website-using-infra-data-foci20.pdf).

In this paper authors have tried to identify the disinformation websites using infrastructure features such as: domain
registration info of websites, for e.g. words in domain name, tld, and second level tld, etc; TLS certificate, for e.g. Subject Alternate
Name (SAN) extension, wildcard in SAN, etc; and web hosting configuration like wordpress configuration and it's plugin
usage.

They used three categories of samples for this study: disinformation websites, authentic news websites, and other websites. For training
they used equal number of websites from each category. They used these features to train multi-class random forrest model
and was able to get good result on training and testing data. This model didn't work well on real world data, when
they tested it against Twitter posts containing URLs.

Limitation of this study is skew in large amount of other websites in real world, so even model has a very small FP rate it
would give large number of FPs. Other reasons they mention is could be that a lot of websites they used for training
were not accessible at the time of training, as they used copy of them from Web archive, which could have resulted in false prediction.

**Note**: This paper has a lot of good reference for SPAM/malicouc website/bot domain detection literature.

See the video of summary at [USENIX website](https://www.usenix.org/conference/foci20/presentation/hounsel).
