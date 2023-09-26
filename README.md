# cdc-s3-sink
Change Data Capture with AWS S3 as target

<br>

### Prerequisites
1. An AWS account;
2. Docker installed;
3. Basic knowledge of SQL commands.

<br>

### Considerations
1. I'm running a docker container to MySQL server, if you want to use other MySQL server, you will need to change the database.hostname config in docker container kafka_connect_source as well the others configs about the database. You will need to make some configurations in MySQL server too, for more informations please visit [debezium documentation - MySQL connector](https://debezium.io/documentation/reference/2.3/connectors/mysql.html#setting-up-mysql);
2. I'm saving the files in parquet format, but you can change the format to json, avro or byte array, for that you will need to change the format.class config in docker container kafka_connect_sink.

<br>

### Steps to work
1. Create an user in AWS with S3 access - you can choose the AmazonS3FullAccess policy to make it easier;
2. Create an access key to this user;
3. Put the access credentials in a .env file - use the .env_template file to help;
4. Create a bucket in S3 - in my example I created a bucket called cdc-s3-sink in us-east-1 region. You can create a bucket with the name and region that you want, but you will need to change the s3.bucket.name and s3.region configs in docker container kafka_connect_sink;
5. Run the command bellow to start the containers and the cdc flow:

    ```sh
    docker-compose up -d
    ```

6. If the MySQL server chosen was in docker-compose.yml, run the commands bellow:

    ```sh
    docker exec -it mysql /bin/bash
    ```
    ```sh
    mysql -u root -p mysql123
    ```

7. Do the DDL and DML commands that you want and see the files arriving in S3.
