# Passikuvakone

**Tee passikuva itse ilman valokuvaamoa.**

🔗 **Käytä työkalua: [okkupokku.github.io/passikuvakone](https://okkupokku.github.io/passikuvakone/)**

Passikuvakone tekee itse otetusta valokuvasta poliisin passikuvaohjeen mittavaatimukset täyttävän kuvatiedoston (500 × 653 px, JPEG, alle 250 kt) ja neuvoo, miten kuva ladataan poliisin valokuvapalvelimelle. Tämä korvaa valokuvaajalla käynnin passin tai henkilökortin uusinnassa.

Työkalu on epävirallinen apuväline, eikä sillä ole yhteyttä poliisiin tai muuhun viranomaiseen. Lopullisen arvion kuvasta tekee aina poliisi.

## Ominaisuudet

- **Kuvausohjeet**: etäisyydet, zoomisuositus ja valaistus havainnekuvineen, jotta kuva onnistuu kotikonstein
- **Automaattinen rajaus**: pää tunnistetaan siluetista ja sovitetaan poliisin apuviivastoon (päälaki 56–84 px, leuankärki 96–124 px, keskilinja ±21 px); hienosäätö onnistuu käsin raahaamalla ja zoomaamalla
- **Soveltuvuusarvio**: selvästi sopimaton kuva (esim. maisema tai ryhmäkuva) hylätään heti, ja rajatapauksista varoitetaan
- **Laatutarkistukset**: tarkkuus, terävyys, valoisuus ja taustan tasaisuus mitataan lopullisesta kuvasta; ilmeen ja asennon kaltaiset asiat kuitataan tarkistuslistalta kuvan vierestä
- **Taustan tasaus (valinnainen)**: yhtenäinen tausta tunnistetaan kuvan reunoilta ja korvataan tasaisella sävyllä; vaatii aina käyttäjän vahvistuksen siitä, ettei mitään peittynyt
- **Vienti**: tarkalleen oikea koko ja muoto, pakkauslaatu säädetään automaattisesti alle 250 kilotavun
- **Ohjeet poliisin palvelimelle**: vaiheittainen polku lupakuvienvastaanotto.fi-palveluun ja kuvatunnuksen käyttöön hakemuksessa
- **Kolme kieltä**: suomi (oletus), ruotsi ja englanti; kielen voi jakaa linkissä (`#sv`, `#en`)

## Tietoturva ja yksityisyys

- Kuva ei koskaan poistu käyttäjän laitteelta: kaikki käsittely tapahtuu selaimessa JavaScriptillä
- Kuvaa tai sen osia ei lähetetä millekään palvelimelle
- Ei evästeitä, ei analytiikkaa, ei selaimen pysyväistallennusta; välilehden sulkeminen tyhjentää kaiken muistista
- Ainoa verkkoliikenne on nimetön latauslaskuri (+1-viesti abacus.jasoncameron.dev-palveluun kuvan tallennuksen yhteydessä), joka ei sisällä kuvadataa eikä henkilö- tai laitetietoja ja jonka estäminen ei haittaa työkalun toimintaa

Tarkempi kuvaus on sivun Dokumentaatio-välilehdellä.

## Tekninen toteutus

Koko sovellus on yksi HTML-tiedosto (`index.html`) ilman riippuvuuksia, kirjastoja tai käännösvaihetta: HTML, CSS ja vanilla JavaScript. Konenäön sijaan käytetään klassisia heuristiikkoja:

- **Pään tunnistus**: reunoilta lähtevä flood fill erottaa taustan, ja siluetin leveysprofiilista löydetään päälaki, posket, leukalinja ja leuankärki (profiili kapenee leukaa pitkin minimiin ja levenee sitten kaulaan)
- **Soveltuvuusportti**: reunakaistojen reunatiheys, kasvoellipsin iho-osuus ja taustan yhtenäisyys erottelevat kelvollisen kasvokuvan esimerkiksi maisemasta
- **Laatumittarit**: Laplace-varianssi (terävyys), luma-keskiarvo (valoisuus) ja reunakaistojen luma-hajonta (taustan tasaisuus)

Heuristiikkojen raja-arvot on kalibroitu poliisin hyväksymillä esimerkkikuvilla, ja ne löytyvät koodista vakioina. Jos löydät kuvan, jolla rajaus tai arvio menee pieleen, kuvaile tapaus issuena: millainen tausta, hiukset ja valaistus, ja mitä mittausarvoja sivu näytti. Älä liitä kasvokuvia julkisiin issueihin.

## Kehittäminen ja julkaisu

Sivu julkaistaan GitHub Pagesilla suoraan tämän repon `main`-haarasta. Muutokset tehdään `index.html`-tiedostoon, ja Pages päivittää julkaistun sivun automaattisesti parissa minuutissa. Paikallinen testaus onnistuu avaamalla tiedosto suoraan selaimeen.

Jos haarautat (fork) tämän projektin, vaihda latauslaskurin nimiavaruus (`COUNTER_NS` koodissa) omaksesi, jotta laskurit eivät mene ristiin.

## Vastuuvapaus

Poliisin passikuvaohje kieltää kuvan digitaalisen muokkaamisen. Taustan tasaus on muokkausta, ja sen käyttö on käyttäjän oma valinta ja vastuulla. Vastuu poliisille ladattavan kuvan oikeellisuudesta on aina kuvan lataajalla. Varminta on ottaa kuva suoraan tasaista, vaaleaa seinää vasten ja käyttää työkalua vain rajaukseen ja tarkistuksiin.

---

## In English

**Passikuvakone** ("Passport Photo Maker") is a free, browser-only tool that turns a self-taken photo into an image file meeting the Finnish police passport photo specification (500 × 653 px, JPEG, under 250 kB), and guides you through uploading it to the police photograph server. Everything runs locally in the browser; the photo never leaves your device. The tool is unofficial, and the final assessment of any photo is always made by the Finnish police. The interface is available in Finnish, Swedish and English: [okkupokku.github.io/passikuvakone](https://okkupokku.github.io/passikuvakone/) (append `#en` for English).
