
## Add Migration

```cmd
Add-Migration <migration-name> -context OBRPDbContext
```


- Run the TaskRunner project and select "1. Command to initialize the Database" to apply the migration

# To remove last migration
```cmd
Remove-Migration -context OBRPDbContext
```
## Remove migration (and unapply migration from database)
```cmd
Remove-Migration -Force -context OBRPDbContext
```
## To list all migrations in the database
```cmd
Get-Migration
```
