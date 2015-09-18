To get started quickly:
  1. Add your hosts to the hostsToTrust String array.
  1. Call CustomTrustManager.initSsl().
  1. Make SSL connections to your hosts.

This is a TrustManager for Java that allows you to connect to sites that you trust that have self signed certs.  It also uses the built in PKIX cert chain verification against CA certs that comes with your Java installation so you don't have to completely throw out all SSL host verification.

After searching the web for an easy, secure way to trust an SSL site that has a self-signed certificate and finding very little in concrete, useful implementations, I decided to create a TrustManager that allows you to do this easily.  Many implementations are too simplistic and throw out the checks for valid certs on other sites.  Others don't give you an easy way to add certificates.  The most useful implementation (http://code.google.com/p/java-use-examples/source/browse/trunk/src/com/aw/ad/util/InstallCert.java) writes to the CA cert keystore that comes with Java.  That doesn't work when you're working with a server installation that requires Java to run as root/Administrator to make the changes.

Specify additional hosts to trust in the hostsToTrust member variable and call the static method initSsl().  This will add the certificates from those hosts to the certificates already in the CA trust store and make them available for consequent HTTPS connections.  The new trust store is kept in memory only in case you don't have the rights to write back to the CA certificate store that comes with Java.