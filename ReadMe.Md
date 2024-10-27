#### intro to event sourcing --- not deep explaination
# --
# --
# Event Sourcing
# wut is event sourcing --??
Event Sourcing is a way to keep track of business actions by saving them as events Instead of just saving the current state of things it saves every change that happens This means no important data is lost Every action creates an event that is saved in a database This helps in checking past actions and understanding what happened It also makes it easier to analyze and report on business activities

# wut is Event ?
Events are facts about things that happened in the past They tell us about actions that were completed and should be named in the past like "user added" or "order confirmed" Events are not meant for one person they are shared information It is like telling a story at a party We hope someone listens but they might not pay attention

## Events have some important features

### They cannot be changed Once something happens it cannot be forgotten

### They can be ignored but you cannot take them back since you cannot change what has already happened

### People can understand events in different ways For example the result of a basketball game is a fact Fans of the winning team will be happy while fans of the losing team will feel sad


# wut is Steam ?
A stream is a way to group events together In Event Sourcing streams represent objects or entities All changes to an entity are saved as events in that stream To understand the current state of the entity you look at all the events in the stream and apply them one by one in the order they happened

Each stream has a special ID that shows which specific object it belongs to Each event in the stream has its own unique position This position is usually a number that goes up with each new event This number helps keep track of the order of events when checking the state It can also help find problems when multiple changes happen at the same time


# Event representation
Events are messages that share information They can be shown in different formats like JSON Binary or XML Along with the main data events usually have some extra details

These details include

### An ID which is a unique identifier for the event

### A type which is the name of the event like "invoice issued"

### A stream ID which shows which object the event is related to like the invoice ID

### A stream position which is a number that tells the order of the event for that object

### A timestamp which shows when the event happened

#### Other details can include things like correlation ID and causation ID which give more context about the event



# Event Storage
Event Storage is about how events are saved Event Sourcing does not depend on a specific type of storage You can use any kind of database like relational or document databases as long as it meets certain requirements

The main idea is to keep an append-only log of events This means you only add new events to the end of the list and do not change what is already there Events are stored in the order they happen This is why Event Stores are special types of databases made just for this purpose



# Retrieving the current state from events
In Event Sourcing the current state of an entity is built from a series of events These events are grouped together in streams which represent the entity 

To get the current state you follow a process called stream aggregation 

First you read all the events related to that specific stream Then you order these events by when they happened 

Next you create an empty version of the entity 

Finally you apply each event to this entity one by one This way you translate all the events back into the current state of the entity 

Each event carries information about what happened to the entity over time 

The advantage of this method is that it always uses the latest rules for applying changes so if the rules change you don’t have to update past data Everything is updated automatically the next time you check the state