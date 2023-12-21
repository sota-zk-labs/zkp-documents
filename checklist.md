# Checklist
| Check         | Task                                                                                                                                                                 |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [x] 1.3.1     | Establish baseline K8s ready go microservice in line with others when it comes to configs, logging, monitoring, healthchecks and profiling.                          |
| [x] 1.3.2     | Allow configuration of several S3 “account” entities.                                                                                                                |
| [x] 1.3.2.1   | Only one s3 entity should be allowed to be marked as shared.                                                                                                         |
| [x] 1.3.2.2   | pathStyle value control if bucket should be accessed using path-style or virtual-hosted-style.                                                                       |
| [x] 1.3.2.3   | Add S3 `POST /rest/v0/s3/verify(/<s3account uuid>)?` endpoint(s).                                                                                                    |
| [] 1.3.3      | Provide service with credentials through vault with K8s annotations/secrets.                                                                                         |
| [] 1.3.3.1    | Document an expectation on clients receiving signed URLs to perform retries in case the credential is invalided due to restarts of this service.                     |
| [x] 1.3.4     | Establish a PostgreSQL database which keeps the state of which tenant has gotten a dedicated assignment to what bucket in what S3 endpoint.                          |
| [x] 1.3.4.1   | The system should verify consistency dedicated bucket assignments and the configured s3 accounts on service start                                                    |
| [x] 1.3.4.1.1 | On service upstart verify that no tenant is assigned to a bucket/account combo that is no longer available.                                                          |
| [x] 1.3.4.2   | We should keep a separate K8s job to perform database migrations as needed towards the DB.                                                                           |
| [x] 1.3.4.3   | The K8s configuration should support separate user and credentials for each of these purposes                                                                        |
| [] 1.3.5      | In the S3 endpoint marked as shared we should default distribute customers between buckets dependent on the first 2 characters of customeruuid.                      |
| [] 1.3.5.1    | We should keep a separate K8s job to perform creation of shared buckets.                                                                                             |
| [x] 1.3.6     | Expose provision service API under `https://outscank8s.devnext.outpost24.com/provision/`                                                                             |
| [] 1.3.7      | Add endpoint `POST /rest/v0/s3/<tenantuuid>` that returns a signed url that should be fully usable by the client to perform the requested action.                    |
| [] 1.3.7.1    | Require and verify K8s service account JWT token from service from clients                                                                                           |
| [] 1.3.7.2    | Append an enforced tag for any PutObject/CopyObject operation request before signing them.                                                                           |
| [] 1.3.7.3    | Only allow Put/CopyObject operations when the destination doesn’t exist or has a tag matching `service=<service_account_jwt.sub>`                                    |
| [] 1.3.7.4    | Only allow GetObject/CopyObject operations when the source has a tag matching `service=<service_account_jwt.sub>`                                                    |
| [] 1.3.7.5    | Only allow operations for files when the tenantuuid in the API is prefixing the path requested in the bucket                                                         |
| [] 1.3.7.6    | Implement “demo client” for interacting with this endpoint                                                                                                           |
| [] 1.3.8      | Implement metric gathering for per bucket tenant and object distribution:                                                                                            |
| [] 1.3.9      | Make sure that APM transaction spans related to S3 convey enough information to break them down by which s3 uri/region/account/bucket/tenant/service they relate to. |
| [] 1.3.10     | Job to apply configured rules after templating with consideration for the tenant-prefix in each bucket. For a bucket with shared                                     |
| [] 1.3.11     | Implement lifecycle policies based on workshop discussions.                                                                                                          |
