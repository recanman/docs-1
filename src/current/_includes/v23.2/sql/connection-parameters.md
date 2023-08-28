Flag | Description
-----|------------
<a name="sql-flag-url"></a> `--url` | A [connection URL]({% link {{ page.version.version }}/connection-parameters.md %}#connect-using-a-url) to use instead of the other arguments. To convert a connection URL to the syntax that works with your client driver, run [`cockroach convert-url`]({% link {{ page.version.version }}/connection-parameters.md %}#convert-a-url-for-different-drivers).<br><br>**Env Variable:** `COCKROACH_URL`<br>**Default:** no URL
`--host` | The server host and port number to connect to. This can be the address of any node in the cluster. <br><br>**Env Variable:** `COCKROACH_HOST`<br>**Default:** `localhost:26257`
`--port`<br><br>`-p` | The server port to connect to. Note: The port number can also be specified via `--host`. <br><br>**Env Variable:** `COCKROACH_PORT`<br>**Default:** `26257`
`--user`<br><br>`-u` | The [SQL user]({% link {{ page.version.version }}/create-user.md %}) that will own the client session.<br><br>**Env Variable:** `COCKROACH_USER`<br>**Default:** `root`
`--insecure` | Use an insecure connection.<br><br>**Env Variable:** `COCKROACH_INSECURE`<br>**Default:** `false`
`--cert-principal-map` | A comma-separated list of `<cert-principal>:<db-principal>` mappings. This allows mapping the principal in a cert to a DB principal such as `node` or `root` or any SQL user. This is intended for use in situations where the certificate management system places restrictions on the `Subject.CommonName` or `SubjectAlternateName` fields in the certificate (e.g., disallowing a `CommonName` like `node` or `root`). If multiple mappings are provided for the same `<cert-principal>`, the last one specified in the list takes precedence. A principal not specified in the map is passed through as-is via the identity function. A cert is allowed to authenticate a DB principal if the DB principal name is contained in the mapped `CommonName` or DNS-type `SubjectAlternateName` fields.
`--certs-dir` | The path to the [certificate directory]({% link {{ page.version.version }}/cockroach-cert.md %}) containing the CA and client certificates and client key.<br><br>**Env Variable:** `COCKROACH_CERTS_DIR`<br>**Default:** `${HOME}/.cockroach-certs/`