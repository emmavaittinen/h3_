#H3 Versionhallinta

Tämä harjoitus on osa kurssia Palvelinten hallinta (http://terokarvinen.com/2020/configuration-managment-systems-palvelinten-hallinta-ict4tn022-spring-2020/)

Harjoituksen tekemisessä käytin apuna opettajan ohjeita: http://terokarvinen.com/2016/publish-your-project-with-github

Sekoilin alussa vähän sen kanssa, miten harjoitus tehdään ja mitä pitää oikeasti tehdä.

Aloitin tehtävän tekemisen joskus 13.40 heti torstaina tunnin jälkeen. Aloitin asentamalla git:n virtuaalipalvelimelleni, mutta se olikin jo siellä valmiiksi asennettuna. Se on DigitalOcean:in kautta hankittu. Sitten loin kansion, jonne laitan kaikki git-juttuni. $mkdir gitTesti. Sitten loin kansion h3, mutta sitten tajusin tehneeni väärin ja poistin kansion. $ git init h3 -komennolla tehdään git-kansio. Sitten $nano README (sen tekeminen kannattaa tehdä ensimmäisenä). $ git add . (tällä saan sen luomani tiedoston tallennettua) $ git commit (tällä saan kommentoitua sitä). Nyt se kysyi, kuka olen. Tässä vaiheessa menen githubin nettisivulle luomaan sen repositoryn.

www.github.com ja kirjaudun sisään aiemmin luomallani tunnuksella. + new repository. Nimeksi h3, description: Harjoitus 3 kurssilla Palvelinten hallinta, public, license: GNU v.3.0. Create repository. 

Nyt tajusin, että tuo kansion ja README:n luominen olivat turhaa, joten poistan ne molemmat. Tai yritin poistaa. Sen tekeminen vaikutti aika vaikealta, joten annoin sen vain olla siellä.

Nyt luon käyttäjätunnuksen gitTesti-kansiolleni. $git config --global user.email säköposti@mail.com. $git config --global user.name Nimi Sukunimi. Laitoin tuohon github:issa käyttämäni tiedot. Lisäksi laitan komennon, joka muistaa salasanan tunnin ajan: $ git config --global credential.helper "cache --timeout=3600".

Seuraavaksi kloonaan repositoryn github:n nettisivulta omaan gitTesti-kansiooni. Kopioi github sivuni osoite. $git clone https://github.etcetc

MUTTA se saakelin h3-kansio oli jo siellä. No, käyn sitten githubissa luomassa uuden repositoryn uudella nimellä: h3_

Kloonaus onnistui. En vielä tee mitään tiedostoa sinne vaan siirryn nyt tehtävien tekemiseen.

----------------------------------------------

d) Näytä omalla git-varastollasi esimerkit komennoista ‘git log’, ‘git diff’ ja ‘git blame’. Selitä tulokset.

Teen tämän luomalla README-tiedoston gittiin. $nano README. Kirjoita: Tämä on harjoitus. $ git add . $ git commit (Add purpose to README). Päätteen mukaan tiedoston lisääminen onnistui. Käyn katsomassa github:ista. *facepalm* ei ollut vielä tullut, koska pitää vielä ajaa pull ja push komennot.

$git pull. Already up to date. $git push. Anna username ja password. Counting objects: 3, done.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 315 bytes | 315.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/emmavaittinen/h3_.git
   43d3da4..060eabd  master -> master

Nyt käyn katsomassa nettisivua. Sinne se oli tullut. (kts kuva 1 sivulla https://emmantutorial.school.blog/2020/04/19/ph-h3-kuvat/

Katsotaan nyt, mitä komento git log sanoo: 
commit 060eabd3befecb0b613260fd225cf3422cdeb672 (HEAD -> master, origin/master, origin/HEAD)
Author: 
Date:   Thu Apr 16 10:50:35 2020 +0000
    Add purpose to README
commit 43d3da4a1f75822063ac8eff42cb649dedff2b35
Author: 
Date:   Thu Apr 16 10:47:40 2020 +0000
    Initial commit

Tämä kertoo, kuka teki, milloin teki ja mitä teki.

Seuraavaksi komento git diff: ensimmäisellä ajolla ei tapahtunut mitään. "git-diff - Show changes between commits, commit and working tree, etc" eli ei kun  vain tekemään muutoksia. Yritin komennolla sudoedit heippa.txt, pääte pyysi sudon salasanaa käyttäjälle, annoin sen, tuli seuraava: sudoedit: heippa.txt: editing files in a writable directory is not permitted. Eli näköjään ei voi sudotella git-kansiossa. Tein sitten nano heippa.txt (kirjoita: Heippa hei). Käytin sitten opettajan antamaa komentoriviä, jossa on kaikki tarvittavat komennot: git add . && git commit; git pull && git push. Se pyysi commit-kommenti, sitten se ajoi sen läpi githubiin. Seuraavaksi (tämän sivun ohjeiden mukaan: https://www.atlassian.com/git/tutorials/saving-changes/git-diff) $echo "this is a diff exampke" > heippa.txt. Tämä muokkaa tiedoston sisällön. Aja komento git diff. Tulos näkyy kuvakaappauksena (Kuva 2 aiemmasta linkistä). Tuloksena on muutos, jonka tein tiedostolle.

Seuraavaksi $git blame. Kun ensiksi ajaa tuon pelkän komennon, tulee vain neuvoja miten sitä käytetään. "Basically, git-blame is used to show what revision and author last modified each line of a file. It's like checking the history of the development of a file. The git blame command is used to know who/which commit is responsible for the latest changes made to a file. The author/commit of each line can also been seen." (https://www.atlassian.com/git/tutorials/inspecting-a-repository/git-blame).

$git blame README: 060eabd3 (Emma Vaittinen 2020-04-16 10:50:35 +0000 1) Tämä on harjoitus

Eli tämä kertoo kuka teki, milloin, mille riville ja mitä kirjoitti. Eri komennoilla saa erilaista tietoa. Esimerkiksi git blame -L 1,5 README kertoisi juuri rivit 1 ja 5. git blame -e README kertoo kirjoittajan sähköpostin eikä nimeä.

-------------------------------

e) Tee tyhmä muutos gittiin, älä tee commit:tia. Tuhoa huonot muutokset ‘git reset –hard’. Huomaa, että tässä toiminnossa ei ole peruutusnappia.

$nano moi.txt:
M
O
O
I

$git add .
$nano moi.txt
M
O
heheee
O
I
$git add .

$git reset --hard:
HEAD is now at 712ad54 Make new txt file to test git diff

Hmm... Mitäköhän tapahtui. Se moi.txt tiedosto on kadonnut! Muut ovat vielä tallella. Eli viimeisin tietodata githubissani on duo MAke new txt file to test git diff

-------------------------------

f) Tee uusi salt-moduli. Voit asentaa ja konfiguroida minkä vain uuden ohjelman: demonin, työpöytäohjelman tai komentokehotteesta toimivan ohjelman. Käytä tarvittaessa ‘find -printf “%T+ %p\n”|sort’ löytääksesi uudet asetustiedostot. (Tietysti eri ohjelma kuin aiemmissa tehtävissä, tarkoitushan on harjoitella Salttia)

Tämä tehtävä aiheutti tuskia. Oikeasti. En millään keksinyt/löytänyt hyvää ohjelmaa, josta tekisin Salt-modulin muokatuin konfiguraatioin. Lopulta sain (kahden kytemispäivän jälkeen) valittua hyvän ohjelman, jolle loin modulin. Sitä ennen kokeilin muutamaa ohjelmaa: whowatch, acct, TigerVNCe, logwatch. (Muistiinpanoistani löytyy myös monta kirosanaa, mutta en osaa nyt tarkkaan sanoa, mikä sai ne purkautumaan ulos minusta. Ehkä ohjelmien konfigurointi oli vaikeata, en löytänyt conf-tiedostoja, niiden säätäminen olisi liian hankalaa). Onneksi sain lopulta keksittyä hyvän ohjelman: xubuntu desktopin.

Aloitin lauantai aamuna klo 9.28 tekemään tehtävää uudestaan. Olin kaikkeen edelliseen käyttänyt n. 2,5 tuntia.

Asensin xubuntu-desktopin ensiksi master-koneelle $sudo apt-get install xubuntu-desktop. Tässä meni aika kauan. Asennus alkoi 9.29 ja päättyi 9.38. State.apply-ajossa menee varmaan yhtä kauan.

Sitten jotakin simppeliä asetusta säätämään. Menen tutkimaan conf-tiedostoja (joita löysin muutaman). Valitsin seuraavan: /etc/xdg/xd-xubuntu/menus/xfce-applications.menu. Sieltä muuttamaan vaikka sanan Game-> Pelit. En nyt keksinyt parempaa.

Sitten /srv/salt/ kansioon tekemään desktop.sls tiedoston (kts Kuva 3 aiemmasta linkistä). Siitä näkyy moduli. Seuraavaksi takaisin sinne, missä conf-tiedosto on. $sudo cp xfce-applications.menu desktop_config. $sudo mv desktop_config /srv/salt.

Sitten sudo salt '*' state.apply desktop. Laitoin sen päälle klo 9.54. Ajo loppui 9.04. Desktop asentui orjalle, mutta punaista tuli: ID: /etc/xdg/xdg-xubuntu/menus
    Function: file.managed
      Result: False
     Comment: Specified target /etc/xdg/xdg-xubuntu/menus is a directory
     Started: 07:03:50.413972
    Duration: 7.834 ms
     Changes:

Kävin muuttamassa sen pelkäksi /menu sinne .sls tiedostoon. Uudestaan state.applyta. Tuli taas samasta kohdasta punaista: ID: menus
    Function: file.managed
      Result: False
     Comment: Specified file menus is not an absolute path
     Started: 07:06:22.059744
    Duration: 3.735 ms
     Changes:

Nyt tajusin, mikä oli virhe. Siinä lopussa pitää olla sen itse tekstitiedoston nimi. Eli lopullinen desktop.sls (kts kuva 4 aiemmasta linkistä). Taas state.applyta. Nyt ajo onnistui vihreällä. 
ID: /etc/xdg/xdg-xubuntu/menus/xfce-applications.menu
    Function: file.managed
      Result: True
     Comment: File /etc/xdg/xdg-xubuntu/menus/xfce-applications.menu updated
     Started: 07:09:09.532353
    Duration: 32.502 ms
     Changes:   
              ----------
              diff:
                  ---
                  +++
                  @@ -78,7 +78,7 @@
                       </Menu>
                       <Menu>
                  -        <Name>Games</Name>
                  +        <Name>Pelit</Name>
                           <Directory>xfce-games.directory</Directory>
                           <Include>
                               <Category>Game</Category>


Lopuksi vielä tarkistus: menen orjakoneella paikallisesti katsomaan sitä tiedostoa. Siellä lukee sana Pelit eikä Games. En sitten tiedä, miltä graaffinen käyttöliittyymä näyttäisi. Ehkä jos jaksan kokeilen ottaa remote desktop yhteyden ja käydä katsomassa.
