[[_TOC_]]


# To apply a migration run:

```
update-database
```

# Rolling back

Because the migrations are timestamped you may find that you and another developer have created a migration but have checked in your code in such a way that the migration steps are out of order.

Consider Developer A creating a migration called `2_FixedColumn` and Developer B created a migration called `3_AddedTable`. Both developers update their local databases. Developer A merges their code first, when Developer B takes master they will have migration `1_Initial` and `3_AddedTable` applied. 

In order for Developer B to get their database in a working state, they will have to rollback to `1_Initial` and then roll forward with `update-database`. This is perhaps the most annoying issue when working with EF.

To roll back run 

```
update-database -m:[NAME]`
```

For Developer B this would look like:

```
update-database -m:Initial //rollback
update-database //applies both 2 and 3
```