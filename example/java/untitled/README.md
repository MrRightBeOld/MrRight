# Useful OpenSSL comands:

Generate a 2048-bit RSA private key

> `$ openssl genrsa -out private_key.pem 2048`

Generate a public key

> `$ openssl rsa -in private_key.pem -pubout > public_key.pem`
> 
Convert private Key to PKCS#8 format (so Java can read it)

> `$ openssl pkcs8 -topk8 -inform PEM -outform DER -in private_key.pem -out private_key.der -nocrypt`

Output public key portion in DER format (so Java can read it)

> `$ openssl rsa -in private_key.pem -pubout -outform DER -out public_key.der`

## Run application to test

Run [Cryptograpic application](./src/Cryptographic.java) to test and validate the string to sign.

Change the string *example* to your own string for testing in the main function

`String string_to_sign = "example";`

  