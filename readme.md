project aim is to provide CFN files which would permit executing tasks described in 'AWS Data Engineering Immersion Day' within AWS Free Tier. These files are designed to work in regions with at least 4AZs (us-east-1 or us-west-2).

Two CFN files are used, originally taken from links provided in 'Lab: Ingestion with DMS': https://catalog.us-east-1.prod.workshops.aws/workshops/976050cc-0606-4b23-b49f-ca7b8ac4b153/en-US/400

Files: 
1.DMSLAB_instructor_CFN.yaml:
https://s3.amazonaws.com/aws-dataengineering-day.workshop.aws/DMSLab_instructor_CFN.yaml

2.SkipDMSlab_student_CFN.yaml
https://s3.amazonaws.com/aws-dataengineering-day.workshop.aws/SkipDMSlab_student_CFN.yaml

Comments on file 1:
-In order to descrease size of database deployment, changes were made to original database creation files, details can be found in this repo: https://github.com/kamusiall/aws-database-migration-samples
-To assure security when connecting to RDS from remote source, an IP of the source can be provided in inbound rules setup at the stage of CFN stack creation

Comments on file 2:
-CFN resources relating to NatGateway creation were removed

****
see branches readme for details on setup
