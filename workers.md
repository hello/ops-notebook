# Workers

## List of Workers
#### Alarm

#### Sense Save

#### Sense Save (DDB)

#### Pill Data

#### Insights

## Reprocessing Kinesis Records
Currently only available for Sense data (pill checkpoint tracking coming soon)
* Determine when the event occured (use papertrail, etc.)
* Find checkpoint(s) for start of event(s) in the checkpoint tracking Dynamo table
	* Remember, these events are in UTC
* Start a new worker instance for reprocessing.
* SSH into new instance and stop all workers.
* Edit prod.yml config file for the worker and assign unique App name for the KCL to use. (e.g. SenseSaveConsumerProdReprocess)
* Restart the worker you want to reprocess (e.g. sense-save)
* Check DynamoDB for a checkpoint record being written. 
* Stop the worker again.
* Modify checkpoint in the Dynamo table named the same as the App name you added to the config file above and replace with the value you found earlier. 
* Restart worker. 
