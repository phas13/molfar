# aws cli

## List encryption status of all S3 buckets

```bash
{
export AWS_PROFILE=logixboard
aws s3api list-buckets --query "Buckets[].Name" \
  | jq -r ".[]" \
  | xargs -I {} bash -c "echo {}; aws s3api get-bucket-encryption --bucket {} | jq -r '.ServerSideEncryptionConfiguration.Rules[0].ApplyServerSideEncryptionByDefault'"
}
```
