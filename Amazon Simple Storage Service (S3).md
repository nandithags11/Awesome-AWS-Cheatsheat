# Amazon Simple Storage Service (S3)

Amazon s3 serves as a data lake, accommodating diverse file formats such as CSV,json, parquet, images, videos etc. it follows a ’  pay as you go ‘ pricing model, making it very cost effective. In s3 files are stored as objects inside buckets, which must have globally unique names and be bound to a single AWS region. S3 achieves 99.999999999% availability by replicating the objects in 3 AZ (availability zone). It can support individual objects size up to 5TB and large files can be uploaded with multipart upload.

## Bucket Configuration and Management

+ Object Ownership and public access settings  
  + Object Ownership controls who own the uploaded object in the buckets (Bucket owner or the object uploader). One can enforce the **Bucket owner enforced** mode that all objects are owned by the bucket owner or **Object writer** mode that the uploader remain the owner of the objects.  
      
+ **Public Access** settings Prevents the unintended public exposure of your buckets and objects    
  + Block public ACLs: Reject new ACLs that grant public access  
  + Ignore public ACLs: Treat existing public access as private  
  + Block public bucket policies: Block bucket policies that allows public access.  
  + Restrict public bucket policies: prevent policy granting

+ **Bucket versioning** helps to keep different version of object in the bucket with

  + Out overwriting or deleting the original. When the versioning is enabled, every PUT, POST, or DELETE adds a new version or a delete marker, preserving prior version.

+ **Bucket Tag** is used to Identify objects by attaching Key value pairs as	metadata. Its common use cases are cost allocation, automation, and access control.

## Security and  Encryption

+ Encryption  
  + SSE S3 (default): Amazon s3 automatically encrypts every newly added object at rest using server-side encryption using amazon s3 managed keys,e mploying AES-256 for data protection without additional configuration or cost.  
  + SSE-KMS (customer managed keys): For greater control, AWS Key Management service can be used for server side encryption, which would let you create, rotate and audit the usage of your encryption keys.  
+ Object Lock  
  + S3 Object Lock Provides a write-once-read-many capability, preventing object from being deleted or overwritten for a specific retention or indefinitely.

## AWS CLI for S3

| List Buckets | aws s3 ls |
| :---- | :---- |
| List Bucket contents | aws s3 ls s3://BucketName \--recursive |
| Copy local to s3 | aws s3 cp localfile.txt s3://BucketName |
| Copy s3 to local | aws s3 cp s3://BucketName/file.txt localfile.txt |
| Sync local to s3 | aws s3 sync ./local-directory s3://your-bucket-name/destination-folder |
| Sync s3 to local | aws s3 sync s3://your-bucket-name/source-folder ./local-directory  |
| Remove Object | aws s3 rm s3://BucketName/file.txt |
|  Remove folder | aws s3 rm s3://BucketName/folder \--recursive |
|  Make bucket |  aws s3 mb s3://new-bucket |
|  Remove bucket | aws s3 rb s3://bucket-name \--force |
| Move/rename object | aws s3 mv s3://bucket/old.txt s3://bucket/new.txt |
| Presign URL | aws s3 presign s3://your-bucket-name/file.txt \--expires-in 3600 |
| Static website hosting |  aws s3 website s3://bucket/ \--index-document index.html \--error-document error.html |

## AMAZON S3 Storage Classes

Amazon Storage classes includes : S3 Intelligent-Tiering, S3 Standard, S3 Express One Zone, S3 Standard Infrequent Access (S3 Standard IA), S3 One Zone \- Infrequent Access (S3 One Zone-IA), S3 Glacier Instant Retrieval,S3 Glacier Flexible Retrieval (formerly S3 Glacier) and Amazon S3 Glacier Deep Archive (S3 Glacier Deep Archive)

## **Lifecycle Management**

Amazon S3 Lifecycle rules enable you to define automated actions—transition or expiration—for groups of objects based on age or other filters. These rules help control costs by moving data to cheaper storage as it becomes less frequently accessed and by deleting obsolete data.

+ Transition actions: Specify when objects move to a different storage class (e.g., 30 days to Standard‑IA, 90 days to Glacier Instant Retrieval).  
+ Expiration actions: Define when objects (or previous versions) are permanently deleted, freeing up storage and avoiding unnecessary costs.  
+ Versioning integration: Lifecycle can also clean up noncurrent object versions after a set period, ensuring only recent versions persist.
