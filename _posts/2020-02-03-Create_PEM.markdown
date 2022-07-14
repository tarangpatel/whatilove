---
title: Create PEM Certificate
categories: [tools, certificates]
tags: [iOS, Push Notification, Certififates, PEM]
image: images/05.jpg
---

- Export certificate and private key separately. First, export the certificate by right-clicking it and choosing "Export".

- Select a name (e.g. apns-cert.p12) and choose .p12 as format.

- When prompted for a password, leave it blank. When prompted for a system password, provide your OSX user
  password.

- Perform steps b-d for the private key. Select a name (e.g. apns-key.p12)

- Converting .p12 Certificate and .p12 Private Key files into a single .pem file. Execute the following commands in
  Terminal after navigating to the folder containing both, the certificate .p12 and key .p12 files:

- Convert certificate .p12 file into .pem file. When prompted for a password, simply press enter since no password should have been given when exporting from keychain.

  {% highlight swift %}
  openssl pkcs12 -clcerts -nokeys -out apns-cert.pem -in apns-cert.p12
  {% endhighlight %}

- Convert key .p12 file into .pem file. When prompted for a password, simply press enter since no password should have been given when exporting from keychain. When prompted to "Enter PEM pass phrase", enter pass phrase of your choice, e.g. 1234.
  {% highlight swift %}
  openssl pkcs12 -nocerts -out apns-key.pem -in apns-key.p12
  {% endhighlight %}

- Remove encryption from key .pem file. Enter pass phrase from previous step when prompted to "Enter pass phrase".

  {% highlight swift %}
  openssl rsa -in apns-key.pem -out apns-key-noenc.pem
  {% endhighlight %}

- Merge certificate and key .pem file into one single .pem file:

  {% highlight swift %}
  cat apns-cert.pem apns-key-noenc.pem > apns-prod.pem
  {% endhighlight %}

- Upload to online services that will require it.
