Cassandra Client-Node SSL with JDBC driver
===========

This folder contains the resources needed to enable SSL in a cassandra node. The SSL connectivity has been tested with CQLSH but with JDBC driver it fails.
The possible reason being a required enhancement missing: https://github.com/zhicwu/cassandra-jdbc-driver/issues/10

Contents
====================
[cassandra.yaml](https://github.com/narendrans/cassandra-jdbc-driver/blob/master/resources/ssl/cassandra.yaml) - If you install cassandra from a package, it will be located by default in `/etc/cassandra/cassandra.yaml`
```
client_encryption_options:
    enabled: true
    # If enabled and optional is set to true encrypted and unencrypted connections are handled.
    optional: false
    keystore: /mnt/c/denodo/dev/ssl/keystore.node0
    keystore_password: cassandra

    require_client_auth: false
    # Set trustore and truststore_password if require_client_auth is true
    truststore: /mnt/c/denodo/dev/ssl/truststore.node0
    truststore_password: cassandra
    protocol: TLS
    algorithm: SunX509
    store_type: JKS
    cipher_suites: [TLS_RSA_WITH_AES_256_CBC_SHA]
```

[cqlshrc](https://github.com/narendrans/cassandra-jdbc-driver/blob/master/resources/ssl/cqlshrc) - This file contains the settings needed to connect from CQLSH tool. 
Only the SSL part is needed.
```
[authentication]
username =
password =

[connection]
hostname = localhost
port = 9042
#factory = cqlshlib.ssl.ssl_transport_factory

[ssl]
certfile = /mnt/c/denodo/dev/ssl/node0.cer.pem
validate = true
```
