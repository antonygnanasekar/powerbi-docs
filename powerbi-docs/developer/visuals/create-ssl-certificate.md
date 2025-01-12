---
title: Create an SSL certificate
description: Work around instructions to create certificates manually for developer server
author: KesemSharabi
ms.author: kesharab
ms.reviewer: sranins
ms.service: powerbi
ms.subservice: powerbi-custom-visuals
ms.topic: tutorial
ms.date: 06/18/2019
---

# Create an SSL certificate

This article describes how to create an SSL certificate.

To generate the certificate by using the PowerShell `New-SelfSignedCertificate` cmdlet on Windows 8 or later, run the following command:

```cmd
pbiviz --create-cert
```

The tool requires an OpenSSL installation for Windows 7. The OpenSSL utility must be available from the command line.

To install OpenSSL, go to the [OpenSSL](https://www.openssl.org) or [OpenSSL Binaries](https://wiki.openssl.org/index.php/Binaries) site.



## Create a certificate (Mac OS X)

Usually, the OpenSSL utility is available in the Linux or Mac OS X operating system.

You can also install the utility by running either of the following commands:
* From the *Brew* package manager:

    ```cmd
    brew install openssl
    brew link openssl --force
    ```

* By using *MacPorts*:

    ```cmd
    sudo port install openssl
    ```

After you install the OpenSSL utility for generating a new certificate, run the following command:

```cmd
pbiviz --create-cert
```

## Create a certificate (Linux)

If the OpenSSL utility isn't available in your Linux operating system, you can install it by using one of the following commands:

* For *APT* package manager:

    ```cmd
    sudo apt-get install openssl
    ```

* For *Yellowdog Updater*:

    ```cmd
    yum install openssl
    ```

* For *Redhat Package Manager*:

    ```cmd
    rpm install openssl
    ```

If the OpenSSL utility is already available in your operating system, generate a new certificate by running the following command:

```cmd
pbiviz --create-cert
```

Or you can get the OpenSSL utility by going to the [OpenSSL](https://www.openssl.org) or [OpenSSL Binaries](https://wiki.openssl.org/index.php/Binaries) site.

## Generate the certificate manually

You can specify that your certificates be generated by any tools.

If the OpenSSL utility is already installed in your system, generate a new certificate by running the following commands:

```cmd
openssl req -x509 -newkey rsa:4096 -keyout PowerBICustomVisualTest_private.key -out PowerBICustomVisualTest_public.crt -days 365
```

You can usually find the PowerBI-visuals-tools web server certificates by running one the following:

* For the global instance of the tools:

    ```cmd
    %appdata%\npm\node_modules\PowerBI-visuals-tools\certs
    ```

* For the local instance of the tools:

    ```cmd
    <custom visual project root>\node_modules\PowerBI-visuals-tools\certs
    ```

If you use the PEM format, save the certificate file as *PowerBICustomVisualTest_public.crt*, and save privateKey as *PowerBICustomVisualTest_public.key*.

If you use the PFX format, save the certificate file as *PowerBICustomVisualTest_public.pfx*.

If your PFX certificate file requires a passphrase, do the following:
1. In the config file, specify:

    ```cmd
    \PowerBI-visuals-tools\config.json
    ```

1. In the `server` section, specify the passphrase by replacing the "*YOUR PASSPHRASE*" placeholder:

    ```cmd
    "server":{
        "root":"webRoot",
        "assetsRoute":"/assets",
        "privateKey":"certs/PowerBICustomVisualTest_private.key",
        "certificate":"certs/PowerBICustomVisualTest_public.crt",
        "pfx":"certs/PowerBICustomVisualTest_public.pfx",
        "port":"8080",
        "passphrase":"YOUR PASSPHRASE"
    }
    ```
