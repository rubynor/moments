# moments
Repo for utdanningsformål :) 

# Create Ruby on Rails 6 app

    rails new share-moment
    cd share-moment

    git init . 
    git add .
    git commit -am “rails new”
    rails server # kjører opp server og lytter på localhost:3000 
      ( krever nodejs og webpacker om ikke installert) (rails webpacker:install, husk git commit)
    stopp server (ctrl + c)
    rails generate scaffold moment description:string
    git add .
    git commit  -am "scaffold moments"
    rails db:migrate # oppdaterer databasen med den nye tabellen
    rails server (gå til localhost:3000/moments )

Vise i kode og i console

    rails console
    Moment.count
    Moment.first
    Moment.all
    pp Moment.all

http://localhost:3000/moments.json
http://localhost:3000/moments/1.json

STOPP HER, hjelp kameratene til å komme hit
FELLES: Mathias tydeliggjøre forskjellen klient og server.
CO-OP:
Få person A til å åpne sin app
Person B peke nettleser til denne og fyre av requests (mens andre person ser i sine logger at ting skjer)

ETT STEG VIDERE
Share reactions on those cool moments

    rails generate scaffold reaction moment:references awe:string

sjekk models etc. 

    rails db:migrate

    rails console
    Reaction.count
    amoment = Moment.first
    reaction = Reaction.create!(moment: amoment, awe: "Aaaawwww")
    reaction.moment # viser at man kan hente tilknyttet objekt
    
    # hva med andre veien?
    moment.reactions 
    # hvorfor gikk det ikke? la oss fikse.
    

legg til `has_many :reactions` i moment.rb

    rails console
    Moment.first.reactions
    
