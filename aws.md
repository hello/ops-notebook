#AWS

###Useful AWS CLI Commands

####Modify Retention Period
* Describe the stream before making changes
 * `aws kinesis describe-stream --stream-name batch_pill_data`
* Set a new value for retention period (in hours; 168hr max)
 * `aws kinesis increase-stream-retention-period --stream-name batch_pill_data --retention-period-hours 168`
* Monitor stream status until retention period is updated to new value
 * `aws kinesis describe-stream --stream-name batch_pill_data`
