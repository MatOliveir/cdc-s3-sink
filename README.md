# cdc-s3-sink
Change Data Capture with AWS S3 as target

### Steps to work
1. Create user in AWS with S3 Full Access
2. Create an access key to this user
3. Put the access credentials in a .env file - use the .env_template file to help
4. Create a bucket in S3 - in my example i created a bucket called cdc-s3-sink in us-east-1 region. You can create a bucket with the name and region that you want, but you will need to change the s3.bucket.name and s3.region configs in docker container kafka_connect_sink

### Considerations
1. I'm running a docker container to MySQL server, if you want to use other MySQL server, you will need to change the database.hostname config in docker container kafka_connect_source as well the others configs about the MySQL server. You will need to make some configures in MySQL server too, for more informations please visit [debezium documentation - MySQL connector](https://debezium.io/documentation/reference/2.3/connectors/mysql.html#setting-up-mysql)
2. I'm saving the files in parquet format, but you can change the format to Json, Avro or ByteArray