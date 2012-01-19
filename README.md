## dynamoDB.js - a node.js module for accessing [Amazon DynamoDB](http://aws.amazon.com/dynamodb/ "click to go to Amazon DynamoDB").

DynamoDB uses JSON for communication. That means both the request body and the response are in JSON format. This module wraps up the request and takes care of authentication. The user will be responsible for crafting the request and parsing the result(both in JSON).

Usage:

    // You can read your credentials from a local file.
    var credentials = {AccessKeyId : "Your_AWS_Access_Key_Id", 
                       SecretKey   : "Your_Secret_Key"}; 
    var dynamoDB = require('./lib/dynamoDB').DynamoDB(credentials);

## Implemented features
### CreateTable [reference on aws](http://docs.amazonwebservices.com/amazondynamodb/latest/developerguide/API_CreateTable.html)

    dynamoDB.createTable(
        {"TableName":"Table1",
            "KeySchema":
                {"HashKeyElement":{"AttributeName":"Color","AttributeType":"S"},
                "RangeKeyElement":{"AttributeName":"Weight","AttributeType":"N"}},
            "ProvisionedThroughput":{"ReadCapacityUnits":5,"WriteCapacityUnits":10}
        }, function(result) {
        result.on('data', function(chunk){
            console.log(""+chunk);
        });
    });

### ListTables [reference on aws](http://docs.amazonwebservices.com/amazondynamodb/latest/developerguide/API_ListTables.html)

    dynamoDB.listTables({}, function(result) {
        result.on('data', function(chunk){
            console.log(""+chunk);
        });
    });

### DeleteTable [reference on aws](http://docs.amazonwebservices.com/amazondynamodb/latest/developerguide/API_DeleteTable.html)

    dynamoDB.deleteTable({"TableName":"Table1"}, function(result) {
        result.on('data', function(chunk){
            console.log(""+chunk);
        });
    });

### DescribeTable [reference on aws](http://docs.amazonwebservices.com/amazondynamodb/latest/developerguide/API_DescribeTable.html)

    dynamoDB.describeTable({"TableName":"Table1"}, function(result) {
        result.on('data', function(chunk){
            console.log(""+chunk);
        });
    });


### PutItem [reference on aws](http://docs.amazonwebservices.com/amazondynamodb/latest/developerguide/API_PutItem.html)

    dynamoDB.putItem(
        {"TableName":"Table1",
            "Item":{
                "Color":{"S":"white"},
                "Name":{"S":"fancy vase"},
                "Weight":{"N":"2"}
            }
        }, function(result) {
            result.on('data', function(chunk){
                console.log(""+chunk);
            });
    });

### GetItem [reference on aws](http://docs.amazonwebservices.com/amazondynamodb/latest/developerguide/API_GetItem.html)

    dynamoDB.getItem(
        {"TableName":"Table1",
            "Key":
                {"HashKeyElement": {"S":"white"},
                "RangeKeyElement": {"N":"2"}
            },
            "AttributesToGet":["Color","Weight", "Name"],
            "ConsistentRead":true
        }, function(result) {
            result.on('data', function(chunk){
                console.log(""+chunk);
            });
    });

### BatchGetItem [reference on aws](http://docs.amazonwebservices.com/amazondynamodb/latest/developerguide/API_BatchGetItem.html)

    dynamoDB.batchGetItem(
        {"RequestItems":
            {"Table1": 
                {"Keys": 
                    [{"HashKeyElement": {"S":"white"}, "RangeKeyElement":{"N":"2"}},
                    {"HashKeyElement": {"S":"blue"}, "RangeKeyElement":{"N":"5"}},
                    {"HashKeyElement": {"S":"red"}, "RangeKeyElement":{"N":"3"}}],
                "AttributesToGet":["Color", "Weight", "Name"]}
            }
        }
        }, function(result) {
            result.on('data', function(chunk){
                console.log(""+chunk);
            });
    });

### UpdateTable [reference on aws](http://docs.amazonwebservices.com/amazondynamodb/latest/developerguide/API_UpdateTable.html)
    dynamoDB.updateTable(
    {"TableName":"Table1",
        "ProvisionedThroughput":{"ReadCapacityUnits":5,"WriteCapacityUnits":5}
    }
    , function(result) {
        result.on('data', function(chunk){
            console.log(""+chunk);
        });
    });

### UpdateItem [reference on aws](http://docs.amazonwebservices.com/amazondynamodb/latest/developerguide/API_UpdateItem.html)
    dynamoDB.updateItem(
        {"TableName":"Table1",
            "Key":
                {"HashKeyElement":{"S":"white"},
                "RangeKeyElement":{"N":"2"}},
            "AttributeUpdates":{"Name":{"Value":{"S":"not-so-fancy-anymore vase"},"Action":"PUT"}},
            "ReturnValues":"ALL_NEW"
        }
    , function(result) {
        result.on('data', function(chunk){
            console.log(""+chunk);
        });
    });

