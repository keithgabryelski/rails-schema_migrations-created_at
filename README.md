# rails-schema_migrations-created_at

add created_at to schema_migrations

```ruby
class SchemaMigrationsTableGetsCreatedAt < ActiveRecord::Migration
  def up
    add_column :schema_migrations, :created_at, :datetime
    ActiveRecord::SchemaMigration.where(created_at: nil).update_all('created_at = now()')
    ActiveRecord::SchemaMigration.reset_column_information
    change_column :schema_migrations, :created_at, :datetime, null: false
  end

  def down
    remove_column :schema_migrations, :created_at
  end
end
```
