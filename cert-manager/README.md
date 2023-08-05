# How to configure local CA

> MacOS requires [additional openssl configuration](https://github.com/jetstack/cert-manager/issues/279#issuecomment-365827793) as described below.

1. Add following confgiuration to `/ect/ssl/openssl.cnf`

    ```text
    [ v3_ca ]
    basicConstraints = critical,CA:TRUE
    subjectKeyIdentifier = hash
    authorityKeyIdentifier = keyid:always,issuer:always
    ```

2. Generate key

    `openssl genrsa -out tls.key 4096`

3. Generate CA certificate

    `openssl req -x509 -new -nodes -key tls.key -sha256 -days 1024 -extensions v3_ca -out tls.crt`

4. Generate sealed secret

    ```sh
    kubectl -n cert-manager create secret generic ca-key-pair --from-file=tls.crt --from-file=tls.key --dry-run -o yaml | kubeseal -o yaml - > ca-sealed.yaml
    ```
