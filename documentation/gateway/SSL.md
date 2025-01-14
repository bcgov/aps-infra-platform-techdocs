---
order: -10000
---

# SSL Termination

If you would like to verify the SSL endpoint for `*.api.gov.bc.ca`, you can run the following two commands and compare the fingerprint and serial no.

```
export A_HOST=httpbin-regression.api.gov.bc.ca
openssl s_client -showcerts -verify 5 -connect 142.34.194.118:443 \
  -servername ${A_HOST} < /dev/null | awk '/BEGIN/,/END/{ if(/BEGIN/){a++}; print}' > gw.crt

openssl x509 -in gw.crt -fingerprint -serial -dates -noout

```

## \*.api.gov.bc.ca

| Issue Date  | Expires     | Deployed    | SHA1 Fingerprint                                            | Serial No.   |
| ----------- | ----------- | ----------- | ----------------------------------------------------------- | ------------ |
| Oct 6 2020  | Oct 16 2021 | Oct 6 2020  | 20:7D:15:9D:42:BE:CC:BC:FD:EF:DF:13:77:C7:25:A3:A4:72:45:05 | 7876EB597E14 |
| Feb 16 2021 | Oct 16 2021 | Feb 25 2021 | 4D:EA:CE:C4:0A:73:67:D3:B4:03:F6:63:C4:E1:67:2C:47:9D:EA:82 | 3B5849D8A670 |
| Sep 27 2021 | Oct 16 2022 | Oct 6 2021  | E3:DF:EC:89:BC:03:9B:E9:7D:57:91:EB:52:18:59:46:AA:A9:3A:15 | 1B588948FBB2 |
| Sep 28 2022 | Oct 16 2023 | TBD | 2D:E5:32:16:C6:0A:0D:F4:0C:1F:39:DD:BD:DD:A8:1A:51:4C:2D:94 | 34A6625E5ECF4E734BA6C4CF198F99B9 |

You can run the above as one line:

```
A_HOST=httpbin-regression.api.gov.bc.ca; openssl s_client -showcerts -verify 5 -connect ${A_HOST}:443 -servername ${A_HOST} < /dev/null | awk '/BEGIN/,/END/{ if(/BEGIN/){a++}; print}' | openssl x509 -fingerprint -serial -dates -noout
```

## Internal Notes

**Individual File Verification**

```
openssl x509 -in data-api-wildcard-2020.crt -fingerprint -serial -dates -noout
openssl x509 -in data-api-wildcard-2021.crt -fingerprint -serial -dates -noout
```

**Cert/Key Verification**

```
openssl x509 -noout -modulus -in data-api-wildcard.crt | openssl md5
openssl rsa -noout -modulus -in data-api-wildcard.key | openssl md5
```
