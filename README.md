
**Spēles Projekts**

Mūsdienu spēļu tirgū Roguelite žanrs ir kļuvis par vienu no populārākajiem indie spēļu virzieniem, pateicoties tā augstajai atkārtojamībai un procesuālās ģenerēšanas  mehānikai, piemēram, "Hades II", "Balatro". Paralēli tam lauksaimniecības simalatori, piemēram, "Star Valley", piesaista spēlētājus ar savu mierīgo un ritmisko spēles pieredzi. Tomēr šo divu žanru kombinācija, kur lauksaimniecība un roguelite kombinācija tirgū ir salīdzinoši maz izplatīta.

Tapēc iztrādāšu 2D spēli, kas apvieno abas šīs mehānikas vienotā spēles ciklā, lai spelētājs varētu izbaudīt gan lauksaimniecības žanru, gan roguelite žanru. Spēles izstrādes mērķis ir izveidot atkārtojamu un stratēģisku spēli, kas sadala abus žanrus divās fāzēs. Es sadaliju to dienas fāze - lauksaimniecība, un nakts fāze - roguelite. Lai es varētu realizētu šo projektu man vajadzētu izveidot spēlētāju tēlu, ko spēlētājs var kontrolēt, lauksaimniecību ar vairāk nekā desmit dažādiem augu veidiem, procedurālu mantu un ienaidnieku viļņu ģenerēšanu, kā arī izveidot Roguelite tipa progresijas sistēmu pēc spēles zaudēšanas.

Spēle ir domāta datoru spēlētājiem vecumā no 16 līdz 35 gadiem, kuri interesējas par indie spēlēm, Roguelite žanru, kā arī lauksaimniecības simulatoriem. Spēlē paredzēts apvienot lauksaimniecību, resursu pārvaldību, aizsardzības struktūru veidošanu un cīņu ar ienaidnieku viļņiem, lai katra spēles sesija būtu atšķirīga un prasītu stratēģisku lēmumu pieņemšanu. Procedurālā ģenerēšana nodrošinās atšķirīgus spēles apstākļus, mantas un ienaidnieku viļņus, savukārt Roguelite progresijas sistēma ļaus spēlētājam pēc zaudēšanas saglabāt noteiktus uzlabojumus un izmantot tos nākamajos spēles gājienos.

## Uzdevuma Formulējums

### Programmvienības
- Spēles dzinējs - Luminix (paša veidots).
- dienas/nakts fāžu maiņas kontrole
- uzvaras un zaudēšanas nosacījumu pārbaude
- spēles stāvokļu pārvaldība.

### Sistēmas elementi
- **Procedurālās ģenerēšanas:** mantu, veikalu un ienaidnieku viļņu ģenerēšana, ņemot vērā grūtības līmeni, run progresu un nejaušības sēklu (seed).
- **Lauksaimniecības:** vairāk nekā 10 augu veidu apstrāde. Sēšana, augšana pa stadijām, laistīšana, ražas novākšana un ražas izmantošana resursu iegūšanai.
- **Progresijas:** Roguelite meta-progresija pēc zaudēšanas, pastāvīgo uzlabojumu saglabāšana starp run.
- **Inventāra un resursu:** mantu, sēklu, ražas un resursu uzskaite un lietošana.
- **Ienaidnieku mākslīgā intelekta:** ienaidnieku uzvedība, ienaidnieku ceļa meklēšana (pathfinding), uzbrukuma loģika un dažādu ienaidnieku tipu atšķirības.

### Apakšsistēmas
- **Saglabāšanas/ielādes:** Roguelite run stāvokļa pārvaldība, kā arī pastāvīgās progresijas un iestatījumu saglabāšana.
- **Audio:** dienas/nakts atmosfēras skaņu un mūzikas atskaņošana, skaņas efektu apstrāde, skaļuma regulēšana pa kanāliem (mūzika, efekti).
- **Grafikas:** 2D sprite renderēšana, animācijas, apgaismojums/atmosfēras efekti dienas un nakts maiņai, izšķirtspējas un kadru ātruma iestatījumu piemērošana.
- **Lietotāja saskarnes (UI):** izvēlnes, HUD, inventāra un iestatījumu saskarnes, teksta fonta un izmēra regulēšana.
- **Ievades:** tastatūras un peles (iespējams, arī kontroliera) ievades apstrāde un vadības pārsaistīšana.

### Vides prasības produkta darbības nodrošināšanai

- **OS:** Windows 10/11, Linux (Ubuntu 20.04+)
- **CPU:** Intel Core i3 / AMD Ryzen 3 vai jaunāks
- **RAM:** min. 4 GB
- **GPU:** OpenGL 4.6 saderīga videokarte
- **Diska vieta:** ~500 MB
- **Papildues Programmatūra**: .NET 10 Desktop Runtim

### Pieejamības nodrošināšanas iespējas

- Grafiskie iestatijumi (Mainīt izšķirtspēja, vertikālā sinhronizācija, Kadri sekundē ierobežojums, tml. )
- Regulējams teksta fonts un izmērs UI elementos

# Prasību specifikācija
## Funkcionālās prasības
### Galvenā funkcionalitāte: Dienas fāze

**Ievaddati:** dienas numurs, kartes stāvoklis (visi stādījumi un to pašreizējā augšanas stadija), audzēto augu saraksts ar katra auga augšanas parametriem, iepriekšējā dienas pārdoto augu saraksts (veids un daudzums), augu pārdošanas cenas, spēlētāja nauda un resursu inventārs, aktīvo buff saraksts, veikala mantu kopa (pool), spēlētāja vadības ievade

**Apstrāde:**

- Dienas sākumā sistēma apstaigā katru iestādīto augu un atjaunina auga augšanas stadiju, ņemot vērā laistīšanu un augšanas modifikatoru buff efektus
- Apstrādā iepriekšējā periodā pārdotos augus un pieskaita spēlētājam iegūto naudas summu
- Procedurāli ģenerē veikala piedāvājumu, mantas, ko pārdod veikala īpašnieks, ņemot vērā dienas numuru un spēlētāja progresu
- Pārbauda atlasītā laukuma pieejamību sēšanai, laistīšanai un ražas novākšanai
- Atjauno resursu inventāru un kartes stāvokli pēc katras spēlētāja darbības
- Kad spēlētājs ieiet savā mājiņā, dienas fāze beidzas

**Rezultāts:** atjaunots kartes vizuālais stāvoklis, jaunās augu stadijas, atjaunota spēlētāja nauda, sagatavots veikala piedāvājums, resursu daudzuma izmaiņas, atlikušais laiks (dienu skaits līdz ražai), pāreja uz nakts fāzi

### Galvenā funkcionalitāte: Nakts fāze

**Ievaddati:** dienas numurs, sarežģītības līkne, nejaušības sēkla (seed), kartes stāvoklis ar visiem augiem, augu īpašības (darbības ilgums un efekts), spēlētāja novietoto aizstāvju konfigurācija, spēlētāja statistika (t. sk. dzīvības) un aktīvo buff saraksts, ienaidnieku tipu saraksts un ienaidnieku ieejas punkti, spēlētāja vadības ievade

**Apstrāde:**

- Nakts sākumā sistēma apstaigā katru augu un nosaka tā darbības laiku naktī, t. i., cik ilgi tas augs ir aktīvs
- Procedurāli ģenerē ienaidnieku vilni pēc dienas numura, sarežģītības līknes un nejaušības sēklas
- Aprēķina kaitējumu, dziedināšanu un efektus reāllaikā
- Pārbauda uzvaras/zaudējuma nosacījumu, t. i., vai spēlētājs izdzīvoja (spēlētāja dzīvības nav sasniegušas nulli)

**Rezultāts:** viļņa rezultāts (izdzīvoja/zaudēja), iegūtie resursi, statistika (nodarītais kaitējums, izdzīvošanas laiks), atjaunots spēlētāja un augu stāvoklis:(3)

### Papildfunkcionalitāte: Laika sistēma (Dienas/Nakts cikls)

**Ievaddati:** pašreizējā fāze (diena/nakts), spēlētāja pozīcija un mijiedarbība ar mājiņu, ienaidnieku viļņa stāvoklis (dzīvo ienaidnieku skaits), spēlētāja dzīvības, notikumu trigeri

**Apstrāde:**

- Dienas fāzē sistēma seko spēlētāja mijiedarbībai ar mājiņu un, tiklīdz spēlētājs tajā ieiet, sāk pāreju uz nakts fāzi
- Nakts fāzē sistēma seko dzīvo ienaidnieku skaitam un, tiklīdz visi ienaidnieki ir uzvarēti, sāk pāreju uz dienas fāzi
- Ja spēlētājs nomirst pirms viļņa uzvarēšanas, sistēma pārtrauc fāžu ciklu un nodod vadību Roguelite progresijas sistēmai
- Pārejas laikā aktivizē vai deaktivizē ienaidnieku parādīšanos (spawn) un palaiž dienas vai nakts sākuma apstrādi (augu stadiju atjaunināšana, viļņa ģenerēšana)

**Rezultāts:** fāzes pāreja ar animāciju, ienaidnieku parādīšanās, pārslēgta spēles fāze

### Galvenā funkcionalitāte: Roguelite progresija (Run sistēma)

**Ievaddati:** run stāvoklis, iegūtie punkti/resursi, spēlētāja nāve vai run pabeigšana.

**Apstrāde:**
- Saglabā meta-progresijas datus (pastāvīgie atbloķējumi)
- Atiestata run specifiskos datus (karte, inventārs, buff saraksts)
- Atbloķē jaunus sākuma bonusus nākamajam run

**Rezultāts:** Meta-progresijas atjaunošana, jaunās run sākuma opcijas, statistikas ekrāns

### Papildfunkcionalitāte: Buff/Upgrade izvēle

**Ievaddati:** Pabeigtā viļņa dati, spēlētāja pašreizējais stāvoklis

**Apstrāde:** Procedurāli atlasa 3 piedāvājumus no buff pool, ņemot vērā sinerģijas ar esošajiem buffiem

**Rezultāts:** Vizuālais izvēles ekrāns ar 3 buff opcijām, izvēlētā buff efekts tiek piemērots

### Prasību kopums

Sistēmai jānodrošina pilnvērtīga lauksaimniecības mehānika (sēšana, laistīšana, ražas novākšana), wave-based cīņas sistēma ar vismaz 5 ienaidnieku tipiem pirmajā versijā, un Roguelite progresijas cilpa ar ne mazāk kā 30 dažādiem buff/upgrade efektiem. Visām trim sistēmām jādarbojas kohezīvi — resursi no dienas fāzes tieši ietekmē nakts fāzes iesējas.

Spēlei jāietver procedurāla kartes ģenerēšana katrai jaunai run-ai, nodrošinot atšķirīgu lauksaimniecības laukumu izvietojumu, resursu pieejamību un ienaidnieku ieejas punktus. Vēl jāietver mini-boss encounters ik pēc 5 viļņiem un boss encounters katras run-as beigā

## Nefunkcionālās Prasības

### Darbības vides prasības (programmatūra/aparatūra)

- **Izstrāde:** Luminix (C#)
- **Mērķplatformas:** Windows 10/11 (x64), Linux (x64)
- **Min. aparatūra:** Intel i3-8100 / Ryzen 3 2200G, 4 GB RAM, 512 MB VRAM, 500 MB HDD
- **Rekomendētā:** Intel i5 / Ryzen 5, 8 GB RAM, 2 GB VRAM

### Drošība / datu aizsardzība / uzticamība

- Saglabāšanas faili tiek glabāti lokāli (ne mākonī bez spēlētāja piekrišanas)
- Saglabāšanas faili tiek validēti ar checksum, lai novērstu korupciju
- Avārijas gadījumā spēle auto-saglabā stāvokli ik pēc katras pabeigtas fāzes
- Nekādi personīgie dati netiek vākti bez eksplicītas piekrišanas

### Saskarne / dizains

- **Valoda:** Interfeiss angļu valodā
- **Responsivitāte:** Atbalsta 1280×720 līdz 3840×2160 rezolūciju ar UI skalēšanu
- **Dizaina stils:** Pikseļu grafika (16×16 tile), silta dienas krāsu palette, tumša/auksta nakts palette
- **UI:** Skaidrs HUD ar resursu skaitītājiem, laika joslu un minikarti

### Veiktspēja

- Mērķis: stabili 60 FPS uz rekomendētās aparatūras, min. 30 FPS uz minimālās
- Ielādes laiks: < 5 sekundes no izvēlnes līdz spēlei
- Nakts fāze ar līdz 31 vienlaicīgiem ienaidnieku objektiem bez FPS krituma zem 43
- Atmiņas patēriņš: < 2 GB RAM spēles laikā

### Prasību Kopums

Spēlei jānodrošina stabila un ātra darbība uz visām trim mērķplatformām (Windows, Linux) bez platformspecifiskām kļūdām. Saglabāšanas sistēmai jābūt uzticamai ar automātisku rezerves kopiju mehānismu. Spēlei jāatbalsta dažādas displeja konfigurācijas un jābūt pieejamā ar pielāgojamiem vadīklu iestatījum

Spēlei jābūt optimizētai ilgstošai spēlēšanas sesijai (2–4 stundas vienā run-ā) bez atmiņas noplūdēm. Audio sistēmai jānodrošina nemanāma pāreja starp dienas/nakts atmosfēras skaņu celiņiem. Roguelite saglabāšanas arhitektūrai jānodrošina, ka meta-progresija tiek saglabāta pat ja run sesija tiek pārtraukta

# Uzdevuma risināšanas līdzekļu apraksts un izvēles pamatojums

# Sistēmas modelēšana un projektēša

#
