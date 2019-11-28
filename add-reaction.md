

 Når vi ser på et Moment, er det fint å kunne komme med sin positive reaksjon :)
 
 Steg 1
 
 Ordne routes, slik at reaction er i kontekst av moment den tilhører
 
    #routes.rb
    
    resources :moments do
      resources :reactions
    end

du må endre i reactions controller, så den tar hensyn til konteksten (altså hvilken moment reactionen tilhører).

Forstår du git diff? Da ser du hvilke linjer som skal legges til og hvilke som skal fjernes:

    app/controllers/reactions_controller.rb
    @@ -14,7 +14,8 @@ class ReactionsController < ApplicationController

       # GET /reactions/new
       def new
    -    @reaction = Reaction.new
    +    @moment = Moment.find(params[:moment_id])
    +    @reaction = @moment.reactions.build
       end

       # GET /reactions/1/edit
    @@ -24,11 +25,11 @@ class ReactionsController < ApplicationController
       # POST /reactions
       # POST /reactions.json
       def create
    -    @reaction = Reaction.new(reaction_params)
    +    @moment = Moment.find(params[:moment_id])

         respond_to do |format|
    -      if @reaction.save
    -        format.html { redirect_to @reaction, notice: 'Reaction was successfully created.' }
    +      if @reaction = @moment.reactions.create(reaction_params)
    +        format.html { redirect_to @moment, notice: 'Reaction was successfully created.' }
             format.json { render :show, status: :created, location: @reaction }
           else
             format.html { render :new }

og du må endre Moment Show

    /app/views/moments/show.html.erb
    @@ -12,5 +12,7 @@
       <p><%= reaction.awe %></p>
     <% end %>

    +<%= link_to 'Add reaction', new_moment_reaction_url(@moment) %>
    +
     <%= link_to 'Edit', edit_moment_path(@moment) %> |


Endre Create Reaction formet:

    app/views/reactions/_form.html.erb
    @@ -1,4 +1,4 @@
    -<%= form_with(model: reaction, local: true) do |form| %>
    +<%= form_for([@moment, @reaction]) do |form| %>
       <% if reaction.errors.any? %>
         <div id="error_explanation">
           <h2><%= pluralize(reaction.errors.count, "error") %> prohibited this reaction from being saved:</h2>
    @@ -11,11 +11,6 @@
         </div>
       <% end %>

    -  <div class="field">
    -    <%= form.label :moment_id %>
    -    <%= form.text_field :moment_id %>
    -  </div>
    -

og edit og new html forms

    /app/views/reactions/edit.html.erb
    @@ -2,5 +2,4 @@

     <%= render 'form', reaction: @reaction %>

    -<%= link_to 'Show', @reaction %> |
    -<%= link_to 'Back', reactions_path %>
    +<%= link_to 'Back', moment_path(@moment) %>
    diff --git a/app/views/reactions/new.html.erb b/app/views/reactions/new.html.erb
    index 8d6c394..433c422 100644
    --- a/app/views/reactions/new.html.erb
    +++ b/app/views/reactions/new.html.erb
    @@ -2,4 +2,4 @@

     <%= render 'form', reaction: @reaction %>

    -<%= link_to 'Back', reactions_path %>
    +<%= link_to 'Back', moment_path(@moment) %>

Bare skrev du, eller leste du og? Forstår du endringene? 

Bare gjør du, blir det monkey see monkey do. Jeg tror du er bedre enn som så, se litt mer på endringene og hvilken effekt de hadde.



sdff
