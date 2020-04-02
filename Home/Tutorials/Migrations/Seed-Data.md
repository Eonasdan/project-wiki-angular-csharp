With Entity Framework it is possible to repopulate data in the database. This is very useful for ensuring that a default user for instance is available when deploying or a new developer comes in.
They way we provide this seed data in this project structure also makes it easy to have mock objects for test.

To add new seed data, add a new entry to `SeedData.cs` located in the business project. Please pay close attention to the existing items as an example of how a new entry should look.
Here’s an example of an entry. It must be `public`, `static` and `readonly`. Make sure that the meta columns (created, modified) are setup exactly like the example.

```
public static readonly Code CodeSystemConstant = new Code { 
    Id = CodeCategories.SystemConstant, CodeDescription = "System Constant",
    Data1Description = "", Data2Description = "", Data3Description = "", 
    CreatedBy = CreatedBy, CreatedDate = CreatedAt, ModifiedBy = CreatedBy,
    ModifiedDate = CreatedAt
};
```

Here’s an example of referencing one entry from another. The benefit of doing this is that the referential integrate between parent and child.

```
public static readonly CodeValue CodeValue3 = new CodeValue { 
    Id = 3, CodeId = CodeSystemConstant.Id, CodeValueKey = SystemConstants.PageCounts,
    CodeValueDescription = "Page Counts To Show", Data1 = "25", Data2 = "",
    Data3 = "", SequenceNumber = 1, CreatedBy = CreatedBy,
    CreatedDate = CreatedAt, ModifiedBy = CreatedBy, ModifiedDate = CreatedAt
};
```

To get your new entries in the database, you will need to add the entries to the Db Context. Go to `ApplicationDbContext` located in the DAL project. Look for `OnModelCreating`, you will need to add your `SeedData.*` to either an existing `modelbuilder*.HasData` or add a new section matching the `<EntityType>`

```
modelBuilder.Entity<Code>().HasData(
    SeedData.CodeSystemConstant,
    …
    SeedData.ProfileStatus,
    [YOUR ITEM GOES HERE]
);
```

Once this is done, you will need to [add a new migration](/Home/Tutorials/Migrations/Adding-a-migration). Because we have added the new seed data to the model builder, the migration will automatically have the `InsertData` and `DeleteData`
