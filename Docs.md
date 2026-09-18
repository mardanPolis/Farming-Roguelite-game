# Produkta plānošanas dokumentācija
# *Harvest & Survive* — Farming RogueLite spēle

---

## 2.1. Ievads

### Situācija pirms produkta izveides

Mūsdienu spēļu tirgū Roguelite žanrs ir kļuvis par vienu no populārākajiem indie spēļu virziem, pateicoties tā augstajai atkārtojamībai un procesuālajai paaudzes mehānikai. Paralēli tam lauksaimniecības simulatori (piemēram, *Stardew Valley*, *Sun Haven*) piesaista miljoniem spēlētāju ar savu nomierinošo, ritmisko gameplay. Tomēr šo divu žanru kombinācija — kur lauksaimniecības dienas ritms tieši ietekmē nakts cīņas spēju — tirgū pastāv tikai daļēji vai ar būtiskiem kompromisiem vienā no pusēm.

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
| **Izstrādes mērķis** | Izveidot atkārtojamu, stratēģiski dziļu spēli, kurā lauksaimniecības dienas fāze un nakts wave aizsardzības fāze veido vienotu, savstarpēji atkarīgu gameplay cilpu |
| **Pamata uzdevumi** | Implementēt procedurālu kartes paaudzi, lauksaimniecības mehāniku ar kultūru vairāk nekā 20 veidiem, wave-based ienaidnieku sistēmu, un Roguelite napildinājumu/zaudēšanas progresiju |
| **Mērķauditorija** | PC spēlētāji vecumā 16–35 gadi, kuri bauda indie spēles, Roguelite žanru (*Hades*, *Dead Cells*) un/vai lauksaimniecības simulatorus (*Stardew Valley*) |

### Realizācijai nepieciešamie elementi

- **Spēles dzinējs:** Luminix(Paša veidots)
- **Grafikas apakšsistēma:** 2D pikseļu grafikas renderēšanas modulis
- **Procedurālās paaudzes sistēma:** Kartes un ienaidnieku spawn ģenerēšana
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

#### Galvenā funkcionalitāte: Dienas fāze (Farming)

**Ievaddati:** Spēlētāja ievade (kursors, poga), resursu inventārs, kartes stāvoklis, Roguelite buff saraksts

**Apstrāde:**
- Sistēma pārbauda atlasītā laukuma pieejamību
- Aprēķina kultūras augšanas laiku pēc laika modifikatoru buffiem
- Atjauno resursu inventāru pēc katras darbības

**Rezultāts:** Atjaunots kartes vizuālais stāvoklis, resursu daudzuma izmaiņas, laika skaits (cik dienas līdz ražai)

---

#### Galvenā funkcionalitāte: Nakts fāze (Wave Combat)

**Ievaddati:** Spēlētāja novietoto aizstāvju konfigurācija, ienaidnieku viļņa parametri (skaits, tips, ātrums), spēlētāja statistika

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

**Izvēlētā valoda: GDScript (primārā) + C# (veiktspējas kritiskajām daļām)**

GDScript tiek izvēlēts kā primārā valoda, jo tā ir natīvi integrēta Godot dzinējā, nodrošina ātrāku izstrādi un ir optimizēta spēles loģikas rakstīšanai. Atšķirībā no vispārīgajām valodām, GDScript ir paredzēta tieši spēļu izstrādei — tai ir iebūvēti signālu/notikumu mehānismi, tween animācijas un scēnas sistēma.

**Izvēlētā tehnoloģija: Godot 4.x**

Godot 4 tiek izvēlēts kā galvenais dzinējs, jo tas piedāvā pilnīgi bezmaksas licenci (MIT) bez royalty maksājumiem, iebūvētu 2D fiziku un renderēšanu, un aktīvu open-source kopienu. Atšķirībā no Unity, Godot neprasa abonēšanas maksu un neuzliek ierobežojumus pēc ieņēmumu sliekšņa — tas ir būtiski indie izstrādātājam.

**Papildu rīki:**
- **Aseprite** — pikseļu grafikas zīmēšana un animācija
- **FMOD / Godot AudioStreamPlayer** — adaptīvā audio sistēma
- **Git + GitHub** — versiju kontrole un sadarbība

---

## 2.5. Sistēmas modelēšana un projektēšana

### 2.5.1. Sistēmas struktūras modelis

#### Produkta struktūra

```
Harvest & Survive
├── Core Systems
│   ├── GameManager (run stāvoklis, fāzu pārvaldība)
│   ├── SaveSystem (saglabāšana/ielāde, meta-progresija)
│   └── EventBus (notikumu sistēma starp komponentiem)
├── Day Phase (Lauksaimniecība)
│   ├── FarmGrid (laukumu karte, tile pārvaldība)
│   ├── CropSystem (kultūru augšana, ražas novākšana)
│   ├── ResourceManager (resursu inventārs)
│   └── TimeManager (dienas laika skaitītājs)
├── Night Phase (Wave Combat)
│   ├── WaveManager (viļņu ģenerēšana, sarežģītība)
│   ├── EnemySpawner (ienaidnieku spawn punkti)
│   ├── DefenseSystem (aizstāvju izvietošana, torņi)
│   └── CombatResolver (kaitējuma aprēķini)
├── Roguelite Layer
│   ├── BuffSystem (buff pool, sinerģijas)
│   ├── MetaProgression (pastāvīgie atbloķējumi)
│   └── RunGenerator (procedurāla karte, sākuma parametri)
└── UI Layer
    ├── HUD (resursi, laiks, vilnis)
    ├── BuffSelectionScreen
    └── MainMenu / RunSummary
```

#### ER diagramma (galvenās entītijas)

```
[Run] ──< [DayState] >── [CropInstance]
  │                           │
  │                      [CropType]
  │
  ├──< [NightState] >── [EnemyWave]
  │                           │
  │                      [EnemyType]
  │
  └──< [BuffCollection] >── [Buff]
                                │
                           [BuffCategory]

[Player] ──< [MetaProgression] >── [UnlockRecord]
```

#### Datu vārdnīca

| Entītija | Atribūts | Tips | Apraksts |
|----------|---------|------|---------|
| Run | run_id | UUID | Unikāls run identifikators |
| Run | day_number | int | Pašreizējā diena (1–N) |
| Run | is_active | bool | Vai run ir aktīva |
| CropInstance | crop_type_id | FK | Kultūras tips |
| CropInstance | growth_stage | int (0–4) | Augšanas stadija |
| CropInstance | planted_day | int | Kad iestādīts |
| CropInstance | tile_x, tile_y | int | Pozīcija kartē |
| CropType | name | string | Kultūras nosaukums |
| CropType | grow_time | int | Dienu skaits līdz ražai |
| CropType | resource_yield | int | Ražas resursu daudzums |
| EnemyWave | wave_number | int | Viļņa numurs |
| EnemyWave | enemy_count | int | Ienaidnieku skaits |
| EnemyWave | difficulty | float | Sarežģītības koeficients |
| Buff | buff_id | UUID | Unikāls buff ID |
| Buff | category | enum | FARMING / COMBAT / UTILITY |
| Buff | effect_type | string | Efekta tips (speed, damage, yield…) |
| Buff | magnitude | float | Efekta spēks |
| MetaProgression | player_id | UUID | Spēlētāja ID |
| MetaProgression | total_runs | int | Kopējais run skaits |
| MetaProgression | unlocked_buffs | JSON | Atbloķēto buff ID saraksts |

#### Diagrammu kopums — galvenās struktūras

```
┌─────────────────────────────────────────┐
│              GAME SESSION               │
│                                         │
│  ┌──────────┐      ┌──────────────────┐ │
│  │  Player  │─────▶│  MetaProgression │ │
│  └──────────┘      └──────────────────┘ │
│       │                                 │
│       ▼                                 │
│  ┌──────────┐                           │
│  │   Run    │                           │
│  └────┬─────┘                           │
│       │                                 │
│  ┌────▼──────┐    ┌───────────────┐     │
│  │ DayPhase  │───▶│  NightPhase   │     │
│  └────┬──────┘    └───────┬───────┘     │
│       │                   │             │
│  ┌────▼──────┐    ┌───────▼───────┐     │
│  │ FarmGrid  │    │  WaveManager  │     │
│  └───────────┘    └───────────────┘     │
└─────────────────────────────────────────┘
```

#### Diagrammu kopums — papildu specifiskās struktūras

```
BUFF SYSTEM STRUKTŪRA:
┌─────────────────────┐
│     BuffPool        │
│  (30+ buffs)        │
└────────┬────────────┘
         │ procedurāla atlase
         ▼
┌─────────────────────┐     ┌──────────────────┐
│  BuffOffer (x3)     │────▶│  SynergyChecker  │
└─────────────────────┘     └──────────────────┘
         │ spēlētāja izvēle
         ▼
┌─────────────────────┐
│   ActiveBuffList    │
│   (uz spēlētāju)   │
└─────────────────────┘
         │ efektu piemērošana
    ┌────┴────┐
    ▼         ▼
[FarmMods] [CombatMods]
```

---

### 2.5.2. Funkcionālais un dinamiskais sistēmas modelis

#### Lietojuma gadījumu diagramma

```
                    ╔═══════════════════════════════════╗
                    ║        Harvest & Survive          ║
                    ║                                   ║
  ┌──────────┐      ║  [Sākt jaunu run]                 ║
  │          │──────╬─▶[Stādīt kultūras]                ║
  │ Spēlētājs│      ║  [Laistīt kultūras]               ║
  │          │──────╬─▶[Novākt ražu]                    ║
  │          │      ║  [Izvietot aizstāvjus]            ║
  │          │──────╬─▶[Izvēlēties buff]                ║
  │          │      ║  [Skatīt statistiku]              ║
  └──────────┘      ║  [Pielāgot iestatījumus]         ║
                    ╚═══════════════════════════════════╝
```

#### Secību diagramma — Dienas/Nakts fāzes pāreja

```
Spēlētājs    TimeManager    GameManager    WaveManager    UI
    │               │               │               │      │
    │               │──timerTick()──▶               │      │
    │               │               │               │      │
    │               │◀──dayEnd()────│               │      │
    │               │               │──prepareWave()▶      │
    │               │               │               │      │
    │               │               │◀──waveReady() │      │
    │               │               │──────────────────────▶showNightUI()
    │◀──────────────────────────────────────────────────────│
    │──placeDefenders()─────────────────────────────────────▶
    │               │               │               │      │
    │──startWave()──────────────────▶               │      │
    │               │               │──spawnWave()──▶      │
```

#### Stāvokļu diagramma — Run progresija

```
        ┌─────────────┐
        │  MAIN MENU  │
        └──────┬──────┘
               │ startRun()
               ▼
        ┌─────────────┐
   ┌───▶│  DAY PHASE  │◀──────────────┐
   │    └──────┬──────┘               │
   │           │ dayEnd()             │
   │           ▼                      │
   │    ┌─────────────┐               │
   │    │ NIGHT PHASE │               │
   │    └──────┬──────┘               │
   │           │                      │
   │    ┌──────┴──────┐               │
   │    │             │               │
   │    ▼             ▼               │
   │ [WAVE WIN]   [WAVE LOSE]         │
   │    │             │               │
   │    ▼             ▼               │
   │ [BUFF        [BASE               │
   │  SELECT]     DESTROYED]          │
   │    │             │               │
   └────┘         ┌───┘               │
                  │                   │
                  ▼                   │
           [RUN SUMMARY]              │
                  │ restartRun()      │
                  └───────────────────┘
```

#### Diagrammas atbilstība funkcionālajām prasībām

Visas iepriekš definētās funkcionālās prasības ir atspoguļotas diagrammās:

- **Dienas fāze (Farming)** → FarmGrid + CropSystem komponenti struktūras modelī, secību diagrammā redzama fāzes pāreja
- **Nakts fāze (Wave Combat)** → WaveManager + EnemySpawner, stāvokļu diagrammā NIGHT PHASE stāvoklis
- **Roguelite progresija** → MetaProgression entītija ER diagrammā, RUN SUMMARY + restartRun() stāvokļu diagrammā
- **Buff sistēma** → BuffPool struktūras modelis ar SynergyChecker, BUFF SELECT stāvoklis

---

*Dokuments sagatavots kā produkta plānošanas dokumentācija.*
*Projekts: Harvest & Survive | Versija: 0.1 — Koncepcijas stadija*
