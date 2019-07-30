# Ballerina Amazon EC2 Connector

Amazon SQS Connector allows you to connect to the Amazon Simple Queue Service (SQS) via REST API from Ballerina.

## Compatibility
| Ballerina Language Version | Amazon SQS API version  |
| -------------------------- | ----------------------  |
| 0.991.0                    | 2012-11-05              |

The following sections provide you with information on how to use the Ballerina Amazon SQS connector.

- [Contribute To Develop](#contribute-to-develop)
- [Working with Amazon SQS Connector Actions](#Working-with-Amazon-SQS-Connector)
- [Sample](#sample)

### Contribute To develop

Clone the repository by running the following command 
```shell
git clone https://github.com/wso2-ballerina/module-amazonsqs.git
```

### Working with Amazon SQS Connector

First, import the `wso2/amazonsqs` module into the Ballerina project.

```ballerina
import wso2/amazonec2;
```

In order for you to use the Amazon SQS Connector, first you need to create a Amazon SQS Client.

```ballerina
amazonsqs:Configuration configuration = {
    accessKey: config:getAsString("ACCESS_KEY_ID"),
    secretKey: config:getAsString("SECRET_ACCESS_KEY"),
    region: config:getAsString("REGION"),
    accountNumber: config:getAsString("ACCOUNT_NUMBER")
};

amazonsqs:Client sqsClient = new(configuration);
```

##### Sample

```ballerina
import ballerina/log;
import wso2/amazonsqs;

// Add the SQS credentials as the Configuration
amazonsqs:Configuration configuration = {
    accessKey: "AKIAIOSFODNN7EXAMPLE",
    secretKey: "wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY",
    region: "us-east-2",
    accountNumber: "610973236798"
};

amazonsqs:Client sqsClient = new(configuration);

public function main(string... args) {

    // Create a new SQS FIFO queue named "demo.fifo"
    map<string> attributes = {};
    string|error response = sqsClient->createQueue("newQueue", attributes);
    if(response is string) {
        log:printInfo("Created queue URL: " + response);
    } else {
        log:printInfo("Error while creating a queue");
    }

}
```