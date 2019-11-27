# Styling - ekstraoppgave

Legg til disse linjene i Gemfile:

```ruby
gem 'material_icons'
gem 'bootstrap',     '4.1.1'
gem 'material-sass', '4.1.1'
```

Deretter kjør bundler, og restart rails-serveren.

```console
bundle install
```

Importer Materialize stilsettet i `app/assets/stylesheets/application.scss` (må opprettes):

```scss
/*
*= require material_icons
*/
@import "material";
```

Slett application.css

```console
$ rm app/assets/stylesheets/application.css
```

Åpne `app/views/moments/index.html.erb` i teksteditoren.

Endre siste linje fra:
```ruby
<%= link_to 'New Moment', new_moment_path %>
```

til:
```ruby
<%= button_to 'New Moment', new_moment_path, :class => 'btn btn-primary', :method => :get %>
```

Refresh siden (http://localhost:3000/moments) og se at "New Moment" knappen har forandret utseende.
