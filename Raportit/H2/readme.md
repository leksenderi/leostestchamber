http://terokarvinen.com/2017/aikataulu-%e2%80%93-palvelinten-hallinta-ict4tn022-2-%e2%80%93-5-op-uusi-ops-loppukevat-2017-p2

# Harjoitus 2

* a) Tee tämä kotitehtävä GitHubiin MarkDownilla
* b) Tee puppet-moduli, joka tekee asetukset jollekkin komentorivi- tai graafisen käyttöliittymän ohjelmalle.

Kone on bootattu Xubuntu 16.04.01 version livetikulta klo 23:35 (TryFree-versio)
 
# HUOM! GitHub ohjeet löytyy pohjalta

Aloitetaan ajamalla peruskomennot 

	setxkbmap fi
	sudo apt-get update
	
Kehitellään itsellemme pienehkö puppet-moduuli.
Otetaan vaikka yksinkertainen alias-moduuli.
Lisätään bash.bashrc tiedostoon koodinpätkä, missä määritellään alias.
Tehdään vaikka yksinkertainen "ls" alias, niin että "h" kirjain tekee saman komennon.

	cd /etc/
	ls
	sudo nano bash.bashrc

Lisätään yläosaan seuraava tiedonpätkä:

	alias h="ls"

Tämän jälkeen asennetaan puppet ja luodaan init.pp tiedostolle oma kansiopolku

	sudo apt-get install puppet

Kansiopolku sekä init.pp tiedoston luonti:
	
	/etc/puppet/modules/aliasmoduuli/manifests
	sudo nano init.pp

Init.pp tiedostoon laitoin seuraavat tiedot:

	class aliasmoduuli{

        file {'/etc/bash.bashrc':
        content => template('aliasmoduuli/bash.bashrc.erb')

		}
	}
Muistetaan tehdä vielä myös templates kansio, minne kopioidaan tuo bash tiedosto.

	cd .. 
tai
	
	cd /etc/puppet/modules/aliasmoduuli
	sudo mkdir templates

tämän jälkeen kopioidaan etc:ssä sijaitseva bash.bashrc ja liitetään se meidän templates kansioon bash.bashrc.erb muodossa

	sudo cp bash.bashrc /etc/puppet/modules/aliasmoduuli/templates/bash.bashrc.erb

Muistetaan vielä ajaa puppetilla komento, jotta moduuli lähtee käyntiin
	
	sudo puppet apply -e 'class {"aliasmoduuli":}'

Ei ongelmia, joten avataan terminaali uudestaan ja voila! "H" kirjain pamauttaa saman kuin "ls"

Tämän jälkeen palautus GitHubbiin, nopeat ohjeet tästä

Ensiksi asennetaan git
	sudo apt-get install git
Tämän jälkeen kopioidaan oman github käyttäjän hakemistot koneelle
	git clone https://github.com/leksenderi/Palvelinten-hallinta-2017.git
Sen jälkeen ennalta määrättyyn kansioon luodaan a) tehtävän vaatima MarkDown tiedosto, tässä tapauksessa omani on 

	cd Palvelinten-hallinta-2017
	sudo nano h2.md

tämän jälkeen raportti siirretään Githubiin seuraavilla komennoilla

	git add .
	git commit
	git pull
	git push

Harjoitus lopetettiin 00:29
	
