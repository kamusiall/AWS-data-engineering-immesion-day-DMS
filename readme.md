Project aim is to provide CFN files which would permit executing lab 'AWS Data Engineering Immersion Day' within AWS Free Tier. These files are designed to work in regions with at least 4AZs (e.g. us-east-1 or us-west-2).

Two CFN files can be used, originally taken from links provided in 'Lab: Ingestion with DMS': https://catalog.us-east-1.prod.workshops.aws/workshops/976050cc-0606-4b23-b49f-ca7b8ac4b153/en-US/400

Source files location: 
1.DMSLAB_instructor_CFN.yaml:
https://s3.amazonaws.com/aws-dataengineering-day.workshop.aws/DMSLab_instructor_CFN.yaml

2.SkipDMSlab_student_CFN.yaml
https://s3.amazonaws.com/aws-dataengineering-day.workshop.aws/SkipDMSlab_student_CFN.yaml

***
***Comments on files:***

Comments on file 1:
-In order to descrease size of database deployment, changes were made to original database creation files, details can be found in this repo: https://github.com/kamusiall/aws-database-migration-samples
-To assure security when connecting to RDS from remote source, an IP of the inbound connection (e.g. IP of your machine to establish connection via SQL Developer tool (e.g. pgadmin / DBeaver)) can be provided in inbound rules setup at the stage of CFN stack creation

Comments on file 2:
-original file creates Nat Gateway which is not within AWS free tier

***
***Branches***

see branches readme for details on setup

`main` branch are raw AWS files which can be compared to other branches (through pull request)

`altered_CFN_noStudent` branch is only for file 1, this assures to remain in Free Tier but requires you to perform DMS lab

`altered_CFN_with_NGH` branch has file 1 and file 2, due to Nat Gateway creation this is not within Free Tier, but it finishes DMS lab

***
***known issues***

1.
no connection between DMS RDS source endpoint and RDS -> follow this instructions: https://catalog.us-east-1.prod.workshops.aws/workshops/976050cc-0606-4b23-b49f-ca7b8ac4b153/en-US/400/401/410-pre-lab-1#changing-rds-security-group

2.
after setup of replication instance (https://catalog.us-east-1.prod.workshops.aws/workshops/976050cc-0606-4b23-b49f-ca7b8ac4b153/en-US/400/401/430-main-lab) it has been found that after some point RDS storage started to decrease rapidly. After checking options listed here:
https://aws.amazon.com/premiumsupport/knowledge-center/diskfull-error-rds-postgresql/
Issue is likely due to 'Streaming read replica lag' causing no WAL consumption.

In order to confirm this is an issue you can:
1. check RDS instance metrics: "Transaction Logs Disk Usage" or "Free Storage Space"
2. run query (in your SQL Developer tool): `SELECT slot_name, pg_size_pretty(pg_wal_lsn_diff(pg_current_wal_lsn(),restart_lsn)) AS replicationSlotLag, 
active FROM pg_replication_slots ;`

To alleviate the issue, you can:
1. setup alarm for metrics listed in point 1 and stop/start the instance when you need to work with the lab (the instance will stop anyway if storage is exhausted). It is unknown if replication will start correctly after this step
2. use pg_drop_replication_slot (per above AWS knowledge-center article)
3. increase size of the instance (whic will incur some costs)

Any other issue is likely described in the AWS lab.

***
***next steps***

alter CFN to assure each lab step setup with one YAML file
figure out original reason for WAL issue described in known issues.
