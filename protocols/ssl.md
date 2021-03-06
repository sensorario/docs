# SSL

## SSL wrapping protocol

SSL \(Secure Sockets Layer\) is not a communication protocol on its own and it is used as a wrapping for SSL-based secure protocols, like [SODEPS](https://github.com/jolielang/docs/tree/de0bcc5b82206ed6be6cb78fa10f6068bbe5881c/documentation/protocols/sodeps.html) and [HTTPS](https://github.com/jolielang/docs/tree/de0bcc5b82206ed6be6cb78fa10f6068bbe5881c/documentation/protocols/https.html).

## SSL Use

To make use of SSL, a valid private-key certificate deposited in a Java keystore is required. On the server side the two protocol parameters `.ssl.keyStore` pointing to the keystore file and `.ssl.keyStorePassword` in presence of a password need to be set.

Clients accessing SSL servers with unsafe \(including self-signed\) certificates usually deny operation. A truststore, likewise a Java keystore, contains trust entries also for potentially unsafe certificates. In Jolie it is specified over the protocol parameters `.ssl.trustStore` \(path\) and eventually `.ssl.trustStorePassword`.

Java's keytool helps to introspect key- and truststore: `keytool -list -keystore <keystore/truststore>.jks -storepass <password>`. In a keystore, a certificate with `PrivateKeyEntry` should be contained, in a truststore the same \(fingerprint\) with a `trustedCertEntry`.

## SSL Parameters

```text
type SSLConfiguration:void {
    .ssl?:void{

        /*
        * Defines the protocol used in encryption.
        *
        * Default: "TLSv1"
        * Supported values: all Java encryption protocols:
        * SSL, SSLv2, SSLv3, TLS, TLSv1, TLSv1.1, TLSv1.2
        */
        .protocol?:string

        /*
        * Defines the format used for storing
        * keys
        *
        * Default: "JKS"
        * Supported values: all java keystore formats:
        * JKS, JCEKS, PKCS12
        */
        .keyStoreFormat?:string

        /*
        * Defines the path of the file where keys are stored
        * 
        * Default: null
        */
        .keyStore?:string

        /*
        * Defines the password of the keystore
        *
        * Default: null
        */
        .keyStorePassword?:string

        /*
        * Defines the format used in the trustStore
        * 
        * Default: JKS 
        */
        trustStoreFormat?:string

        /*
        * Defines the path of the trustStore file
        * 
        * Default: null
        */
        .trustStore?:string

        /*
        * Defines the password of the trustStore
        * 
        * Default: none
        */
        .trustStorePassword?:string
    }
}
```

