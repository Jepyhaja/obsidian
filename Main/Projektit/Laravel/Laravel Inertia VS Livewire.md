### 1. Perus Laravel Setup
#### 1.1. Laravel paketin asennus composerilla 
`composer create-project laravel/laravel kspk`
 
 #### 1.2. Luodaan muutama Model ja Migraatiot niille
 `php artisan make:model haul -m`
 `php artisan make:model fish -m`
 
 Modelit löytyy /app/models/ kansiosta
 Migraatiot löytyy /database/migrations/ kansiosta
 
 -m argumentillä saadaan myös migraatio modelin luonnin yhteydessä
 -f argumenttillä saataisiin luotua myös factory, jolla voidaan luoda puppudataa kantaan.
 
 #### 1.3. Kirjoitetaan pieni seeder fish modelille
 `php artisan make:seeder FishSeeder`
 
 Seederit löytyy /database/seeders/ kansiosta.
 
 Seedereillä saadaan nopeasti täytettyä kantaan tavaraa, jolla päästään testaamaan sovellusta. Tässä tapauksessa seederillä alustetaan eri kalalajeja.
 
 #### 1.4. Ajetaan migraatiot ja seederit
 
`php artisan migrate`
`php artisan db:seed DatabaseSeeder`
`php artisan db:seed FishSeeder`

Kantaan pitäisi olla ilmestynyt kalalajit fish-tauluun, sekä 10 puppu käyttäjää users-tauluun.

Seederit voi ja kannattaisi laittaa kaikki pyörimään DatabaseSeederissä, jolloin kaikki seedattava data menee yhdellä komennolla ja voidaan myös resetoida kanta yhdellä komennolla:
`php artisan migrate:fresh --seed` --seed perään voidaan antaa seeder classin nimi, muutoin käyttää tuota DatabaseSeederiä.

### 2. Livewire käyttöön
#### 2.1. Breeze boilerplate käyttöön
`composer require laravel/breeze --dev`
`php artisan breeze:install`
`npm install && npm run dev`

#### 2.2. Luodaan livewire "full page"-komponentti
`php artisan livewire:make Pages/Users/Index`
Luo komponentille "Controllerin" `/app/http/livewire/pages/users/index.php` ja "Viewin" `/resources/views/livewire/pages/users/index.blade.php`

###### Lopppu hienous selvinnee itse tiedostoista

### 3. Inertia.js käyttöön
#### 3.1. Breeze boilerplate käyttöön
`composer require laravel/breeze --dev`
`php artisan breeze:install react`
Tässä hienous että breezeen on integroitu inertia asennus sekä reactille että vuelle.
`npm install && npm run dev`

#### 3.2 Layout pohjan luonti

/views kansioon täytyy luoda app.blade.php tiedosto josta `inertia`-branchilla hyvin simppeli versio. Tämä on koko sovelluksen "wrapperi".

#### 3.3. Luodaan Controller
`php artisan make:controller UserController`

#### 3.4. Luodaan react komponentit
react komponentit tulee kansioon /resources/js/pages/
Nyt tehdään tuonne kansio users, jonne tehdään komponentit index.js ja show.js

###### Lopppu hienous selvinnee taas itse tiedostoista