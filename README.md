# docker-cloudsql

A utility that helps manage a Docker container running Google's Cloud SQL Proxy, which allows you to connect to a Cloud SQL instance from your local machine. For more information about the proxy, see:

* https://cloud.google.com/sql/docs/postgres/connect-docker
* https://cloud.google.com/sql/docs/mysql/sql-proxy

---

## Installation

To install this utility, run the following command:

```
curl -sL https://raw.githubusercontent.com/marksost/docker-cloudsql/master/install.sh | bash
```

Which will download and make executable the `docker-cloudsql` bash script contained within repository.

**NOTE**: The above command will download the script into your current working directory. You may want to move it afterwards to a directory in your path, such as `/usr/local/bin`.

## Usage

There are two required parameters that this utility needs, passed in as command line flags. They are: `-c` and `-i`.

The `-c` flag should contain the full path to a Cloud SQL service account crednetials JSON file. For more information about how to set up a service account for Cloud SQL and the permissions required for the account, take a look at [this tutorial](https://cloud.google.com/sql/docs/postgres/connect-docker), specifically step 6.

The `-i` flag should contain the full connection name of the Cloud SQL instance to proxy connections to. This name takes the form of:

```
<GCP project ID>:<region>:<Cloud SQL instance name>
```

The last argument passed to the utility is the command to run. Currently this utility supports the following commands:

* status - Prints the status of the Cloud SQL proxy
* start - Starts the Cloud SQL proxy
* stop - Stops the Cloud SQL proxy
* restart - Restarts the Cloud SQL proxy
* update - Pulls the latest image for the Cloud SQL proxy

### Example

```
$ docker-cloudsql -c /path/to/creds.json -i test-project-1234:us-central1:test-postgres-instance start

>> Executing docker-cloudsql with the following settings:
>>   Credentials file: /path/to/creds.json
>>   Cloud SQL instance connection name: test-project-1234:us-central1:test-postgres-instance
>>   Proxy flavor: postgres
>>   Proxy port: 5432
>>   Container name: cloudsql-proxy-postgres
>> Starting container...

>> 553ec919c41dede14ae8a3da99aaea430ecdf7de9291b4341cc2c43cfee24139

>> Cloud SQL proxy docker container started successfully!
```
