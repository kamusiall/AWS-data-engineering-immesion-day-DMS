****
this CFN files should be executed with file 1. first and file 2. second. File 2. will create an NAT gateway which will incur some costs to your account. However, it allows communication between replication instances and your database. Initial setup of RDS database can be with inbound TCP range 0.0.0.0/0 <- all traffic. This is not recommended. After initial setup you can change inbound rules to Public IP from NAT Gateway.
