# Redshift Security

## S3 Encryption

The COPY command supports the following types of Amazon S3 encryption:

- Server-side encryption with Amazon S3-managed keys (SSE-S3)
- Server-side encryption with AWS KMS keys (SSE-KMS)
- Client-side encryption using a client-side symmetric root key

The COPY command doesn't support the following types of Amazon S3 encryption:

- Server-side encryption with customer-provided keys (SSE-C)
- Client-side encryption using an AWS KMS key
- Client-side encryption using a customer-provided asymmetric root key

