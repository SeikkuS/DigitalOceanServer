# H7 DigitalOceanServer

## x)

- VPS:n perustamiseen DigitalOceaniin Ubuntu 16.04 LTS:llä annetaan vaiheittaiset ohjeet.

- Korostaa vahvojen salasanojen käytön tärkeyttä koko prosessin ajan.

- Selitetään, miten luodaan uusi VPS-tili, kirjaudutaan sisään ensimmäistä kertaa, perustetaan palomuuri, luodaan sudo-käyttäjä, lukitaan pääkäyttäjätili, poistetaan pääkäyttäjän kirjautuminen käytöstä SSH:lla, päivitetään ohjelmisto ja tehdään palvelimesta julkisesti käytettävissä oleva.

- Mainitaan ilmaisen VPS:n ja .me-verkkotunnuksen saatavuus GitHub Education -opiskelijapaketin kautta.

- Antaa lyhyet ohjeet julkisen DNS-nimen lisäämisestä NameCheapissa.

## a) 

Tein tilin Digital Oceaniin, jonka yhdistin Github Education -pakettiin. Tein Dropletin, jossa oli muistia 1GB ja tallenustilaa 25GB.

Tämän jälkeen toteutin seuraavat komennot virtualboxin terminaalissa:

      ssh root@(palvelimen IPv4 osoite)
      
Kirjauduin antamallani salasanalla. ja vastasin kysymykseen "yes".

![kuva](https://user-images.githubusercontent.com/105205141/217605632-6575ef34-8b4e-4656-9673-b05dffd0afdb.png)
    
## b)

Tämän jälkeen asensin itselleni UFW:n ja tein reiän palomuuriini itselleni ja nettisivuille komennoilla:

      sudo apt-get install ufw
      ufw allow 22/tcp
      ufw allow 80/tcp
      ufw enable
      
sitten tein käyttäjän ja annoin sille oikeudet:

      sudo adduser tero
      sudo adduser tero sudo
      sudo adduser tero adm
      sudo adduser tero admin
      
Luotuani tilin suljin root tilini:

      sudo usermod --lock root
      sudoedit /etc/ssh/sshd_config
      
Avattuani sshd_configin painamalla CTRL + W, etsin hakupalkilla "PermitRoot" ja painoin Enter. Muutin sen jälkeen seuraavan komennon nuolen osoittamalla tavalla:
      
      PermitRootLogin yes --> PermitRootLogin no
      
Painoin CTRL X, tallensin painamalla y ja painoin Enter, jolloin muutettu tiedosto tallennetaan samana tiedostona vaihtamatta nimeä.

      sudo service ssh restart
      
Lopuksi päivitin sovellukset kirjoittamalla

      sudo apt-get update
      sudo apt-get upgrade
      
      
## c)

Sitten asensin Apache2-palvelimeni kirjoittamalla: 

      sudo apt-get install apache2

ja käynnistin sen:

      sudo systemctl start apache2
      
Tämän jälkeen kokeilin yhdistää varsinaisella tietokoneellani palvelimeeni IP-osoitteella:

![kuva](https://user-images.githubusercontent.com/105205141/217608012-a3ae068c-375b-49fd-b23a-55d767e014f0.png)

Testasin muuttuuko index.html tiedosto kirjoittamalla seuraavan komennon:

      echo moi | sudo tee /var/www/html/index.html
      
sitten latasin sivun uudelleen: 

![kuva](https://user-images.githubusercontent.com/105205141/217610142-f1559d74-44c6-4317-9347-c644b14ca7c1.png)

d)
