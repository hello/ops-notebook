
# Update Firehose -> Redshift

When adding new columns to redshift tables populated by firehose,
make sure that the number of columns in a `record` matches the number of columns in the database table.
Otherwise, you'd see this error when you run
`select * FROM stl_load_errors order by starttime desc limit 1;`
```
err_code        | 1214
err_reason      | Delimiter not found
```


Steps to deploy changes to the firehose stream after adding new columns:

1. Stop firehose worker (via `sanders`)
2. Wait for data in the pipeline to be delivered to Redshift (check "DeliveryToRedshift Records" graph)
3. Update the table schema in Redshift (might take a while if table has lots of data)
4. Deploy updated firehose worker
5. Monitor (kinesis app millis behind, query table, redshift performance graphs, firehose delivery graphs)


