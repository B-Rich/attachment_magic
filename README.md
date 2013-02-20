# Attachment Magic

Rails 3.x compatible, file-system-storage-only version of the good old `act_as_attachment` plugin.

## Install

```shell
gem install attachment_magic
```

Or put it in your `Gemfile`

```ruby
gem 'attachment_magic', :github => 'magiclabs/attachment_magic'
```

## Usage

Create a model that should have an attachment:

```shell
rails generate model Document filename:string content_type:string size:string more fields ...
```

`filename`, `content_type` and `size` are mandatory. Feel free to add more fields of your choice.

Call this class method in your model:

```ruby
class Document < ActiveRecord::Base
  has_attachment
end
```

## Forms

```erb
<%= form_for :attachment, :html => { :multipart => true } do |f| %>
  <p><%= f.file_field :uploaded_data %></p>
  <p><%= submit_tag :Save %>
<% end %>
```

The `:html => { :multipart => true }` is important.

## Confguration

*  `:content_type`
  - Allowed content types.
  - Allows all by default.
  - Use `:image` to allow all standard image types.
*  `:min_size`
  - Minimum size allowed.
  - `1` byte is the default.
*  `:max_size`
  - Maximum size allowed.
  - `1.megabyte` is the default.
*  `:size`
  - Range of sizes allowed.
  - `1..1.megabyte` is the default.
  - This overrides the `:min_size` and `:max_size` options.
*  `:file_system_path`
  - Path to store the uploaded files.
  - Uses `public/#{table_name}` by default.

### Examples:

```ruby
has_attachment :max_size => 1.kilobyte
has_attachment :size => 1.megabyte..2.megabytes
has_attachment :content_type => 'application/pdf'
has_attachment :content_type => ['application/pdf', 'application/msword', 'text/plain']
```

## Validations

If you want to add validations, just call this class method in your model:

```ruby
...
  validates_as_attachment
...
```

## License

MIT License
