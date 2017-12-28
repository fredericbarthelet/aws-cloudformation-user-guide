# AWS::RDS::EventSubscription<a name="aws-resource-rds-eventsubscription"></a>

Use the `AWS::RDS::EventSubscription` resource to get notifications for Amazon Relational Database Service events through the Amazon Simple Notification Service\. For more information, see [ Using Amazon RDS Event Notification](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Events.html) in the *Amazon Relational Database Service User Guide*\.


+ [Syntax](#aws-resource-rds-eventsubscription-syntax)
+ [Properties](#w3ab2c21c10d908b9)
+ [Return Value](#w3ab2c21c10d908c11)
+ [Example](#w3ab2c21c10d908c13)

## Syntax<a name="aws-resource-rds-eventsubscription-syntax"></a>

To declare this entity in your AWS CloudFormation template, use the following syntax:

### JSON<a name="aws-resource-rds-eventsubscription-syntax.json"></a>

```
{
  "Type" : "AWS::RDS::EventSubscription",
  "Properties" : {
    "[[ERROR] BAD/MISSING LINK TEXT](#cfn-rds-eventsubscription-enabled)" : Boolean,
    "[[ERROR] BAD/MISSING LINK TEXT](#cfn-rds-eventsubscription-eventcategories)" : [ String, ... ],
    "[[ERROR] BAD/MISSING LINK TEXT](#cfn-rds-eventsubscription-snstopicarn)" : String,
    "[[ERROR] BAD/MISSING LINK TEXT](#cfn-rds-eventsubscription-sourceids)" : [ String, ... ],
    "[[ERROR] BAD/MISSING LINK TEXT](#cfn-rds-eventsubscription-sourcetype)" : String
  }
}
```

### YAML<a name="aws-resource-rds-eventsubscription-syntax.yaml"></a>

```
Type: "AWS::RDS::EventSubscription"
Properties: 
  [[ERROR] BAD/MISSING LINK TEXT](#cfn-rds-eventsubscription-enabled): Boolean
  [[ERROR] BAD/MISSING LINK TEXT](#cfn-rds-eventsubscription-eventcategories):
    - String
  [[ERROR] BAD/MISSING LINK TEXT](#cfn-rds-eventsubscription-snstopicarn): String
  [[ERROR] BAD/MISSING LINK TEXT](#cfn-rds-eventsubscription-sourceids):
    - String
  [[ERROR] BAD/MISSING LINK TEXT](#cfn-rds-eventsubscription-sourcetype): String
```

## Properties<a name="w3ab2c21c10d908b9"></a>

`Enabled`  
Indicates whether to activate the subscription\. If you don't specify this property, AWS CloudFormation activates the subscription\.  
*Required: *No  
*Type*: Boolean  
*Update requires*: No interruption

`EventCategories`  
A list of event categories that you want to subscribe to for a given source type\. If you don't specify this property, you are notified about all event categories\. For more information, see [ Using Amazon RDS Event Notification](http://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_Events.html) in the *Amazon Relational Database Service User Guide*\.  
*Required: *No  
*Type*: List of String values  
*Update requires*: No interruption

`SnsTopicArn`  
The Amazon Resource Name \(ARN\) of an Amazon SNS topic that you want to send event notifications to\.  
*Required: *Yes  
*Type*: String  
*Update requires*: Replacement

`SourceIds`  
A list of identifiers for which Amazon RDS provides notification events\.  
If you don't specify a value, notifications are provided for all sources\. If you specify multiple values, they must be of the same type\. For example, if you specify a database instance ID, all other values must be database instance IDs\.  
*Required: *No  
*Type*: List of String values  
*Update requires*: No interruption

`SourceType`  
The type of source for which Amazon RDS provides notification events\. For example, if you want to be notified of events generated by a database instance, set this parameter to `db-instance`\. If you don't specify a value, notifications are provided for all source types\. For valid values, see the `SourceType` parameter for the [CreateEventSubscription](http://docs.aws.amazon.com/AmazonRDS/latest/APIReference/API_CreateEventSubscription.html) action in the *Amazon Relational Database Service API Reference*\.  
*Required: *Conditional\. If you specify the `SourceIds` or `EventCategories` property, you must specify this property\.  
*Type*: String  
*Update requires*: Replacement if you're removing this property after it was previously specified\. All other updates require no interruption\.

## Return Value<a name="w3ab2c21c10d908c11"></a>

When the logical ID of this resource is provided to the `Ref` intrinsic function, `Ref` returns the resource name\. For example:

```
{ "Ref": "myEventSubscription" }
```

For the resource with the logical ID `myEventSubscription`, `Ref` returns the Amazon RDS event subscription name, such as: `mystack-myEventSubscription-1DDYF1E3B3I`\.

For more information about using the `Ref` function, see Ref\.

## Example<a name="w3ab2c21c10d908c13"></a>

The following snippet creates an event subscription for an existing database instance `db-instance-1` and a database with the logical ID `myDBInstance`, which is declared elsewhere in the same template\.

### JSON<a name="aws-resource-rds-eventsubscription-example.json"></a>

```
"myEventSubscription": {
  "Type": "AWS::RDS::EventSubscription",
  "Properties": {
    "EventCategories": ["configuration change", "failure", "deletion"],
    "SnsTopicArn": "arn:aws:sns:us-west-2:123456789012:example-topic",
    "SourceIds": ["db-instance-1", { "Ref" : "myDBInstance" }],
    "SourceType":"db-instance",
    "Enabled" : false
  }
}
```

### YAML<a name="aws-resource-rds-eventsubscription-example.yaml"></a>

```
myEventSubscription: 
  Type: "AWS::RDS::EventSubscription"
  Properties: 
    EventCategories: 
      - "configuration change"
      - "failure"
      - "deletion"
    SnsTopicArn: "arn:aws:sns:us-west-2:123456789012:example-topic"
    SourceIds: 
      - "db-instance-1"
      - 
        Ref: "myDBInstance"
    SourceType: "db-instance"
    Enabled: false
```