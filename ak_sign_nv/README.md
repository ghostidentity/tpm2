Sign with AK saved to NV


https://pkg.go.dev/github.com/google/go-tpm-tools/client#EndorsementKeyFromNvIndex




for GCE VMs

```golang
const (
	tpmDevice             = "/dev/tpm0"
	signCertNVIndex       = 0x01c10000
	signKeyNVIndex        = 0x01c10001
	encryptionCertNVIndex = 0x01c00002
	emptyPassword         = ""
)
```

---

```bash
# go run main.go 

2022/09/19 16:41:52 ======= Init  ========
2022/09/19 16:41:52 0 handles flushed
2022/09/19 16:41:52      Load SigningKey and Certifcate 
2022/09/19 16:41:52      Signing PEM 
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAti9OxVJdynQP8T1jz4wK
gjSs+LNxpbYp94bOnkSoLg7Zd3RcMfy4863mvVkYZ8FLSfLyXxZV8hgNfUYd91or
sZ09Q1TqQjsKPtCUi6MSxGhCyIRLj7xZt3and5OyrFU2D/KKTdPOePys4NQeQM6s
UdOX/h4jrrFRQIYW7sdKVggxV5RTl//vPRLxdge1TjIYaPlRzVKSXf70GtRpwUrE
nR2cx6e81qp82rjh5GCBmTkdCIV8iJkEPVVOF3/1VveefymBoavK4wq1j7kd9Nj2
lvxGwU83DXitpM0uVPAmkC6ULGwBuC63AbvVwsXeUBt9Rt+0SaRk7I4SAhbXqO9A
YQIDAQAB
-----END PUBLIC KEY-----
2022/09/19 16:41:52      AK Signed Data using go-tpm-tools krLYr99i6qTlB+UZ1bQ0pJUPooWW7IQD7lQ+5Fp+pmEp47UnBMK+TZkeH7ATGeVrXYY4bsPix/+f8p1DoTXObcSQZVZNdEEsBofCKULkUKZ5doggtl17zNWzKnjl6jjIr7criEOLRNZXVQZR/AckBZQIWWZ7ZO8unaHkoOXWlF6CIUdOaYIm0nuPGRrwmL5G15CTAUGeudIwMJBb7qZt2WaTyPddeUOzN4KsEuRfYXQpeRUNfcTcNMPiZENj5fNEUybviOTb8XW05e2ZhdD4DFBVyzaZ9lK3VnYICDHfWngnipO3LMWC+aJjei1C2CVnuHvhEsNPxdFDQfh5NPQ53w==
2022/09/19 16:41:52      AK Issued Hash w6uP8Tcg6K2QR905Rms8iXTlksL6OD1KOWBxTK7wxPI=
2022/09/19 16:41:52      AK Signed Data krLYr99i6qTlB+UZ1bQ0pJUPooWW7IQD7lQ+5Fp+pmEp47UnBMK+TZkeH7ATGeVrXYY4bsPix/+f8p1DoTXObcSQZVZNdEEsBofCKULkUKZ5doggtl17zNWzKnjl6jjIr7criEOLRNZXVQZR/AckBZQIWWZ7ZO8unaHkoOXWlF6CIUdOaYIm0nuPGRrwmL5G15CTAUGeudIwMJBb7qZt2WaTyPddeUOzN4KsEuRfYXQpeRUNfcTcNMPiZENj5fNEUybviOTb8XW05e2ZhdD4DFBVyzaZ9lK3VnYICDHfWngnipO3LMWC+aJjei1C2CVnuHvhEsNPxdFDQfh5NPQ53w==
2022/09/19 16:41:52      Signature Verified
```


Note the signingKey public cert is matches the one derived from the ek in NVRAM

```
$ gcloud compute instances get-shielded-identity instance-1
encryptionKey:
  ekCert: |
    -----BEGIN CERTIFICATE-----
    MIIFMjCCBBqgAwIBAgITAbWVqg51HbFjiPBfeNh6jor1ETANBgkqhkiG9w0BAQsF
    ADCBuTELMAkGA1UEBhMCVVMxEzARBgNVBAgTCkNhbGlmb3JuaWExFjAUBgNVBAcT
    DU1vdW50YWluIFZpZXcxEzARBgNVBAoTCkdvb2dsZSBMTEMxDjAMBgNVBAsTBUNs
    b3VkMVgwVgYDVQQDDE90cG1fZWtfdjFfY2xvdWRfaG9zdC1zaWduZXItMC0yMDIw
    LTEwLTIyVDE0OjAyOjA4LTA3OjAwIEs6MSwgMjpIQk5wQTNUUEFiTTowOjE4MCAX
    DTIxMDkxNzE1MDI1M1oYDzIwNTEwOTEwMTUwNzUzWjAAMIIBIjANBgkqhkiG9w0B
    AQEFAAOCAQ8AMIIBCgKCAQEAwz3ojgM5gcGYC9kcGbgtrTjhPcfsLNddlZ6qYiwT
    i3qpiF0SGW4i7o8Jlq+Epc7DR7vLGb7XGooW0K2NaMXU3jbsLCB9qOuk6Uv4rOvj
    kPsOIQ+sT8UuIQYH2oFmFpoka9siMCtDuZwWlXOXzCAPyZgrn3t3s8qFcCJuQbRq
    K6B+OfTFrpaNZip0+V7T/QwFZbYWhK8zI4FKb3G9BTIswy6iOMJs8gucFjb2X1qe
    08X15BAATIXabRfseSa4g4W3W7+9AXvo9ZuTI2MOpd2qR4tcR20DwVWEDHB7lvHP
    RBVa5kSYPmfHixuPu3qOQ5iFPAlUwrF4Kl4UkeARmJ9WsQIDAQABo4IB5zCCAeMw
    DAYDVR0TAQH/BAIwADAfBgNVHSMEGDAWgBQTzXG6WLIKUaMoDmW5lp67HQ0RkzBW
    BggrBgEFBQcBAQRKMEgwRgYIKwYBBQUHMAKGOmh0dHBzOi8vcGtpLmdvb2cvY2xv
    dWRfaW50ZWdyaXR5L3RwbV9la19pbnRlcm1lZGlhdGVfMi5jcnQwSwYDVR0fBEQw
    QjBAoD6gPIY6aHR0cHM6Ly9wa2kuZ29vZy9jbG91ZF9pbnRlZ3JpdHkvdHBtX2Vr
    X2ludGVybWVkaWF0ZV8yLmNybDAOBgNVHQ8BAf8EBAMCBSAwEAYDVR0lBAkwBwYF
    Z4EFCAEwIgYDVR0JBBswGTAXBgVngQUCEDEOMAwMAzIuMAIBAAICAI4wUQYDVR0R
    AQH/BEcwRaRDMEExFjAUBgVngQUCAQwLaWQ6NDc0RjRGNDcxDzANBgVngQUCAgwE
    dlRQTTEWMBQGBWeBBQIDDAtpZDoyMDE2MDUxMTB0BgorBgEEAdZ5AgEVBGYwZAwN
    dXMtY2VudHJhbDEtYQIGAPltg2V0DBNtaW5lcmFsLW1pbnV0aWEtODIwAghwPVe4
    v+kR0AwKaW5zdGFuY2UtMaAgMB6gAwIBAKEDAQH/ogMBAQCjAwEBAKQDAQEApQMB
    AQAwDQYJKoZIhvcNAQELBQADggEBAHbWCz4wOnW2VhWxCWsxwO4Nz2j0ajy02JSc
    WAfYN4/yJm0ggiRXax8wYHzTCFOYWSjhx1VK2ih2rh38/gPWCWB4IzlUEPFtorPT
    tZniqtb58I/Ahf0Vj18K5PfjaOvQLjQP/OZnGcDcopgqJtxZugPArgshftyP3LHx
    AMcw30yQODM2jU7AGds+E0emizHEknQNLZRhMnmEHI3qe/xUU/hNR3oU0BpsoLh0
    sI3SS+VQddw0aIoCbbr7c+DnjQaPJI2XyJGrIEIfwvSORCAEbTDwk9Buo2zgcN/3
    LWhhd73AvwuP+K3tNCdg6t/b+bIHXgIdivCKzPFMPyPLAY3p078=
    -----END CERTIFICATE-----
  ekPub: |
    -----BEGIN PUBLIC KEY-----
    MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAwz3ojgM5gcGYC9kcGbgt
    rTjhPcfsLNddlZ6qYiwTi3qpiF0SGW4i7o8Jlq+Epc7DR7vLGb7XGooW0K2NaMXU
    3jbsLCB9qOuk6Uv4rOvjkPsOIQ+sT8UuIQYH2oFmFpoka9siMCtDuZwWlXOXzCAP
    yZgrn3t3s8qFcCJuQbRqK6B+OfTFrpaNZip0+V7T/QwFZbYWhK8zI4FKb3G9BTIs
    wy6iOMJs8gucFjb2X1qe08X15BAATIXabRfseSa4g4W3W7+9AXvo9ZuTI2MOpd2q
    R4tcR20DwVWEDHB7lvHPRBVa5kSYPmfHixuPu3qOQ5iFPAlUwrF4Kl4UkeARmJ9W
    sQIDAQAB
    -----END PUBLIC KEY-----
kind: compute#shieldedInstanceIdentity
signingKey:
  ekCert: |
    -----BEGIN CERTIFICATE-----
    MIIFMjCCBBqgAwIBAgITATvpjlUxE5jt4EjklNN635sHaDANBgkqhkiG9w0BAQsF
    ADCBuTELMAkGA1UEBhMCVVMxEzARBgNVBAgTCkNhbGlmb3JuaWExFjAUBgNVBAcT
    DU1vdW50YWluIFZpZXcxEzARBgNVBAoTCkdvb2dsZSBMTEMxDjAMBgNVBAsTBUNs
    b3VkMVgwVgYDVQQDDE90cG1fZWtfdjFfY2xvdWRfaG9zdC1zaWduZXItMC0yMDIw
    LTEwLTIyVDE0OjAyOjA4LTA3OjAwIEs6MSwgMjpIQk5wQTNUUEFiTTowOjE4MCAX
    DTIxMDkxNzE1MDI1M1oYDzIwNTEwOTEwMTUwNzUzWjAAMIIBIjANBgkqhkiG9w0B
    AQEFAAOCAQ8AMIIBCgKCAQEAti9OxVJdynQP8T1jz4wKgjSs+LNxpbYp94bOnkSo
    Lg7Zd3RcMfy4863mvVkYZ8FLSfLyXxZV8hgNfUYd91orsZ09Q1TqQjsKPtCUi6MS
    xGhCyIRLj7xZt3and5OyrFU2D/KKTdPOePys4NQeQM6sUdOX/h4jrrFRQIYW7sdK
    VggxV5RTl//vPRLxdge1TjIYaPlRzVKSXf70GtRpwUrEnR2cx6e81qp82rjh5GCB
    mTkdCIV8iJkEPVVOF3/1VveefymBoavK4wq1j7kd9Nj2lvxGwU83DXitpM0uVPAm
    kC6ULGwBuC63AbvVwsXeUBt9Rt+0SaRk7I4SAhbXqO9AYQIDAQABo4IB5zCCAeMw
    DAYDVR0TAQH/BAIwADAfBgNVHSMEGDAWgBQTzXG6WLIKUaMoDmW5lp67HQ0RkzBW
    BggrBgEFBQcBAQRKMEgwRgYIKwYBBQUHMAKGOmh0dHBzOi8vcGtpLmdvb2cvY2xv
    dWRfaW50ZWdyaXR5L3RwbV9la19pbnRlcm1lZGlhdGVfMi5jcnQwSwYDVR0fBEQw
    QjBAoD6gPIY6aHR0cHM6Ly9wa2kuZ29vZy9jbG91ZF9pbnRlZ3JpdHkvdHBtX2Vr
    X2ludGVybWVkaWF0ZV8yLmNybDAOBgNVHQ8BAf8EBAMCB4AwEAYDVR0lBAkwBwYF
    Z4EFCAEwIgYDVR0JBBswGTAXBgVngQUCEDEOMAwMAzIuMAIBAAICAI4wUQYDVR0R
    AQH/BEcwRaRDMEExFjAUBgVngQUCAQwLaWQ6NDc0RjRGNDcxDzANBgVngQUCAgwE
    dlRQTTEWMBQGBWeBBQIDDAtpZDoyMDE2MDUxMTB0BgorBgEEAdZ5AgEVBGYwZAwN
    dXMtY2VudHJhbDEtYQIGAPltg2V0DBNtaW5lcmFsLW1pbnV0aWEtODIwAghwPVe4
    v+kR0AwKaW5zdGFuY2UtMaAgMB6gAwIBAKEDAQH/ogMBAQCjAwEBAKQDAQEApQMB
    AQAwDQYJKoZIhvcNAQELBQADggEBAG2WSu+2TVcBjRP23hUsHDfo9893+1GiVzZv
    Zxw65tIiqjOp1fFHPH+ucqFmdT+pS4doI13zmt5p2qomxOqL9GBcOvQfH2BrJcEI
    9YavgEf6F2xgafq92dLsWcIl++WyP4q8MG73JhfjwJhE4hYOiDtyPtmHxegyueDr
    6TgDE4o/zepP/4TtumR9bK996oIzEJZStF7/sFiorB7DD0CTFN4RiunSJxmMRkA5
    yKLQ6JVYrD308XIhE9zlXRwXbQLKg6FqlST0BE4hi24TxHd5yCOxz6aM/vRUIq/5
    Gs3Pu4pwcYz30veuFCJij/Thlq71Ekky/Szr7EM3yrcGs+xNXlY=
    -----END CERTIFICATE-----
  ekPub: |
    -----BEGIN PUBLIC KEY-----
    MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAti9OxVJdynQP8T1jz4wK
    gjSs+LNxpbYp94bOnkSoLg7Zd3RcMfy4863mvVkYZ8FLSfLyXxZV8hgNfUYd91or
    sZ09Q1TqQjsKPtCUi6MSxGhCyIRLj7xZt3and5OyrFU2D/KKTdPOePys4NQeQM6s
    UdOX/h4jrrFRQIYW7sdKVggxV5RTl//vPRLxdge1TjIYaPlRzVKSXf70GtRpwUrE
    nR2cx6e81qp82rjh5GCBmTkdCIV8iJkEPVVOF3/1VveefymBoavK4wq1j7kd9Nj2
    lvxGwU83DXitpM0uVPAmkC6ULGwBuC63AbvVwsXeUBt9Rt+0SaRk7I4SAhbXqO9A
    YQIDAQAB
    -----END PUBLIC KEY-----


```