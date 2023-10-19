
# MR- Integration Document

Examples of code to interact with MR API

### Requirements

- OpenSSL - *[Installation Guide](https://github.com/openssl/openssl)*

## Signature generation and validation

All examples imply that you have already generated ssl-rsa key-pair with such command:
```bash
openssl genrsa -out private_key.pem 2048
```
and extracted public key:
```bash
openssl rsa -in private_key.pem -pubout > public_key.pem
```
## General workflow

### **Signing:**

Prerequisite:
1. generate private and public key.
2. send public key to MR representative

Process:
1. sign request body with your private key
2. encode signature in base64
3. put result of step 2 into request header with key: ***<font color="yellow">mrbo-sig</font>***
4. send request

### **Validation of signature:**

Prerequisite: receive and save MR public key

Process:
1. receive request
2. get value from request header with key:  ***<font color="yellow">mrbo-sig</font>***
3. decode it from base64
4. check that result of step 3 is valid for combination of this request body and MR public key

## Examples

We have few code examples for generating the signature and it's validation. Also [`example`](./example) folder contains demo pair of private and public keys.

* Java

In below table you can find examples of data and corresponding signature(signed with private key from [resource](./resource) folder). Try to get same signatures and validate these signatures with [public key](./resource/public_key.pem)

| Data            | Signature                                                                                                                                                                                                                                                                                                                                                |
|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| {"test":"test"} | HPRO8VucedHjcj3pJq4Nzzw7lFDwS81GfLhpW1ypeD7P6nGdJ6tId7b8G2kwSJNtGG5efv2H7Jgpum9IFAUTC+jTUY+Y+8RB22wfbhx1NwP/ujLrxqodZWTX4Qo0etoCI9/VfbLuNF62lLOIypkLYC7CBuB841p8B5XZ1/PMawRcd4fsQo2XWLZaAXyph5D+HZw8GpFQu9sSzUWFYAfYYjwsOieGY4nI5DX0cuTQKEqbruNdiWhjDk4dt5AXf9dZN3a+oKWls5MwY3uQ77jLcnUBe+73mao9b/9vh8Uka1xtRVmXjUQhqMuLZncNcfEoZoR/+H0OVVd6d9LlCT5ciQ== |
| example         | WHpSemvBGo0kKxGMsUWkV1eztZPcL0m3AMDvBHCnG46TPwmG3qHYqVrdo9KKOMFGpJipwDTaKcf9vD0TsYMw1dZ8Xmu4UAGNeRL5BmtNwiA8tMxolXAnJHBJxT/1MfVFtTZxJrw0098uST1Gu0+YVP3Rs8T/emr0bI7y9ZI84PwqwGzidHgj8K2E7rNTvUgW7GXfPtkHO3+Difv+dxA9bIYt2QLclT/S5JAG2cojHugpC8ZaHpuCWcz3b0vzpFlOZK4Mq3BEuSU/5hZdZsnEH1T2QrHqco5oTAG+lY61qn7rJlGpL4FluZ3UMyBzQWZDQ+s20ore6Fxqn3mRB0Vd4g== |