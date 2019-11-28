
# React to awesome moments

Bygger på README.md i https://github.com/rubynor/moments

Share reactions on moments

    rails generate scaffold reaction moment:references awe:string

Sjekk models etc. 

    rails db:migrate

    rails console
    Reaction.count
    amoment = Moment.first
    reaction = Reaction.create!(moment: amoment, awe: "Aaaawwww")

Viser at man kan hente tilknyttet objekt

    # i rails console
    reaction.moment
    
hva med andre veien?

    # i rails console
    moment.reactions 
    # hvorfor gikk det ikke? la oss fikse.
    

Legg til dette i `app/models/moment.rb`

    has_many :reactions

Kjør deretter
    rails console
    Moment.first.reactions

Hva gjør egentlig denne?

Svaret ligger i output.

Et ORM mapper fra objekter til SQL. så `has_many` koblingen gjør at du slipper å skrive SQL direkte.

Du ser i console hvilken SQL-spørring som kjøres for å hente dataene fra tabellen.

Vise reaksjonene på et øyeblikk (moment)

    <p id="notice"><%= notice %></p>

    <p>
      <strong>
        <%= @moment.description %>
      </strong>
    </p>

    <p> <%= @moment.reactions.count %> reaksjoner </p>

    <% @moment.reactions.each do |reaction| %>
      <p><%= reaction.awe %></p>
    <% end %>

    <%= link_to 'Edit', edit_moment_path(@moment) %> |
    <%= link_to 'Back', moments_path %>



Gå videre til [steg 3](step3.md) (bilde opplasting).
