# mssql server 2014 express image listening on static port 1433
#
# Note: This dockerfile is based on Buc Rogers' work here:
# https://github.com/brogersyh/Dockerfiles-for-windows/tree/master/sqlexpress
#
# .NET 3.5 required for SQL Server
FROM mcr.microsoft.com/dotnet/framework/sdk:3.5-20191008-windowsservercore-ltsc2019

# Switch to cmd shell
SHELL ["cmd", "/S", "/C"]

# Switch user to user with more privileges
USER "NT Authority\System"

# set environment variables
ENV sa_password ****
ENV attach_dbs "[]"

# make install files accessible
COPY sql_server_2008_dev /
COPY start.ps1 /
WORKDIR /

# download and install Microsoft SQL 2014 Express Edition in one step
RUN /setup.exe /q /ACTION=Install /INSTANCENAME=SQL /FEATURES=SQLEngine /SQLSVCACCOUNT="NT AUTHORITY\SYSTEM" /SQLSYSADMINACCOUNTS="BUILTIN\ADMINISTRATORS" /TCPENABLED=1 /NPENABLED=0 /SKIPRULES=PerfMonCounterNotCorruptedCheck /AGTSVCACCOUNT="NT AUTHORITY\SYSTEM" /IACCEPTSQLSERVERLICENSETERMS

# Set registry values
RUN powershell -Command \
        set-strictmode -version latest ; \
        stop-service MSSQL`$SQL ; \
        set-itemproperty -path 'HKLM:\software\microsoft\microsoft sql server\mssql10_50.SQL\mssqlserver\supersocketnetlib\tcp\ipall' -name tcpdynamicports -value '' ; \
        set-itemproperty -path 'HKLM:\software\microsoft\microsoft sql server\mssql10_50.SQL\mssqlserver\supersocketnetlib\tcp\ipall' -name tcpport -value 1433 ; \
        set-itemproperty -path 'HKLM:\software\microsoft\microsoft sql server\mssql10_50.SQL\mssqlserver\' -name LoginMode -value 2 ;

# Expose SQL Server port
EXPOSE 1433

# Start SQL Server
CMD powershell ./start -sa_password %sa_password% -attach_dbs \"%attach_dbs%\" -Verbose
