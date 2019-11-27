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

Eksempel på hvordan du kan benytte material design til å stilsette nettsiden.

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
        <%= image_tag(@moment.photo, width: '200px', :class => 'card-img-top') %>
        <div class="card-body">
          <blockquote class="blockquote mb-0">
            <%= moment.description %>
          </blockquote>
          <div class="mt-4">
            <%= material_icon.mode_comment %> <%= @moment.reactions.count %>
          </div>
          <div>
          <ul class="list-group list-group-flush pt-3">
            <% @moment.reactions.each do |reaction| %>
              <li class="list-group-item"><%= reaction.awe %></li>
            <% end %>
          </ul>
          </div>
        </div>
      </div>

    <% end %>
  </div>
  <br>

  <%= button_to 'New Moment', new_moment_path, :class => 'btn btn-primary', :method => :get %>
</div>
```
