# EMR Security

## Encrypting your S3 buckets with different encryption modes and keys


- With S3 encryption on Amazon EMR, all the encryption modes use a single CMK by default to encrypt objects in S3. 
- If you have highly sensitive content in specific S3 buckets, you may want to manage the encryption of these buckets separately by using different CMKs or encryption modes for individual buckets. 
- You can accomplish this using the per bucket encryption overrides option in Amazon EMR.

> With per bucket encryption overrides, you can choose optimal encryption overrides for specific buckets.
