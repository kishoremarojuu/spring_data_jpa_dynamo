# spring_data_jpa_dynamo

Dynamo DB provides the jar to be downloaded locally and work with Dynamo Db
Method1:

1.Refer this link to download the jar to the local ->https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DynamoDBLocal.html

2.go to the jar location and run the following command 
D:\SomeDrive\programs\18.AWS\DynamoDBLocalJar>java -Djava.library.path=./DynamoDBLocal_lib -jar DynamoDBLocal.jar -sharedDb

3.Set up Amazon CLI in windows, Refer ->https://docs.aws.amazon.com/cli/latest/userguide/awscli-install-windows.html
4.Configure the AWS 
C:\Users\kishore****>aws configure
AWS Access Key ID [****************XNGQ]: ********************
AWS Secret Access Key [****************5TGC]: ***********************************
Default region name [None]: us-west-2
Default output format [None]:

5.Dynamo DB will run in the background, check the URL 
http://localhost:8000/shell/#

6.Create the table from CLI 
D:\SomeDrive\programs\18.AWS\DynamoDBLocalJar>aws dynamodb create-table --table-name Customer --attribute-definitions AttributeName=Id,AttributeType=S --key-schema AttributeName=Id,KeyType=HASH --provisioned-throughput ReadCapacityUnits=1,WriteCapacityUnits=1 --endpoint-url http://localhost:8000
Dynamo DB will keep on running, press ctrl+c to stop the local instance of the server 

Application.properties in spring boot app
security.user.name=************* 
security.user.password=*****************
amazon.dynamodb.endpoint=http://localhost:8000/
amazon.aws.accesskey=********************
amazon.aws.secretkey=****************************************

7.D:\SomeDrive\programs\18.AWS\DynamoDBLocalJar>aws dynamodb list-tables --endpoint-url http://localhost:8000/shell
8.run the spring boot application, check the rest URL's 


-------------------------------------------------------------------------------------------------------------
Method2:
Without running the local instance of the jar, you can still save the data in the remote directly, 

Following upto 4 steps above
5.Application.properties in the spring boot application 
security.user.name=************* 
security.user.password=******************
amazon.dynamodb.endpoint=http://dynamodb.us-west-2.amazonaws.com
amazon.aws.accesskey=***********************
amazon.aws.secretkey=***********************

6.Check the list of already existing tables 
D:\SomeDrive\programs\18.AWS\DynamoDBLocalJar>aws dynamodb list-tables --endpoint-url http://dynamodb.us-west-2.amazonaws.com

7.Configure the VPC endpoint, Refer->https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/vpc-endpoints-dynamodb.html

8.Create the table from amazon CLI or directly create from amazon console
D:\SomeDrive\programs\18.AWS\DynamoDBLocalJar>aws dynamodb create-table --table-name Customer --attribute-definitions AttributeName=Id,AttributeType=S --key-schema AttributeName=Id,KeyType=HASH --provisioned-throughput ReadCapacityUnits=1,WriteCapacityUnits=1 --endpoint-url http://dynamodb.us-west-2.amazonaws.com

9.run the spring boot application, check the rest URL's 
