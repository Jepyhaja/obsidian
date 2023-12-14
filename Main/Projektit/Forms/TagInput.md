# Variants
[[AutocompletingTagInput]]-vartiantti 

## Base variant:

```php

```
# Toiminto
- [[Input]], joka luo [[Tags]] kun syötteessä tulee välilyönti tai painetaan "Add tag"-nappia
- Esim. "melee spell dark" luo automaattisesti tagit "melee" ja "spell", dark jää syötekenttään odottamaan "Add tag"-napin painallusta
- Ennakoiva syöte

##### Käyttökohteet:
[[Loihdin]],



### Kehitettävää

Muokkaa toimimaan siten että komponentti ottaa vastaan listan elementeistä, joista voidaan tehdä tageja. Jos tätä ei anneta luodaan syötteestä tagit. Vältytään ylimääräisiltä queryiltä.
#### DONE