 # Et bilde sier mer enn tusen ord
 
 Vi skal nå gjøre det mulig å laste opp bilde til et moment og vise dette. Vi følger guiden på 
 
 https://edgeguides.rubyonrails.org/active_storage_overview.html
 
 Først vil jeg konfigurere opp en streng regel som gjør feil parametre i requests tydelige i stedet for usynlige
 
    # i config/application.rb, legg til denne
    config.action_on_unpermitted_parameters = :raise
 
 Tilbake til guiden for bildeopplastning. Vi må kjøre installasjon:
 
    rails active_storage:install
 
 Vi må fortelle hvilken klasse/model som skal ha bildet, og det er moment.
 
     moment.rb
     has_one_attached :photo

Vi må legge til opplastningen i create/edit formet:

    app/views/moments/_form.html.erb
    <%= form.file_field :photo %>

Vi må vise bildet, sammen med kommentarer

    <p>
      <strong>
      <%= @moment.description %>
      </strong>
    </p>

    <p>
      <%= image_tag(@moment.photo, width: '500px') %>
    </p>
    <p> <%= @moment.reactions.count %> reaksjoner </p>

    <% @moment.reactions.each do |reaction| %>
      <p><%= reaction.awe %></p>
    <% end %>      
