# Migrations

The migration will create five (or six if you use teams feature) tables in your database:

* `roles` — stores role records.
* `permissions` — stores permission records.
* `teams` — stores teams records (Only if you use the teams feature).
* `role_user` — stores [polymorphic](https://laravel.com/docs/eloquent-relationships#polymorphic-relations) relations between roles and users.
* `permission_role` — stores [many-to-many](https://laravel.com/docs/eloquent-relationships#many-to-many) relations between roles and permissions.
* `permission_user` — stores [polymorphic](https://laravel.com/docs/eloquent-relationships#polymorphic-relations) relations between users and permissions.

## Known Issue

**Resolving SQLSTATE[42000] Error Due to Long Index Names**

When running database migrations, you might encounter the error ```SQLSTATE[42000]: Syntax error or access violation: 1059 Identifier name 'permission_user_user_id_permission_id_user_type_my_custom_team_id_unique' is too long.``` This occurs when the name of a unique index exceeds the database's character limit.

***Solution: Customizing Index Names***

To solve this issue, you can specify a custom name for your unique index in migration file.

```php
// Before:
$table->unique(['user_id', 'permission_id', 'user_type', 'my_custom_team_id']);

// After:
$table->unique(['user_id', 'permission_id', 'user_type', 'my_custom_team_id'], 'customized_shorter_index_name');
```
