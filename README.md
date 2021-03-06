# svalbard
Svalbard is an encrypted backup solution for AWS S3.  It is a simple bash script which can be used to backup to, restore from, or list the encrypted files in an S3 bucket.  Filenames are encrypted with relative path information, allowing multi-level backup/restore.  Backup will check S3 for existing files before uploading, and only upload if the local copy is newer.

## Dependencies
- openssl and aws command line executables
- aws credentials and a writable S3 bucket

## Usage
svalbard OP BUCKET [PATH...]

OP can be one of backup|restore|ls
BUCKET is an S3 bucket
PATH is zero or more local filesystem paths

The password and salt used to derive the encryption key must be set in ~/.svalbard using the variables 'salt' and 'pass'.  The script will fail if these are not set.  You may also set the 'cipher' and 'TMPDIR' variables, though if you don't defaults will be provided.

## Examples
##### backup everything under docs/ to my-backup-bucket
svalbard backup my-backup-bucket docs/

##### restore bat.txt and everything under docs/baz from my-backup-bucket
svalbard restore my-backup-bucket docs/bar/baz/bat.txt docs/baz/

##### list all files under docs/bar and docs/baz in my-backup-bucket
svalbard ls my-backup-bucket docs/bar docs/baz

