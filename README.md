### Old SQL Server Developer container images

This repository contains Dockerfiles to create SQL Server Developer 2012 and 2008 container images.

Once the images are built from the Dockerfiles, you can create SQL Server Developer 2012 and 2008 containers.

Instructions:
Acquire the SQL Server 2008 R2 Developer ISO and the SQL Server 2012 Developer ISO

Extract the contents of the ISO into folders SQLServer2008Developer\sql_server_2008_dev and SQLServer2012Developer\lol respectively

CD into SQLServer2008Developer and SQLServer2012Developer

Execute docker build -t sqlserver2012 . and docker build -t sqlserver2008 . respectively
