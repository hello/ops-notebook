
When adding new columns to redshift tables populated by firehose,
make sure that the number of columns in a `record` matches the number of columns in the database table.
Otherwise, you'd see this error when you run
`select * FROM stl_load_errors order by starttime desc limit 1;`
```
err_code        | 1214
err_reason      | Delimiter not found
```
