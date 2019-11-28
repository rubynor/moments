# moments
Repo for utdanningsformål :)

# Krav

* [Node.js](https://nodejs.org/en/)
* [Rails](https://rubyonrails.org/)
* [Git](https://git-scm.com/)
* [Ruby](https://www.ruby-lang.org/en/)
* [Ruby-irb](https://github.com/ruby/irb)
* En teksteditor/IDE

# Installere Yarn

Legg til yarn i pakkeregisteret
```bash
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
```

Oppdater fra pakkeregister
```bash
sudo apt update && sudo apt install yarn
```

Installer yarn
```bash
sudo apt update && sudo apt install --no-install-recommends yarn
```

# Lag en "Ruby on Rails 6" app


0. Åpne console, vi kjøre kommandolinje

```    
    Gå til hjemmeområdet: 
    $ cd
    # cd uten argument tar deg "hjem"
    $ pwd
    # du skal nå se /home/ole, om du ditt brukernavn er ole
    $ mkdir dev
    #oppretter mappen dev
    $ cd dev
    # navigerer deg inn i dev-mappen
    $ pwd
    # viser nå /home/ole/dev
    Her inne kjører du
    rails -v
    og rails new kommandoen under
```    


1. Lag et nytt rails prosjekt
 
   `rails new share-moment`
 
2. Gå inn i prosjektmappen

   `cd share-moment`

3. Initialiser versjonskontrollsystem (git)

   `git init .`

4. Legg til alle filer i git

   `git add .`

5. Lag ny commit med commitbeskjed "rails new"

   `git commit -am "rails new"`

6. Kjør opp rails webserver. Webserveren lytter på port 3000.

   `rails server`

   Sjekk at nettsiden er oppe på http://localhost:3000.

   Mulig man må installere webpacker med `rails webpacker:install`

7. Stopp webserver med

   `(ctrl+c)`

8. Generer scaffold.

   `rails generate scaffold moment description:string`

9. Legg til endringer i git.

   `git add .`
   
   `git commit  -am "scaffold moments"`

10. Oppdaterer databasen med den nye tabellen.

   `rails db:migrate`

11. Start rails webserver.

   `rails server`

12. Gå deretter til [http://localhost:3000/moments](http://localhost:3000/moments)

Vise i kode og i console

    rails console
    Moment.count
    Moment.first
    Moment.all
    pp Moment.all

http://localhost:3000/moments.json

http://localhost:3000/moments/1.json

STOPP HER, hjelp kameratene til å komme hit FELLES.

Mathias tydeliggjør forskjellen klient og server.

En av elevene starter en lokal server som er tiljengelig for de andre på det lokale nettet `rails server -b <din ip adresse>`.

CO-OP:

Få person A til å åpne sin app

Person B peke nettleser til denne og fyre av requests (mens andre person ser i sine logger at ting skjer)

# Ett steg videre

Gå videre til [steg 2](step2.md).
