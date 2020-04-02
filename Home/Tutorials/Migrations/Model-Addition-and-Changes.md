[[_TOC_]]

# Introduction
In a Code First environment there are several steps to complete.

## Creating a new model/entity 
1. Add a new class in `*.Business.Models`
1. Inherit from `EntityBase` to ensure common, required, meta data like `Id`.
1. Add any other required properties.
1. Create a Map file

## Updating a Model
When adding a new property or relationship to a model, you must follow the steps given under [Map File - Updating](#Updating)

## Map File
A Map file is required when creating new Entities. A map file uses the Fluent API to describe how the Code First model should translate to the data storage solution. Oracle, for instance, has many annoying naming/storage restrictions that we do not want represented in the code for normal use. Thus, the mapping file can allow clean code but also allow the data solution to work under the constraints.

Use `nameof` whenever possible. In the event the property or class name changes this will cause a migration to pick this rename up as a change and rename the database object as well.

> Be careful not to included the meta columns more then once.

### Creating a new map
1. Create a map file called `[Entity]Map` e.g. `UserMap`.
1. You must inherit from `IEntityTypeConfiguration<T>`
1. Implement the `Configure(EntityTypeBuilder<T> builder)` method:
   1. The table must be described as 
`builder.ToTable(nameof(User));`
   1. The PK must be described as 
`builder.HasKey(t => t.Id);`
   1. The PK must also be described as a property as 
`builder.Property(t => t.Id).HasColumnName($"{nameof(User)}Id");`
   1. See Updating steps below

### Updating
   1. You must describe each property in the Entity at minimum as 
`builder.Property(t => t.[Property]).HasColumnName(nameof([Entity].[Property]));`.
 There are other chains that can be applied such as `IsRquired`

### Relationships
Assuming that there is are `User`, `UserPreference`, `UserUnitData` classes where `User` can have one `UserPreference` but multiple `UserUnitData` you would describe the relationship as:
```
builder.HasOne(pr => pr.UserPreference).WithOne(dep => dep.User)
    .HasForeignKey<UserPreference>(x => x.UserId);
builder.HasMany(pr => pr.UserUnitData).WithOne(dep => dep.User);
```

### Metadata

You must ensure that all of the meta data columns inherited from `EntityBase` are included in the map as:

```
builder.Property(t => t.IsDeleted).HasColumnName(nameof(EntityBase.IsDeleted));
builder.Property(t => t.CreatedBy).IsRequired().HasMaxLength(100).HasColumnName(nameof(EntityBase.CreatedBy));
builder.Property(t => t.ModifiedBy).IsRequired().HasMaxLength(100).HasColumnName(nameof(EntityBase.ModifiedBy));
builder.Property(t => t.CreatedDate).HasColumnName(nameof(EntityBase.CreatedDate));
builder.Property(t => t.ModifiedDate).HasColumnName(nameof(EntityBase.ModifiedDate));
```
Be sure to validate that no additional columns have been added in the base class. Please be sure to notify the team lead to update this article.