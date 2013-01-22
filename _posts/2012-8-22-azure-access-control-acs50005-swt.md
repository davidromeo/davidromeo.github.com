---
layout: post
tags: [Windows Azure, Access Control, SWT]
title: "Access Control returns error ACS5000 for SWT"
---
{% include JB/setup %}


If you're going along and configuring ACS like I was for a SWT protected Web Api you might find yourself getting this crazy message:

<p>
  <script src="https://gist.github.com/3428072.js?file=ACS50005"> </script>
  <noscript>
    <pre>
       Error:Code:400:SubCode:T0:Detail:ACS50000: There was an error issuing a token. ACS50005: Token encryption is required but no encrypting certificate is configured for the relying party.
    </pre>
  </noscript>
</p>

What this means is that when you were configuring your relying party you encountered a fun bug on the ACS website. When you are first configuring the relying party if you change the token format to SWT or JWT but the token encryption policy section doesn't dissapear. If you accidentially select to require token encryption for a SWT or JWT ACS will yell at you with the above error message.

![Copy Local]({{ BASE_PATH }}/assets/images/2012/acs50005.png)

The quick fix is to select one of the SAML token formats, change your token encryption policy back to none and then select the correct token format again.

![Copy Local]({{ BASE_PATH }}/assets/images/2012/happyacs50005.png)