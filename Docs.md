# Produkta plānošanas dokumentācija
#  Farming RogueLite spēle

---

## Ievads

### Situācija pirms produkta izveides

Mūsdienu spēļu tirgū Roguelite žanrs ir kļuvis par vienu no populārākajiem indie spēļu virzieniem, pateicoties tā augstajai atkārtojamībai un procesuālajai paaudzes mehānikai. Paralēli tam lauksaimniecības simulatori (piemēram, *Stardew Valley*, *Sun Haven*) piesaista miljoniem spēlētāju ar savu nomierinošo, ritmisko gameplay. Tomēr šo divu žanru kombinācija — kur lauksaimniecības dienas ritms tieši ietekmē nakts cīņas spēju — tirgū pastāv tikai daļēji vai ar būtiskiem kompromisiem vienā no pusēm.

### Produkta nepieciešamība

Trūkst spēles, kas **organiski apvieno** abas šīs mehānikas vienā kohezīvā gameplay cilpā: dienā tu audzē kultūras, izveido aizsardzības struktūras un gatavojies, bet naktī tu atvairī ienaidnieku viļņus, izmantojot tieši to, ko dienā uzcēli un uzaudzēji. Šāda mehāniskā saikne starp divām fāzēm rada unikālu spriedzi un stratēģisku dziļumu, kas pašreiz tirgū nav pilnvērtīgi aizpildīts.

### Produkta aktualitāte

Roguelite spēļu tirgus 2024.–2026. gadā turpina augt, ar spēlēm kā *Hades II*, *Balatro* un *Vampire Survivors* pierādot, ka indie Roguelite tituli var sasniegt masveida popularitāti. Lauksaimniecības spēļu popularitāte ar *Stardew Valley* pārsniegdama 30 miljonus pārdoto kopiju apliecina pastāvīgu pieprasījumu pēc šī žanra. Divu žanru hibrīds ar skaidru dienas/nakts ciklu ir aktuāls un tirgū pieprasīts risinājums.

---

## 2.2. Uzdevuma formulējums

| | |
|---|---|
| **Produkta nosaukums** | *-* |
| **Produkta veids** | 2D Roguelite spēle ar lauksaimniecības un tower-defense mehānikām |
| **Izstrādes mērķis** | Izveidot atkārtojamu, stratēģisku spēli, kurā lauksaimniecības dienas fāze un nakts wave aizsardzības fāze veido vienotu, savstarpēji atkarīgu gameplay cilpu |
| **Pamata uzdevumi** | Implementēt procedurālu mantu un ienaidnieku parādīšanos ģenerēšanu, lauksaimniecības mehāniku ar augiem vairāk nekā 10 veidiem, un Roguelite zaudēšanas progresiju |
| **Mērķauditorija** | PC spēlētāji vecumā 16–35 gadi, kuri bauda indie spēles, Roguelite žanru (*Hades*, *Dead Cells*) un/vai lauksaimniecības simulatorus (*Stardew Valley*) |

### Realizācijai nepieciešamie elementi

- **Spēles dzinējs:** Luminix (Paša veidots)
- **Procedurālās paaudzes sistēma:*mantuuun n ienaidnieku spawn ģenerēšana
- **Saglabāšanas/ielādes apakšsistēma:** Roguelite run stāvokļa pārvaldība
- **Audio apakšsistēma:** Dienas/nakts atmosfēras skaņu un mūzikas atskaņošana

### Vides prasības produkta darbības nodrošināšanai

- **OS:** Windows 10/11, Linux (Ubuntu 20.04+)
- **CPU:** Intel Core i3 / AMD Ryzen 3 vai jaunāks
- **RAM:** min. 4 GB
- **GPU:** OpenGL 4.6 saderīga videokarte
- **Diska vieta:** ~500 MB

### Pieejamības nodrošināšanas iespējas

- Pilnībā pielāgojamas vadīklas (pele + tastatūra)
- Regulējams teksta fonts un izmērs UI elementos

---

## 2.3. Prasību specifikācija

### 2.3.1. Sistēmas funkcionālās prasības

#### Galvenā funkcionalitāte: Dienas fāze

**Ievaddati:** Spēlētāja kontroļu ievade, kartes stāvoklis, resursu inventārs, buff saraksts

**Apstrāde:**
- Sistēma pārbauda atlasītā laukuma pieejamību
- Aprēķina augu augšanas laiku pēc laika modifikatoru buffiem
- Atjauno resursu inventāru pēc katras darbības

**Rezultāts:** Atjaunots kartes vizuālais stāvoklis, resursu daudzuma izmaiņas, laika skaits (cik dienas līdz ražai)

---

#### Galvenā funkcionalitāte: Nakts fāze

**Ievaddati:**  Spēlētāja kontroļu ievade, Spēlētāja novietoto aizstāvju konfigurācija, ienaidnieku viļņa parametri, spēlētāja statistika

**Apstrāde:**
- Procedurāli ģenerē ienaidnieku vilni pēc dienas numura un sarežģītības līknes
- Aprēķina kaitējumu, dziedināšanu un efektus reāllaikā
- Pārbauda win/lose kondīciju (bāze izdzīvoja / tika iznīcināta)

**Rezultāts:** Wave rezultāts (izdzīvoja/zaudēja), iegūtie resursi, statistika (nodarītais kaitējums, izdzīvošanas laiks)

---

#### Galvenā funkcionalitāte: Roguelite progresija (Run sistēma)

**Ievaddati:** Run stāvoklis, iegūtie punkti/resursi, izgāšanās vai uzvaras kondīcija

**Apstrāde:**
- Saglabā meta-progresijas datus (pastāvīgie atbloķējumi)
- Atiestata run-specifiskos datus (karte, inventārs, buff saraksts)
- Atbloķē jaunus sākuma bonusus nākamajai run-ai

**Rezultāts:** Meta-progresijas atjaunošana, jaunās run sākuma opcijas, statistikas ekrāns

---

#### Papildfunkcionalitāte: Buff/Upgrade izvēle

**Ievaddati:** Pabeigtā viļņa dati, spēlētāja pašreizējais stāvoklis

**Apstrāde:** Procedurāli atlasa 3 piedāvājumus no buff pool, ņemot vērā sinerģijas ar esošajiem buffiem

**Rezultāts:** Vizuālais izvēles ekrāns ar 3 buff opcijām, izvēlētā buff efekts tiek piemērots

---

#### Papildfunkcionalitāte: Dinamiskā laika sistēma (Dienas/Nakts cikls)

**Ievaddati:** Spēlētāja darbības ātrums, spēles laiks, notikuma trigeri

**Apstrāde:** Seko dienas laika skaitītājam, brīdina spēlētāju par tuvojošos nakti, automātiski pārslēdz fāzi

**Rezultāts:** Fāzes pāreja ar animāciju, ienaidnieku spawn aktivācija vai deaktivācija

---

#### Prasību kopums — galvenā funkcionalitāte

Sistēmai jānodrošina pilnvērtīga lauksaimniecības mehānika (sēšana, laistīšana, ražas novākšana), wave-based cīņas sistēma ar vismaz 5 ienaidnieku tipiem pirmajā versijā, un Roguelite progresijas cilpa ar ne mazāk kā 30 dažādiem buff/upgrade efektiem. Visām trim sistēmām jādarbojas kohezīvi — resursi no dienas fāzes tieši ietekmē nakts fāzes iespējas.

---

#### Prasību kopums — papildu funkcionalitāte

Spēlei jāietver procedurāla kartes ģenerēšana katrai jaunai run-ai, nodrošinot atšķirīgu lauksaimniecības laukumu izvietojumu, resursu pieejamību un ienaidnieku ieejas punktus. Vēl jāietver mini-boss encounters ik pēc 5 viļņiem un boss encounters katras run-as beigās.

---

### 2.3.2. Sistēmas nefunkcionālās prasības

#### Darbības vides prasības (programmatūra/aparatūra)

- **Izstrāde:** Luminix (C#)
- **Mērķplatformas:** Windows 10/11 (x64), Linux (x64)
- **Min. aparatūra:** Intel i3-8100 / Ryzen 3 2200G, 4 GB RAM, 512 MB VRAM, 500 MB HDD
- **Rekomendētā:** Intel i5 / Ryzen 5, 8 GB RAM, 2 GB VRAM
- ---

#### Drošība / datu aizsardzība / uzticamība

- Saglabāšanas faili tiek glabāti lokāli (ne mākonī bez spēlētāja piekrišanas)
- Saglabāšanas faili tiek validēti ar checksum, lai novērstu korupciju
- Avārijas gadījumā spēle auto-saglabā stāvokli ik pēc katras pabeigtas fāzes
- Nekādi personīgie dati netiek vākti bez eksplicītas piekrišanas
- ---

#### Saskarne / dizains

- **Valoda:** Interfeiss latviešu un angļu valodā (i18n arhitektūra papildu valodām)
- **Responsivitāte:** Atbalsta 1280×720 līdz 3840×2160 rezolūciju ar UI skalēšanu
- **Dizaina stils:** Pikseļu grafika (16×16 vai 32×32 tile), silta dienas krāsu palette, tumša/auksta nakts palette
- **UI:** Skaidrs HUD ar resursu skaitītājiem, laika joslu un minikarti


---

#### Veiktspēja

- Mērķis: stabili 60 FPS uz rekomendētās aparatūras, min. 30 FPS uz minimālās
- Ielādes laiks: < 5 sekundes no izvēlnes līdz spēlei
- Nakts fāze ar līdz 200 vienlaicīgiem ienaidnieku objektiem bez FPS krituma zem 45
- Atmiņas patēriņš: < 1 GB RAM spēles laikā


---

#### Galvenās nefunkcionālās prasības (kopums)

Spēlei jānodrošina stabila un ātra darbība uz visām trim mērķplatformām (Windows, Linux, macOS) bez platformspecifiskām kļūdām. Saglabāšanas sistēmai jābūt uzticamai ar automātisku rezerves kopiju mehānismu. Spēlei jāatbalsta dažādas displeja konfigurācijas un jābūt pieejamā ar pielāgojamiem vadīklu iestatījumiem.


---

#### Papildu specifiskās nefunkcionālās prasības (kopums)

Spēlei jābūt optimizētai ilgstošai spēlēšanas sesijai (2–4 stundas vienā run-ā) bez atmiņas noplūdēm. Audio sistēmai jānodrošina nemanāma pāreja starp dienas/nakts atmosfēras skaņu celiņiem. Roguelite saglabāšanas arhitektūrai jānodrošina, ka meta-progresija tiek saglabāta pat ja run sesija tiek pārtraukta negaidīti.


## 2.4. Uzdevuma risināšanas līdzekļu apraksts un izvēles pamatojums

### 2.4.1. Iespējamo risinājuma līdzekļu un valodu apraksts

#### Programmēšanas valodas (alternatīvas)

| Valoda | Raksturojums | Piemērotība |
|--------|-------------|-------------|
| **GDScript** | Godot dzinējam specifiska, Python-līdzīga sintakse, ātrs prototipu izveides process | ✅ Augsta — tieši optimizēta Godot ekosistēmai |
| **C#** | Statiski tipizēta, plaša ekosistēma, darbojas gan Godot, gan Unity | ✅ Augsta — labāka veiktspēja lielajām sistēmām |
| **C++** | Maksimāla veiktspēja, zemākā līmeņa kontrole | ⚠️ Vidēja — pārmērīgi sarežģīta indie spēlei |

#### Tehnoloģijas/rīki (alternatīvas)

| Rīks | Raksturojums | Piemērotība |
|------|-------------|-------------|
| **Godot 4.x** | Atvērtā koda dzinējs, lielisks 2D atbalsts, bezmaksas, aktīva kopiena | ✅ Augsta — ideāls 2D indie spēlēm |
| **Unity 2022 LTS** | Industriāls standarts, plašs asset store, C# skriptēšana | ✅ Augsta — pierādīta platforma, laba dokumentācija |
| **Pygame (Python)** | Viegls ietvars 2D spēlēm, ātrs prototips | ⚠️ Zema — nepietiekama veiktspēja un rīku ekosistēma |

### 2.4.2. Izvēlēto risinājuma līdzekļu un valodu apraksts

**Izvēlētā valoda: C# (veiktspējas kritiskajām daļām)**

GDScript tiek izvēlēts kā primārā valoda, jo tā ir natīvi integrēta Godot dzinējā, nodrošina ātrāku izstrādi un ir optimizēta spēles loģikas rakstīšanai. Atšķirībā no vispārīgajām valodām, GDScript ir paredzēta tieši spēļu izstrādei — tai ir iebūvēti signālu/notikumu mehānismi, tween animācijas un scēnas sistēma.

**Izvēlētā tehnoloģija: Luminix (Personīgais Game Engine)**

Godot 4 tiek izvēlēts kā galvenais dzinējs, jo tas piedāvā pilnīgi bezmaksas licenci (MIT) bez royalty maksājumiem, iebūvētu 2D fiziku un renderēšanu, un aktīvu open-source kopienu. Atšķirībā no Unity, Godot neprasa abonēšanas maksu un neuzliek ierobežojumus pēc ieņēmumu sliekšņa — tas ir būtiski indie izstrādātājam.

**Papildu rīki:**
- **Aseprite** — pikseļu grafikas zīmēšana un animācija
- **FMOD / Godot AudioStreamPlayer** — adaptīvā audio sistēma
- **Git + GitHub** — versiju kontrole un sadarbība

---

## 2.5. Sistēmas modelēšana un projektēšana

#### 
