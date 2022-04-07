### Serializing and deserializing Order objects
 
**Branch name:** dynamodbscanandserialization-prework

**AWS account:** (account number for your &lt;Alias&gt;ATAUnit5 account -- 
[find on Conduit](https://access.amazon.com/aws/accounts))
 
**role:** IibsAdminAccess-DO-NOT-DELETE
 
**RDE workfows:**
* `rde wflow run dynamodbscanandserialization-prework-serialize-orderserializertest`
 
Expected time required: 10 min
 
You have a database table, `OnlineUserOrders`, that keeps track of users' online orders and the cost of each order.
 
First, use CloudFormation to populate the table.

1. Make sure `ada` is running with the credentials specified at the top of this README
   (the AWS account that ATA set up for you for this unit). [Instructions on `ada` and `aws`
   command line interfaces](https://w.amazon.com/bin/view/Amazon_Technical_Academy/Internal/HowTos/Get_AWS_Credentials_On_Laptop/).
1. Create the tables we'll be using for this activity by running the following `aws` CLI commands:
   ```none
   aws cloudformation create-stack --region us-west-2 --stack-name dynamodbscan-onlineuserorderstable --template-body file://cloudformation/dynamodbscanandserialization/prework/DynamoDB_OnlineUserOrders.yml --capabilities CAPABILITY_IAM
   ```
1. Make sure the `aws` command runs without error.
1. Log into your AWS account on Conduit and verify that the table exists and has sample data.
 
The `OnlineUserOrders` table looks like this:
 
* `userId`: partition key—unique id for each user
* `orderId`: sort key—unique id for each order
* `totalCost`: total cost of the order
 
You want to be able to transfer data from the table so that it can be stored in a file and backed up. You also need to 
be able to recover from one of these backup files by deserializing each order object and writing it to the database. You
will be implementing the methods on the `OrderSerializer` class. The `toJSON` method accepts an `Order` object and 
returns its JSON representation, and the `toOrder` accepts a `String` and returns an `Order` object.

You have also been provided with a `OrderSerializationException` that can be thrown if an exception occurs while
serializing or deserializing.
