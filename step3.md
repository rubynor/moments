 # Et bilde sier mer enn tusen ord
 
 Vi skal nå gjøre det mulig å laste opp bilde til et moment og vise dette.

 Vi følger guiden på https://edgeguides.rubyonrails.org/active_storage_overview.html
 
 Først vil jeg konfigurere opp en streng regel som gjør feil parametre i requests tydelige i stedet for usynlige
 
 Legg til denne linjen i `config/application.rb`
 
 ```ruby
 config.action_on_unpermitted_parameters = :raise
 ```
 
 Tilbake til guiden for bildeopplastning. Vi må kjøre installasjon:
 
    rails active_storage:install
 
 Vi må fortelle hvilken klasse/model som skal ha bildet.
 
 Det definerer vi i filen `app/models/moment.rb`
 
 ```ruby
 has_one_attached :photo
 ```

 Deretter må legge til opplastningen i create/edit skjemaet i filen `app/views/moments/_form.html.erb`:

 ```ruby
 <%= form.file_field :photo %>
 ```
 
 Nå sendes bilde fra klienten til serveren, men for at serveren skal kunne mota bilde må vi fortelle den at den aksepterer bilder. dette gjør vi ved å legge til "photo" som paramater i metoden moments_param fra kontrolleren `app/controllers/moments_controller.rb`
 
 ```ruby
 def moment_params
  params.require(:moment).permit(:description, :photo)
 end
 ```

 Til slutt må vi vise bildet, sammen med kommentarer i filen `app/views/moments/show.html.erb`

 ```ruby
   <p>
     <strong>
     <%= @moment.description %>
     </strong>
   </p>

   <p>
     <%= image_tag(@moment.photo, width: '500px') if @moment.photo.attached? %>
   </p>
   <p> <%= @moment.reactions.count %> reaksjoner </p>

   <% @moment.reactions.each do |reaction| %>
     <p><%= reaction.awe %></p>
   <% end %>
 ```

Fortsett til [ekstraoppave - stilsetting](extra-styling.md)

Fortsett til [ekstraoppave - Add Reaction to Moment](add-reaction.md)

Ekstraoppgave: [brukerinnlogging](https://github.com/rubynor/rails-setup#9-devise-for-handling-authentication)
