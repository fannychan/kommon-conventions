
```
    __ __                                         ______                            __  _                 
   / //_/___  ____ ___  ____ ___  ____  ____     / ____/___  ____ _   _____  ____  / /_(_)___  ____  _____
  / ,< / __ \/ __ `__ \/ __ `__ \/ __ \/ __ \   / /   / __ \/ __ \ | / / _ \/ __ \/ __/ / __ \/ __ \/ ___/
 / /| / /_/ / / / / / / / / / / / /_/ / / / /  / /___/ /_/ / / / / |/ /  __/ / / / /_/ / /_/ / / / (__  ) 
/_/ |_\____/_/ /_/ /_/_/ /_/ /_/\____/_/ /_/   \____/\____/_/ /_/|___/\___/_/ /_/\__/_/\____/_/ /_/____/  
                                                                                                          
```
## About
In this repo you can find conventions for naming of business related things and other best practices. By following these conventions you will not only save yourself from a spanking during the next code review but you will also contribute to making our stack more coherent and easier read/modify.

Unhappy with something? Bring it up on Slack in #dev or call for meeting. Or simply modify this document. Missing something? Just add it.

## Naming

| Type                 | Description and convention | Example |                        
|----------------------|----------------------------|---------|
| Identification (id) | Everything that has is used to identify something should end with `id`. Do not use `no` or `number`  | `cartId`, `userId`, `orderId`
| A physical item | This is an item that is being sold online/in-store, e.g. a box of anti-histamine or a tube tooth paste. If you are referring to an item, use the above convention with `id`. We do not call this a `product`  | `item`, `itemId` |
Microservice | These names should contain any abbreviations (that is abbreviations of the service name) in the beginning. Either the name is an abbreviation or the full name is used, not both. Do not call your service some like `ps-product-service` but rather `product-service` | `oorc` (Order orchestrator), `ecom-order-return` |


## Conventions

### Date and time

We are following the `ISO 8601` standard (https://en.wikipedia.org/wiki/ISO_8601). Sometimes time-zone is included, sometimes it is not. In the table below you can see which time object you should use if you are writing a Java-application.
| Type | Time object | 
|-|-|
| Time span | Duration (Period could also be applied, depending on how large the span is) |
| Time (no date) | LocalTime |
| Time and date | LocalDateTime |
| Time and date with time-zone | ZonedDateTime |

### Kafka

All Kafka schemas are defined by Avro in https://github.com/oriola-corporation/kafka-message.
Avro will create the classes you need for your backend-applicaton (Java or Node). New schemas should be named according to the standard `KafkaXXX`, e.g. `KafkaAddress`, `KafkaCart`. The resulting classes for will be named according to the `KafkaXXXMessage` standard, e.g. `KafkaCartMessage` in order to make it clearer that this is the model used for sending Kafka messages.

### Databases

It is good practice to always have an `id` column as your primary key. Further, everything that is used as identification, i.e. everything that has `id` at the end of column name, should have a unique constraint.

### Language specific conventions

#### Java

##### Converters
The names of the methods in you converter class should contain a verb so that it is easy to understand what they actually do, e.g. `convertToKafkaCartMessage()`.

##### Getters
Should just be named after the instance variable that they are fetching, e.g. `orderId()` instead of `getOrderId()`. Remember:

``` "get is for old timers" - David Strömberg ```


