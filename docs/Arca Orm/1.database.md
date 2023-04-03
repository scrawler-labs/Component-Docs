# Database and Drivers

## Database class
`\Scrawler\Arca\Database` serves as a entry point for Arca, it provides you with all the utility functions from model creation to advance things like table manager. The most basic function of this class is to connect with database and creating/getting models.

To initialise database you need to pass the appropriate drivers and all details required by that driver.

```php

// Basic Setup 
    $connectionParams = array(
        'dbname' => 'YOUR_DB_NAME',
        'user' => 'YOUR_DB_USER',
        'password' => 'YOUR_DB_PASSWORD',
        'host' => 'YOUR_DB_HOST',
        'driver' => 'pdo_mysql', //You can use other supported driver this is the most basic mysql driver
    );

    $db =  new \Scrawler\Arca\Database($connectionParams);

// create a model
$user = $db->create('user');
$user->name = 'Pranjal Pandey';
$user->email = 'therealpranjal@gmail.com';
$user->save();

// retrive single model via id 
$user = $db->get('user',1);

// retrive all models (collection) from table
$user = $db->get('user');

```
## Supported databases
- MySQL
- Oracle
- Microsoft SQL Server
- PostgreSQL
- SQLite

## Drivers

Arca support a lot of database and drivers, here is a list of some built in drivers:

- pdo_mysql: A MySQL driver that uses the pdo_mysql PDO extension.
- mysqli: A MySQL driver that uses the mysqli extension.
- pdo_sqlite: An SQLite driver that uses the pdo_sqlite PDO extension.
- pdo_pgsql: A PostgreSQL driver that uses the pdo_pgsql PDO extension.
- pdo_sqlsrv: A Microsoft SQL Server driver that uses pdo_sqlsrv PDO
- sqlsrv: A Microsoft SQL Server driver that uses the sqlsrv PHP extension.
- oci8: An Oracle driver that uses the oci8 PHP extension.

Here is configuration parameters for each drivers:

### pdo_mysql
- user (string): Username to use when connecting to the database.
- password (string): Password to use when connecting to the database.
- host (string): Hostname of the database to connect to.
- port (integer): Port of the database to connect to.
- dbname (string): Name of the database/schema to connect to.
- unix_socket (string): Name of the socket used to connect to the database.
- charset (string): The charset used when connecting to the database.

### mysqli
- user (string): Username to use when connecting to the database.
- password (string): Password to use when connecting to the database.
- host (string): Hostname of the database to connect to.
- port (integer): Port of the database to connect to.
- dbname (string): Name of the database/schema to connect to.
- unix_socket (string): Name of the socket used to connect to the database.
- charset (string): The charset used when connecting to the database.
- ssl_key (string): The path name to the key file to use for SSL encryption.
- ssl_cert (string): The path name to the certificate file to use for SSL encryption.
- ssl_ca (string): The path name to the certificate authority file to use for SSL encryption.
- ssl_capath (string): The pathname to a directory that contains trusted SSL CA certificates in PEM format.
- ssl_cipher (string): A list of allowable ciphers to use for SSL encryption.
- driverOptions Any supported flags for mysqli found on [http://www.php.net/manual/en/mysqli.real-connect.php](http://www.php.net/manual/en/mysqli.real-connect.php)

### pdo_sqlite
- user (string): Username to use when connecting to the database.
- password (string): Password to use when connecting to the database.
- path (string): The filesystem path to the database file. Mutually exclusive with memory. path takes precedence.
- memory (boolean): True if the SQLite database should be in-memory (non-persistent). Mutually exclusive with path. path takes precedence.

### pdo_pgsql
- user (string): Username to use when connecting to the database.
- password (string): Password to use when connecting to the database.
- host (string): Hostname of the database to connect to.
- port (integer): Port of the database to connect to.
- dbname (string): Name of the database/schema to connect to.
- charset (string): The charset used when connecting to the database.
- default_dbname (string): Override the default database (postgres) to connect to.
- sslmode (string): Determines whether or with what priority a SSL TCP/IP connection will be negotiated with the server. See the list of available modes: [https://www.postgresql.org/docs/9.4/static/libpq-connect.html#LIBPQ-CONNECT-SSLMODE](https://www.postgresql.org/docs/9.4/static/libpq-connect.html#LIBPQ-CONNECT-SSLMODE)
- sslrootcert (string): specifies the name of a file containing SSL certificate authority (CA) certificate(s). If the file exists, the server's certificate will be verified to be signed by one of these authorities. See [https://www.postgresql.org/docs/9.4/static/libpq-connect.html#LIBPQ-CONNECT-SSLROOTCERT](https://www.postgresql.org/docs/9.4/static/libpq-connect.html#LIBPQ-CONNECT-SSLROOTCERT)
- sslcert (string): specifies the filename of the client SSL certificate. See [https://www.postgresql.org/docs/9.4/static/libpq-connect.html#LIBPQ-CONNECT-SSLCERT](https://www.postgresql.org/docs/9.4/static/libpq-connect.html#LIBPQ-CONNECT-SSLCERT)
- sslkey (string): specifies the location for the secret key used for the client certificate. See [https://www.postgresql.org/docs/9.4/static/libpq-connect.html#LIBPQ-CONNECT-SSLKEY](https://www.postgresql.org/docs/9.4/static/libpq-connect.html#LIBPQ-CONNECT-SSLKEY)
- sslcrl (string): specifies the filename of the SSL certificate revocation list (CRL). See [https://www.postgresql.org/docs/9.4/static/libpq-connect.html#LIBPQ-CONNECT-SSLCRL](https://www.postgresql.org/docs/9.4/static/libpq-connect.html#LIBPQ-CONNECT-SSLCRL)
- application_name (string): Name of the application that is connecting to database. Optional. It will be displayed at pg_stat_activity.

### pdo_sqlsrv / sqlsrv
- user (string): Username to use when connecting to the database.
- password (string): Password to use when connecting to the database.
- host (string): Hostname of the database to connect to.
- port (integer): Port of the database to connect to.
- dbname (string): Name of the database/schema to connect to.

### oci8
- user (string): Username to use when connecting to the database.
- password (string): Password to use when connecting to the database.
- host (string): Hostname of the database to connect to.
- port (integer): Port of the database to connect to.
- dbname (string): Name of the database/schema to connect to.
- servicename (string): Optional name by which clients can connect to the database instance. Will be used as Oracle's SID connection parameter - if given and defaults to Doctrine's dbname connection parameter value.
- service (boolean): Whether to use Oracle's SERVICE_NAME connection parameter in favour of SID when connecting. The value for this will be read from Doctrine's servicename if given, dbname otherwise.
- pooled (boolean): Whether to enable database resident connection pooling.
- charset (string): The charset used when connecting to the database.
- instancename (string): Optional parameter, complete whether to add the INSTANCE_NAME parameter in the connection. It is generally used to connect to an Oracle RAC server to select the name of a particular instance.
- connectstring (string): Complete Easy Connect connection descriptor, see https://docs.oracle.com/database/121/NETAG/naming.htm. When using this option, you will still need to provide the user and password parameters, but the other parameters will no longer be used. Note that when using this parameter, the getHost and getPort methods from Doctrine\DBAL\Connection will no longer function as expected.
- persistent (boolean): Whether to establish a persistent connection.
