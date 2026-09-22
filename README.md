
# Spēles Projekts

Mūsdienu spēļu tirgū Roguelite žanrs ir kļuvis par vienu no populārākajiem indie spēļu virzieniem, pateicoties tā augstajai atkārtojamībai un procesuālās ģenerēšanas  mehānikai, piemēram, "Hades II", "Balatro". Paralēli tam lauksaimniecības simalatori, piemēram, "Star Valley", piesaista spēlētājus ar savu mierīgo un ritmisko spēles pieredzi. Tomēr šo divu žanru kombinācija, kur lauksaimniecība un roguelite kombinācija tirgū ir salīdzinoši maz izplatīta.

Tapēc iztrādāšu 2D spēli, kas apvieno abas šīs mehānikas vienotā spēles ciklā, lai spelētājs varētu izbaudīt gan lauksaimniecības žanru, gan roguelite žanru. Spēles izstrādes mērķis ir izveidot atkārtojamu un stratēģisku spēli, kas sadala abus žanrus divās fāzēs. Es sadaliju to dienas fāze - lauksaimniecība, un nakts fāze - roguelite. Lai es varētu realizētu šo projektu man vajadzētu izveidot spēlētāju tēlu, ko spēlētājs var kontrolēt, lauksaimniecību ar vairāk nekā desmit dažādiem augu veidiem, procedurālu mantu un ienaidnieku viļņu ģenerēšanu, kā arī izveidot Roguelite tipa progresijas sistēmu pēc spēles zaudēšanas.

Spēle ir domāta datoru spēlētājiem vecumā no 16 līdz 35 gadiem, kuri interesējas par indie spēlēm, Roguelite žanru, kā arī lauksaimniecības simulatoriem. Spēlē paredzēts apvienot lauksaimniecību, resursu pārvaldību, aizsardzības struktūru veidošanu un cīņu ar ienaidnieku viļņiem, lai katra spēles sesija būtu atšķirīga un prasītu stratēģisku lēmumu pieņemšanu. Procedurālā ģenerēšana nodrošinās atšķirīgus spēles apstākļus, mantas un ienaidnieku viļņus, savukārt Roguelite progresijas sistēma ļaus spēlētājam pēc zaudēšanas saglabāt noteiktus uzlabojumus un izmantot tos nākamajos spēles gājienos.

# Uzdevuma Formulējums

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
- **Papildues Programmatūra**: .NET 10 Desktop Runtime

### Pieejamības nodrošināšanas iespējas

- Grafiskie iestatijumi (Mainīt izšķirtspēja, vertikālā sinhronizācija, Kadri sekundē ierobežojums, tml. )
- Regulējams teksta fonts un izmērs UI elementos

# Prasību specifikācija
## Funkcionālās prasības
### Galvenā funkcionalitāte: Dienas fāze

**Ievaddati:** dienas numurs, kartes stāvoklis (visi stādījumi un to pašreizējā augšanas stadija), audzēto augu saraksts ar katra auga augšanas parametriem, iepriekšējā dienas pārdoto augu saraksts (veids un daudzums), augu pārdošanas cenas, spēlētāja nauda un resursu inventārs, veikala mantu kopa (pool), spēlētāja vadības ievade

**Apstrāde:**

- Dienas sākumā sistēma apstaigā katru iestādīto augu un atjaunina auga augšanas stadiju, ņemot vērā laistīšanu
- Apstrādā iepriekšējā periodā pārdotos augus un pieskaita spēlētājam iegūto naudas summu
- Procedurāli ģenerē veikala piedāvājumu, mantas, ko pārdod veikala īpašnieks, ņemot vērā dienas numuru un spēlētāja progresu
- Pārbauda atlasītā laukuma pieejamību sēšanai, laistīšanai un ražas novākšanai
- Atjauno resursu inventāru un kartes stāvokli pēc katras spēlētāja darbības
- Kad spēlētājs ieiet savā mājiņā, dienas fāze beidzas

**Rezultāts:** atjaunots kartes vizuālais stāvoklis, jaunās augu stadijas, atjaunota spēlētāja nauda, sagatavots veikala piedāvājums, resursu daudzuma izmaiņas, atlikušais laiks (dienu skaits līdz ražai), pāreja uz nakts fāzi

### Galvenā funkcionalitāte: Nakts fāze

**Ievaddati:** dienas numurs, sarežģītības līkne, nejaušības sēkla, kartes stāvoklis ar visiem augiem, augu īpašības, spēlētāja novietoto aizstāvju konfigurācija, spēlētāja statistika, ienaidnieku tipu saraksts un ienaidnieku ieejas punkti, spēlētāja vadības ievade

**Apstrāde:**

- Nakts sākumā sistēma apstaigā katru jauno augu un nosaka tās augšanas laiku.
- Procedurāli ģenerē ienaidnieku vilni pēc dienas numura, sarežģītības līknes un nejaušības sēklas
- Aprēķina kaitējumu, dziedināšanu un efektus reāllaikā
- Pārbauda uzvaras/zaudējuma nosacījumu, vai spēlētājs izdzīvoja vai neizdzīvoja nakti.

**Rezultāts:** fāzes rezultāts (izdzīvoja/zaudēja), iegūtie resursi, statistika (nodarītais kaitējums, izdzīvošanas laiks), atjaunots spēlētāja un augu stāvoklis

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
- Atiestata run specifiskos datus (karte, inventārs)
- Atbloķē jaunus sākuma bonusus nākamajam run

**Rezultāts:** Meta-progresijas atjaunošana, jaunās run sākuma opcijas, statistikas ekrāns

### Papildfunkcionalitāte: Mantu Veikals

**Ievaddati:** dienas numurs, spēlētāja progress, spēlētāja nauda un resursu inventārs, veikala mantu kopa, sinerģiju noteikumi, spēlētāja vadības ievade (mantas izvēle un pirkšanas apstiprinājums)

**Apstrāde:**
- Kad spēlētājs pieiet pie veikala īpašnieka, sistēma atver veikala saskarni ar dienas sākumā sagatavoto piedāvājumu
- No mantu kopas procedurāli atlasa piedāvājumu, ņemot vērā dienas numuru, spēlētāja progresu.
- Pārbauda, vai spēlētājam pietiek naudas un vietas inventārā izvēlētās mantas pirkšanai
- Atjaunina piedāvājumu, atzīmējot nopirktās mantas kā izpārdotas

**Rezultāts:** vizuāls veikala piedāvājums ar cenām, atjaunota spēlētāja nauda un inventārs, paziņojums, ja pirkums nav iespējams.

### Prasību kopums

Galvenās funkcionalitātes kopums: Sistēma nodrošina pilnvērtīgu lauksaimniecības mehāniku (sēšana, laistīšana, ražas novākšana), viļņu cīņas sistēmu ar vismaz pieciem ienaidnieku tipiem un Roguelite progresijas ciklu. Visas trīs sistēmas darbojas kopā: dienas fāzē iegūtie resursi tieši ietekmē nakts fāzes iespējas.

Papildu funkcionalitātes kopums: Sistēma nodrošina dienas un nakts cikla pārvaldību, kas automātiski pārslēdz fāzes, un mantu veikalu, kur spēlētājs par iegūto naudu iegādājas mantas un uzlabojumus. Procedurāla kartes ģenerēšana katrai jaunai spēles sesijai nodrošina atšķirīgu lauksaimniecības laukumu izvietojumu, resursu pieejamību un ienaidnieku ieejas punktus.

## Nefunkcionālās Prasības

### Darbības vides prasības (programmatūra/aparatūra)

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
- **Dizaina stils:** Pikseļu grafika (16×16 tile).
- **UI:** Skaidrs HUD ar resursu skaitītājiem, laika joslu un minikarti

### Veiktspēja

- Mērķis: stabili 60 FPS uz rekomendētās aparatūras, min. 30 FPS uz minimālās
- Ielādes laiks: < 5 sekundes no izvēlnes līdz spēlei
- Līdz 30 vienlaicīgiem ienaidnieku objektiem bez FPS krituma zem 20 FPS uz min. aparatūras.
- Atmiņas patēriņš: < 2 GB RAM spēles laikā

### Prasību Kopums

Spēlei jānodrošina stabila un ātra darbība uz divām mērķplatformām (Windows, Linux) bez platformspecifiskām kļūdām. Saglabāšanas sistēmai jābūt uzticamai ar automātisku rezerves kopiju mehānismu. Spēlei jāatbalsta dažādas displeja konfigurācijas.

Spēlei jābūt optimizētai ilgstošai spēlēšanas sesijai (2–4 stundas vienā spēles sesijā) bez atmiņas noplūdēm. Saglabāšanas arhitektūrai jānodrošina, ka meta-progresija tiek saglabāta pat ja spēles sesija tiek pārtraukta

# Uzdevuma risināšanas līdzekļu apraksts un izvēles pamatojums

## Valodu alternatīvas

### C++
Kompilējama, zema līmeņa valoda ar manuālu atmiņas pārvaldību. Tā ļauj precīzi kontrolēt resursu izmantošanu un ir plaši izmantota komerciālu spēļu dzinēju izstrādē (Unreal Engine, daudzi paštaisīti dzinēji). Tā varētu būt piemērota, jo tā nodrošina augstu veiktspēju, kas svarīga. Ir pieejamas grafikas bibliotēkas (SDL, SFML, OpenGL). Tomēr tā ir pietiekami sarežģīta.

### Java
Objektorientēta valoda, kas darbojas uz virtuālās mašīnas (JVM). Tai ir bagāta standarta bibliotēka, automātiska atmiņas pārvaldība un laba pārnesamība starp operētājsistēmām. Tā varētu būt piemērota, jo tās viens un tas pats kods darbojas gan Windows, gan Linux. Ir spēļu bibliotēkas (LibGDX, LWJGL), kas nodrošina 2D renderēšanu un ievadi, un tā ir plaši pazīstama valoda ar daudz mācību materiālu.

### Python
Interpretējama augsta līmeņa valoda ar vienkāršu sintaksi. Spēļu izstrādei izmanto bibliotēkas, piemēram, Pygame un Arcade. Tā varētu būt piemērota, jo tai ir ļoti ātra prototipēšana un lasāms kods, kas ir noderīgi procedurālās ģenerēšanas un spēles loģikas testēšanai. Tomēr zemāka izpildes ātruma dēļ tā mazāk piemērota reāllaika cīņām ar daudziem objektiem.

## Tehnoloģiju alternatīvas

### Unity
Plaši izmantots dzinējs ar vizuālo redaktoru, ko var izmantot 2D un 3D spēlēm. Skriptus raksta C# valodā. Tas ietver gatavu fiziku, animācijas sistēmu, ceļa meklēšanu un eksportu uz dažādām platformām.
Kāpēc piemērots: ievērojami paātrina izstrādi, jo lielākā daļa apakšsistēmu (grafika, audio, ievade) jau ir gatava, un ir liels resursu un moduļu klāsts.

### Godot
Atvērtā koda dzinējs ar vieglu redaktoru un labu 2D atbalstu. Skriptēšanai izmanto GDScript vai C#.
Kāpēc piemērots: ir īpaši piemērots 2D spēlēm, tā pikseļu grafikas atbalsts ir labs, tas ir bez maksas un darbojas Windows un Linux vidē.

### JetBrains Rider
Kompleksa, specializēta C# un .NET integrētā izstrādes vide (IDE) ar spēcīgiem koda refaktorēšanas, analīzes un atkļūdošanas rīkiem.
Kāpēc piemērots: nodrošina augstākā līmeņa C# koda analīzi un automatizāciju, kas palīdz izvairīties no kļūdām un paātrina koda rakstīšanu.

## Izvēlētā Valoda
### C#
izvēlējos valodu c#, jo tā apvieno pietiekamu veiktspēju ar ērtu, drošu izstrādi. Tā ir objektorientēta valoda ar automātisku atmiņas pārvaldību, stingru tipizēšanu un labu kļūdu atklāšanu kompilēšanas laikā. Spēles projekts sastāv no daudziem savstarpēji saistītiem moduļiem un objektorientēta pieeja ļauj tos strukturēt kā atsevišķas klases.

## Izvēlētās Tehnoloģijas
### Luminix
Es izvēlējos savu paša taisīto dzinēju, jo par to man ir pilna izpratne, par tā arhitektūru, kādas sistēmas tajā jau ir iestrādātas un kādu trūkst. Tas ievērojami atvieglo izstrādes procesu un ļauj efektīvāk plānot darbu. Papildus tam projekta izstrāde kalpo kā praktisks tests paša veidotā dzinēja funkcionalitātes un veiktspējas pārbaudei reālos apstākļos. Luminix nodrošina tieši šai spēlei nepieciešamo funkcionalitāti - 2D sprite renderēšanu, ievades apstrādi, audio atskaņošanu un lietotāja saskarnes pamatelementus. Atšķirībā no vispārīgajiem spēļu dzinējiem Unity vai Godot, tas satur tikai nepieciešamās funkcijas un nav pārslogots ar liekiem rīkiem (3D, sarežģīta fizika), nodrošinot mazāku resursu patēriņu un pilnīgu kontroli pār koda bāzi.

### VS Code
Es izvēlējos Visual Studio Code, jo tā ir pietiekami viegla, bezmaksas un ātra koda redaktora vide, kas darbojas gan Windows, gan Linux operētājsistēmās, atbilstot spēles mērķplatformām. Ar C# paplašinājumu tā nodrošina koda pabeigšanu, kļūdu izcelšanu, atkļūdošanu un Git integrāciju. Salīdzinājumā ar pilna izmēra IDE kā JetBrains Rider vai Visual Studio, VS Code ir resursu ziņā daudz vieglāka un ātrāk ielādējas.

# Sistēmas modelēšana un projektēša
Sistēma sastāv no diviem slāņiem dzinēja un spēles loģikas

### Dzinējs
Nodrošina entītiju, komponenšu glabāšanu. Nodrošina grafisko resursu, skaņas failu ielādi atmiņā un apstrādā lietotāja ievades signālus nodošanai spēles sistēmām, kā arī nodrošina renderēšanu un 2D fiziku.

### Spēles Loģika
Nodrošina dienas un nakts fāžu ciklu, spēlētāja vadību un ienaidnieku uzvedību, kā arī pārvalda resursu ieguvi, inventāru, veikala sistēmu un spēles progresa saglabāšanu.

## Datu Vārdnīca

| Lauks |  Tips  | Apraksts |
| :---- | :---- | :------- |
| GameState | string | Sistēmas kopējais stāvoklis: vai spēle atrodas izvēlnē, aktīvā spēles sesijā, pauzē vai sesijas beigu ekrānā |
| RunPhase  | string | Pašreizējā fāze aktīvas sesijas ietvaros: diena vai nakts |
| RunSeed   | int    | Nejaušības sēkla, kas tiek izmantota kartes, veikala un ienaidnieku viļņu procedurālajai ģenerēšanai konkrētajā sesijā |
| RunLevel  | int    | Cik tālu spēlētājs ticis pašreizējā sesijā; pieaug pēc katras veiksmīgi pārdzīvotas nakts |
| RunDiff   | int    | Spēlētāja izvēlētā sākotnējā grūtības pakāpe pirms sesijas sākuma; ietekmē ienaidnieku skaitu, dzīvības un uzbrukuma spēku visas sesijas garumā. |
| CurrDiff  | int    | Pašreizējā aprēķinātā grūtības pakāpe nakts fāzē; tiek aprēķināta no `RunDiff` un `RunLevel` un to izmanto ienaidnieku vilņa ģenerēšanai
| TotalRuns | int    | Kopējais pabeigto spēles sesiju skaits kopš spēles pirmās palaišanas |
| TopLevel  | int    | Labākais jebkad sasniegtais RunLevel starp visām spēles sesijām; izmanto statistikas rādīšanai un progresa izsekošanai |
| PlayerID  | EntityID | Atsauce uz spēlētāja entītiju dzinēja entītiju-komponenšu sistēmā |
| Settings  | struct | Saglabātie spēlētāja iestatījumi (izšķirtspēja, skaļums u.c.) |
