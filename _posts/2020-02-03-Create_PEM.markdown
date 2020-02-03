---
title: Create PEM Certificate
---

1. Export certificate and private key separately. First, export the certificate by right-clicking it and choosing "Export".

2. Select a name (e.g. apns-cert.p12) and choose .p12 as format.

3. When prompted for a password, leave it blank. When prompted for a system password, provide your OSX user
    password.

4. Perform steps b-d for the private key. Select a name (e.g. apns-key.p12)

5. Converting .p12 Certificate and .p12 Private Key files into a single .pem file. Execute the following commands in
    Terminal after navigating to the folder containing both, the certificate .p12 and key .p12 files:

6. Convert certificate .p12 file into .pem file

    {% highlight bash %}

    openssl pkcs12 -clcerts -nokeys -out apns-cert.pem -in apns-cert.p12

    {% endhighlight %}
     
    When prompted for a password, simply press enter since no password should have been given when exporting
    from keychain.

7. Convert key .p12 file into .pem file:

    {% highlight bash %}

    openssl pkcs12 -nocerts -out apns-key.pem -in apns-key.p12

    {% endhighlight %}  

    When prompted for a password, simply press enter since no password should have been given when exporting
    from keychain. When prompted to "Enter PEM pass phrase", enter pass phrase of your choice, e.g. 1234.

8. Remove encryption from key .pem file:

    {% highlight bash %}

    openssl rsa -in apns-key.pem -out apns-key-noenc.pem

    {% endhighlight %}  

    Enter pass phrase from previous step when prompted to "Enter pass phrase".

9. Merge certificate and key .pem file into one single .pem file:
    
    {% highlight bash %}

    cat apns-cert.pem apns-key-noenc.pem > apns-prod.pem
    
    {% endhighlight %}  

10. Upload to online services that will require it.
