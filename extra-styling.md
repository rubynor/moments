# Styling - ekstraoppgave

Legg til disse linjene **nederst** i Gemfile:

```ruby
gem 'material_icons'
gem 'bootstrap',     '4.1.1'
gem 'material-sass', '4.1.1'
```

Deretter kjør bundler, og restart rails-serveren.

```console
bundle install
```

Stopp rails serveren `CTRL+C`.

Start den igjen med `rails server`

Importer Materialize-stilsettet i `app/assets/stylesheets/application.scss` (må opprettes):

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


## Eksempel

Eksempel på hvordan du kan benytte material design til å stilsette moments-siden.

Åpne `app/views/moments/index.html.erb` i teksteditoren, erstatt innholdet i filen med følgende kode:

```ruby
<p id="notice"><%= notice %></p>

<div class="container">
  <h1>Moments</h1>

  <div class="row">
    <% @moments.each do |moment| %>

      <div class="card m-2" style="width: 18rem;">
        <div class="card-header">
          <div class="float-right">
            <%= link_to material_icon.create, edit_moment_path(moment), :class => 'card-link' %>
            <%= link_to material_icon.delete, moment, method: :delete, :class => 'card-link', data: { confirm: 'Are you sure?' } %>
          </div>
        </div>
        <div class="card-body">
          <blockquote class="blockquote mb-0">
            <%= moment.description %>
          </blockquote>
        </div>
        <%= link_to 'Gå til moment', moment, :class => 'btn btn-primary', :method => :get %>
      </div>

    <% end %>
  </div>
  <br>

  <%= button_to 'New Moment', new_moment_path, :class => 'btn btn-primary', :method => :get %>
</div>
```

Her er dokumentasjon hvis du vil stilsette de andre sidene på egenhånd: http://daemonite.github.io/material/ 

For å overstyre "primary color" erstatt innholdet i `app/assets/stylesheets/application.scss` med følgende:

```css
/*
*= require material_icons
*/

$primary: (
  color: #000000,
  dark:  darken(#ffc107, 10%),
  light: lighten(#ffc107, 10%)
);

@import "material";
```
