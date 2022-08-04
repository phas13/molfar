# aws cli

## List encryption status of all S3 buckets

Replace _<SOME_PROFILE>_ with actual value

```bash
{
export AWS_PROFILE=<SOME_PROFILE>
aws s3api list-buckets --query "Buckets[].Name" \
  | jq -r ".[]" \
  | xargs -I {} bash -c "echo {}; aws s3api get-bucket-encryption --bucket {} | jq -r '.ServerSideEncryptionConfiguration.Rules[0].ApplyServerSideEncryptionByDefault'"
}
```
