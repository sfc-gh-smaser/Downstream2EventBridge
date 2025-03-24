# Downstream2EventBridge
This provides an example of capturing Snowflake Changes and delivery downstream and second with AWS EventBridge as the receipant of those events.
First built March, 2025


A prebuilt framework (coded in 2 notebooks to create the objects) that allows one to send new/updated rows that happen within the tables you specific to be sent as events into AWS EventBridge.  The means of "Change Data Capture" of Snowflake to downstream applications, showing Snowflake can be a central data hub.  To add a table, just add it to the control table.  You can then register what UDF the process should call, so can be used to any external endpoing or even to take actions within Snowflake.

It uses:
* Triggered Task and Stream on the control table
* The Task in #1 creates new Stream and triggered task when a table is added
* Vectorized UDF using External Access w/ Python calls the AWS API with the appropriate payload (bundles 10 events/message, the max that AWS can handle today). 
* Uses our latest IAM authentication into AWS.  The Client code is easily reusable to access anything in AWS that has a BOTO3 API.
* It is parameterized, neatly written in the Notebooks and slightly documented.

# Notebooks:
* Notebook #1 creates the UDF to deliver Events to EventBridge (two versions, second one accommodates refreshing AWS Token for long-running jobs)
* Notebook #2 creates the change capture registration and configuration
