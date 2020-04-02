After adding a new property or making any modifications to the database entities in Code First, you will need to create a new migration.

A migration can be created in the PMC with the command 

```
add-migration [NAME]
```

For example `add-migration AddMiddleNameToPerson`.

Try to make the name of the migration as descriptive as possible without going overboard.

After running the command a new file will be created in `*.DAL.SQL` with a date stamp and the migration name. E.g. `20190814202755_Initial`

In EF Core you cannot simply rerun the migration create command in the event you need additional changes. In order to re-scaffold a migration you will need to follow the instructions in [Removing Migrations](/Home/Tutorials/Migrations/Removing-Migrations).

To apply the migration see the instructions in [Changing Migration Target (Rolling back and forwards)](/Home/Tutorials/Migrations/Changing-Migration-Target-\(Rolling-back-and-forwards\))