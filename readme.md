Comments on file 1:
-In order to descrease size of database deployment, changes were made to original database creation files, details can be found in this repo: https://github.com/kamusiall/aws-database-migration-samples
-To assure security when connecting to RDS from remote source, an IP of the source can be provided in inbound rules setup at the stage of CFN stack creation

Comments on file 2:
-CFN resources relating to NatGateway creation were removed


****
in this setup you are only provided with RDS, without replication instances. It is a (free of charge) alternative for deployment of CFN from this lab:
https://catalog.us-east-1.prod.workshops.aws/workshops/976050cc-0606-4b23-b49f-ca7b8ac4b153/en-US/400/401/410-pre-lab-1

in order to establish communication with replication instances you can setup replication instances in the same VPC as your RDS - see step 2 from this lab:
https://github.com/sanchitdilipjain/acd-2022-dna-workhop/blob/main/DNA%20Lab%20Manual.pdf

after creation of 'Source Endpoint' add inbound rule to your RDS to permit Postgresql communication through security group.
