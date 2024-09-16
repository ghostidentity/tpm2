## Python ESAPI and FAPI examples


Ref: 

* [https://tpm2-pytss.readthedocs.io/en/latest/api.html](https://tpm2-pytss.readthedocs.io/en/latest/api.html)
* [/P_RSA2048SHA256.json](https://github.com/tpm2-software/tpm2-tss/blob/master/dist/fapi-profiles/P_RSA2048SHA256.json)
* [fapi-config](https://github.com/tpm2-software/tpm2-tss/blob/master/doc/fapi-config.md)

* [TSS_FAPI_v0p94_r09_pub.pdf](https://trustedcomputinggroup.org/wp-content/uploads/TSS_FAPI_v0p94_r09_pub.pdf)
* [TSS_JSON_Policy_v0p7_r08_pub](https://trustedcomputinggroup.org/wp-content/uploads/TSS_JSON_Policy_v0p7_r08_pub.pdf)

#### Install

```bash
apt-get install libtss2-dev
python3 -m pip install tpm2-pytss
```


### ESAPI

- `esapi_create_sign.py`: create rsa key and sign/verify
- `esapi_encrypt_decrypt.py`: create aes key and encrypt/decrypt
- `esapi_hmac_import.py`: import and use an hmac key
- `esapi_keyfile.py`: create and use PEM encoded keyfiles
- `esapi_auth.py`: create key with auth password
- `esapi_pcr.py`: create key with pcrpolicy

- `fapi_create_sign.py`: create rsa key and sign/verify
- `fapi_seal_unseal.py`: seal/unseal 
- `fapi_import_tpm2.py`: import pub/priv keys generated by tpm2tools into fapi contexts
- `fapi_export_tpm2.py`: export key fapi context to pub/priv blobs readable by tpm2tools
- `fapi_auth.py`: create key and bind to password auth with callback
- `fapi_pcr.py`: create key and bind to pcr policy

### Policy JSON

[JSON Data Types and Policy Language Specification](https://trustedcomputinggroup.org/resource/tcg-tss-json/)

### FAPI Session Encryption

From : [TCG_CPU_TPM_Bus_Protection_Guidance_Passive_Attack_Mitigation](https://trustedcomputinggroup.org/wp-content/uploads/TCG_CPU_TPM_Bus_Protection_Guidance_Passive_Attack_Mitigation_8May23-3.pdf)

```
• Application developers typically use the high-level TCG Feature API (FAPI) [3]. A compliant TSS
implementation of FAPI automatically encrypts commands and responses, and no work is required by
application developers.
```


```bash
rm -rf ~/.local/share/tpm2-tss/
rm -rf /tmp/myvtpm && mkdir /tmp/myvtpm
sudo swtpm_setup --tpmstate /tmp/myvtpm --tpm2 --create-ek-cert 
sudo swtpm socket --tpmstate dir=/tmp/myvtpm --tpm2 --server type=tcp,port=2321 --ctrl type=tcp,port=2322 --flags not-need-init,startup-clear  --log level=5

export TPM2TOOLS_TCTI="swtpm:port=2321"
export TPM2OPENSSL_TCTI="swtpm:port=2321"

tpm2_flushcontext -t && tpm2_flushcontext -s && tpm2_flushcontext -l
```