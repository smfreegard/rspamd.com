---
layout: doc
title: URL reputation module
---

# URL reputation module

The URL reputation plugin filters URLs for relevance and assigns dynamic reputation to selected TLDs which is persisted in Redis (see [here]({{ site.baseurl }}/doc/configuration/redis.html) for information on configuring redis).

For it to be enabled, the following should be set in `/etc/rspamd/local.d/url_reputation.conf`:
~~~ucl
enabled = true;
~~~

# Configuration

The following settings can be configured for this module:

~~~ucl
# Key prefix for redis - default "Ur."
key_prefix = "Ur.";
# Symbols to insert - defaults as shown
symbols {
  white = "URL_REPUTATION_WHITE";
  black = "URL_REPUTATION_BLACK";
  grey = "URL_REPUTATION_GREY";
  neutral = "URL_REPUTATION_NEUTRAL";
}
# DKIM/DMARC/SPF allow symbols - defaults as shown
foreign_symbols {
  dmarc = "DMARC_POLICY_ALLOW";
  dkim = "R_DKIM_ALLOW";
  spf = "R_SPF_ALLOW";
}
# SURBL metatags to ignore - default as shown
ignore_surbl = ["URIBL_BLOCKED", "DBL_PROHIBIT", "SURBL_BLOCKED"];
# Amount of samples required for scoring - default 5
threshold = 5;
# Maximum number of TLDs to update reputation on (default 1)
update_limit = 1;
# Maximum number of TLDs to query reputation on (default 100)
query_limit = 100;
# If true, try to find most 'relevant' URL (default true)
relevance = true;
~~~
