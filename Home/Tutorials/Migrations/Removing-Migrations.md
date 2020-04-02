In order to properly remove a migration you must run the command:

```
remove-migration
```

For this command to succeed, the migration must not have been run against the target database already. See [Changing Migration Target (Rolling back and forwards)](/Home/Tutorials/Migrations/Changing-Migration-Target-\(Rolling-back-and-forwards\)) on how to rollback a migration.

Once the command completes, it will remove the migration file and update the snapshot file.