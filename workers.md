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
  * You can either spin up an instance manually from the AWS console (if you have IAM list roles privileges) and specify your own keypair at that time
  * OR... You can use the `sanders create --emergency` command to create a new launch config which will generate a new keypair and allow you to use this new keypair to SSH into the instance. 
* SSH into new instance and stop all workers.
 * `initctl list |grep suripu` to list all suripu services currently available 
 * `sudo service stop suripu-workers-<worker_name>` for each worker 
* Edit the prod.yml config file for the worker and assign unique App name for the KCL to use. (e.g. SenseSaveConsumerProdReprocess)
* Restart the worker you want to reprocess (e.g. sense-save)
* Check DynamoDB for a checkpoint record being written. 
* Stop the worker again.
* Modify checkpoint in the Dynamo table named the same as the App name you added to the config file above and replace with the value you found earlier. 
* Restart worker. 
