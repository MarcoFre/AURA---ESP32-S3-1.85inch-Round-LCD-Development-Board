# Aura · ESP32-S3 Touch LCD 1.85C

![ESPHome](https://img.shields.io/badge/ESPHome-2026.6.3%2B-18BCF2?logo=esphome&logoColor=white)
![Home Assistant](https://img.shields.io/badge/Home%20Assistant-Voice%20Assistant-41BDF5?logo=homeassistant&logoColor=white)
![Music Assistant](https://img.shields.io/badge/Music%20Assistant-Radio-7C3AED)
![LVGL](https://img.shields.io/badge/UI-LVGL-22D3EE)
![Hardware](https://img.shields.io/badge/Hardware-Waveshare%20ESP32--S3%201.85C-F97316)

**Aura** trasforma il display circolare **Waveshare ESP32-S3 Touch LCD 1.85C** in un assistente vocale per Home Assistant con interfaccia LVGL animata, riproduzione audio locale e controllo delle radio di Music Assistant.

Il progetto utilizza il display QSPI ST77916 da 360×360 pixel, il touch CST816, i codec ES7210/ES8311 e gli 8 MB di PSRAM presenti sulla scheda.

> Versione YAML: `0.3.1-lvgl-music-assistant-radio-vu`

<p align="center">
  <a href="https://github.com/MarcoFre/images-aura/blob/main/aura_half_smile.png">
    <img src="https://raw.githubusercontent.com/MarcoFre/images-aura/main/aura_half_smile.png" alt="Aura con mezzo sorriso" width="280">
  </a>
</p>

<p align="center"><em>Aura — frame “half smile”. Clicca sull’immagine per aprire l’asset originale.</em></p>

---

## Funzioni principali

- Voice Assistant di Home Assistant con wake word locale.
- Animazioni di Aura per ascolto, elaborazione, risposta, errore e riposo.
- Movimento naturale degli occhi, blink e piccole espressioni casuali.
- Animazione della bocca sincronizzata con la voce riprodotta.
- Timer e sveglia con stato visualizzato sul display.
- Modalità musica con pose animate, note fluttuanti e VU meter circolare.
- VU meter basato sul livello **RMS**, calibrato tra `-58 dB` e `-1 dB`.
- Pagina LVGL dedicata alle radio di Music Assistant.
- Controlli touch per volume, mute, luminosità, Voice Assistant e allarme.
- Modalità sonno automatica dopo un periodo di quiete.
- Download guidato degli asset grafici con barra di avanzamento al boot.
- Aggiornamento OTA tramite ESPHome.

## Navigazione touch

| Pagina | Gesto o comando | Azione |
|---|---|---|
| Aura | Swipe verso destra | Apre le radio di Music Assistant |
| Aura | Swipe verso l’alto | Apre i controlli di Aura |
| Radio | Tap su una stazione | Avvia la radio selezionata |
| Radio | Swipe verso sinistra | Torna ad Aura |
| Controlli | Swipe verso il basso | Torna ad Aura |

Quando una radio parte, il display torna automaticamente alla pagina principale e Aura entra in modalità musica.

---

## Hardware supportato

Il file YAML è configurato per:

- Waveshare ESP32-S3 Touch LCD 1.85C;
- display circolare ST77916, QSPI, 360×360;
- touch capacitivo CST816;
- ESP32-S3 dual core a 240 MHz;
- 16 MB Flash;
- 8 MB Octal PSRAM;
- ADC audio ES7210;
- DAC audio ES8311;
- amplificatore integrato;
- microfoni e altoparlante collegati tramite I²S;
- expander I/O PCA/TCA9554.

Riferimenti hardware:

- [Pagina prodotto Waveshare](https://www.waveshare.com/esp32-s3-touch-lcd-1.85c.htm)
- [Documentazione Waveshare](https://docs.waveshare.com/ESP32-S3-Touch-LCD-1.85C)

---

## Requisiti software

- Home Assistant con ESPHome configurato;
- ESPHome **2026.6.3 o successivo**;
- integrazione Voice Assistant di Home Assistant;
- add-on o server Music Assistant collegato a Home Assistant;
- provider **Home Assistant Media Players** abilitato in Music Assistant;
- accesso a Internet durante il primo avvio per scaricare gli asset di Aura.

Il progetto usa inoltre il componente esterno ES8311 disponibile nel repository:

- [`sw3Dan/waveshare-s2-audio_esphome_voice`](https://github.com/sw3Dan/waveshare-s2-audio_esphome_voice)

Gli asset grafici vengono scaricati da:

- [`MarcoFre/images-aura`](https://github.com/MarcoFre/images-aura)

---

## Installazione

### 1. Copia il file YAML

Copia il file del progetto nella cartella ESPHome di Home Assistant, ad esempio:

```text
/config/esphome/aura-touch-lcd.yaml
```

### 2. Proteggi le credenziali

> [!CAUTION]
> Non pubblicare su GitHub password Wi-Fi, chiavi API, password OTA, indirizzi IP privati o altri segreti presenti nel file YAML.

Sostituisci i valori sensibili con riferimenti a `secrets.yaml`:

```yaml
substitutions:
  password: !secret wifi_password
  api_key: !secret aura_api_key
  ota_key: !secret aura_ota_password
  ssid: !secret wifi_ssid
```

E inserisci i valori reali esclusivamente in `/config/esphome/secrets.yaml`:

```yaml
wifi_ssid: "NOME_RETE"
wifi_password: "PASSWORD_WIFI"
aura_api_key: "CHIAVE_API_BASE64"
aura_ota_password: "PASSWORD_OTA"
```

`secrets.yaml` non deve essere caricato nel repository.

### 3. Configura rete e dispositivo

Aggiorna le sostituzioni iniziali del file:

```yaml
substitutions:
  device_name: aura-touch-lcd
  friendly: "Aura"

  ip: "192.168.1.50"
  gateway: "192.168.1.1"
  subnet: "255.255.255.0"
  dns: "192.168.1.1"
```

È possibile rimuovere `manual_ip` dal blocco `wifi:` per utilizzare il DHCP.

### 4. Compila e installa

Da ESPHome:

1. valida il file YAML;
2. esegui la prima installazione tramite USB;
3. attendi la connessione Wi-Fi e Home Assistant;
4. lascia completare il download dei 16 asset grafici.

Durante il primo avvio il display mostra l’avanzamento di:

1. connessione Wi-Fi;
2. connessione a Home Assistant;
3. download sequenziale delle immagini di Aura.

---

## Configurazione Music Assistant

### 1. Importa il player ESPHome

In Music Assistant apri:

```text
Settings → Player providers → Home Assistant Media Players
```

Abilita il media player ESPHome esposto da Aura. Music Assistant creerà una propria entità media player, per esempio:

```text
media_player.home_assistant_voice_speaker_02_media_player_2
```

Inserisci l’entità ottenuta nella sostituzione:

```yaml
substitutions:
  ma_player_entity: "media_player.NOME_DEL_PLAYER_MUSIC_ASSISTANT"
```

### 2. Consenti le azioni Home Assistant

In Home Assistant apri:

```text
Impostazioni → Dispositivi e servizi → ESPHome → Aura → Configura
```

Abilita l’opzione che consente al dispositivo ESPHome di eseguire azioni di Home Assistant.

Senza questa autorizzazione i pulsanti radio non potranno richiamare `music_assistant.play_media`.

### 3. Recupera gli URI delle radio

In **Strumenti per sviluppatori → Azioni**, esegui:

```yaml
action: music_assistant.get_library
data:
  config_entry_id: ID_DELLA_TUA_ISTANZA_MA
  media_type: radio
  limit: 20
  offset: 0
  order_by: name
  search: Number
```

La risposta contiene il nome e l’URI della radio:

```yaml
items:
  - media_type: radio
    uri: library://radio/12
    name: Radio Number One
    favorite: true
```

### 4. Configura le radio nel file YAML

Aggiorna le sostituzioni con gli URI della tua libreria:

```yaml
substitutions:
  ma_radio_number_one_uri: "library://radio/12"
  ma_radio_deejay_uri:     "library://radio/6"
  ma_radio_italia_uri:     "library://radio/11"
  ma_radio_kiss_kiss_uri:  "library://radio/7"
  ma_radio_r101_uri:       "library://radio/1"
  ma_radio_ambient_uri:    "library://radio/10"
```

Gli identificativi `library://radio/...` sono locali alla propria libreria Music Assistant e possono essere diversi da quelli dell’esempio.

### 5. Verifica la riproduzione

Prima di provare il touch, esegui questo test da Home Assistant:

```yaml
action: music_assistant.play_media
data:
  media_id: library://radio/12
  media_type: radio
  enqueue: play
target:
  entity_id: media_player.NOME_DEL_PLAYER_MUSIC_ASSISTANT
```

Per fermare la riproduzione:

```yaml
action: media_player.media_stop
target:
  entity_id: media_player.NOME_DEL_PLAYER_MUSIC_ASSISTANT
```

---

## Radio incluse nella pagina LVGL

La versione attuale mostra sei pulsanti statici:

1. Radio Number One;
2. Radio Deejay;
3. Radio Italia;
4. Radio Kiss Kiss;
5. R101;
6. Ambient Sleeping Pill.

La lista è volutamente statica per ridurre l’uso di memoria ed evitare di trasferire al microcontrollore l’intera libreria Music Assistant.

Per cambiare una radio occorre modificare:

- l’URI nelle `substitutions`;
- il testo del pulsante nella pagina `aura_radio_page`;
- il parametro `radio_name` associato al relativo `on_click`.

---

## Modalità musica e VU meter

Quando il media player entra nello stato `playing`, Aura attiva automaticamente la modalità musica:

- alterna tre pose Dance;
- esegue blink casuali;
- mostra sei note animate;
- muove leggermente l’immagine seguendo il livello audio;
- visualizza un VU meter circolare.

Il VU meter usa `playback_rms` anziché il solo valore di picco:

```cpp
float normalized = (rms_db + 58.0f) / 57.0f;
real_level = powf(normalized, 1.55f);
```

Lo smoothing utilizza un attacco rapido e un rilascio più lento:

```cpp
const float alpha =
  target > id(aura_music_level) ? 0.58f : 0.14f;
```

Le soglie colore sono:

- verde sotto il 70%;
- giallo dal 70%;
- arancione/rosso dal 90%.

---

## Wake word

La configurazione comprende:

- `Okay Nabu`;
- `Kenobi`;
- `Hey Jarvis`;
- modello interno `Stop` per interrompere la risposta.

Le opzioni di sensibilità, guadagno microfono, soppressione del rumore e ascolto continuo sono esposte a Home Assistant.

---

## Personalizzazione degli asset

Gli asset sono immagini PNG 360×360 convertite a RGB565 durante il download.

Per usare un repository differente, modifica gli URL nella sezione:

```yaml
online_image:
```

La sequenza corrente contiene 16 immagini:

- idle;
- blink metà e occhi chiusi;
- direzione degli occhi;
- viso alto e basso;
- sorriso;
- tre aperture della bocca;
- tre pose Dance.

Le immagini vengono caricate in sequenza per limitare i picchi di memoria durante il boot.

---

## Risoluzione dei problemi

### I pulsanti radio restituiscono un errore

Verifica che:

- Music Assistant sia online;
- il player Aura sia abilitato nel provider Home Assistant Media Players;
- `ma_player_entity` contenga l’entità Music Assistant, non quella ESPHome originale;
- il dispositivo ESPHome sia autorizzato a eseguire azioni Home Assistant;
- l’URI della radio esista nella tua libreria.

### La radio parte in Home Assistant ma non dal display

Controlla i log ESPHome. La pagina mostra anche uno stato sintetico:

- `Avvio ...`;
- `In riproduzione ...`;
- `Errore avvio ...`.

### Il boot resta sul download degli asset

Verifica:

- accesso a Internet;
- risoluzione DNS;
- raggiungibilità di `raw.githubusercontent.com`;
- data e ora corrette, necessarie per la verifica TLS.

### Errori di memoria

- mantieni `psram` in modalità Octal a 80 MHz;
- non aumentare contemporaneamente numero e dimensione degli asset;
- evita di scaricare copertine radio dinamiche senza una strategia di rilascio della memoria;
- mantieni la libreria Music Assistant lato Home Assistant e invia all’ESP32 solo i dati necessari.

### Display nero o colori invertiti

Il progetto forza `invert_colors` dopo il setup del display. Verifica di non aver modificato:

- modello MIPI/QSPI;
- pin del display;
- reset tramite expander;
- rotazione e inversione dei colori;
- configurazione della retroilluminazione.

---

## Struttura consigliata del repository

```text
.
├── README.md
├── aura-touch-lcd.yaml
├── secrets.example.yaml
├── LICENSE
└── docs/
    ├── aura-main.jpg
    ├── aura-radio.jpg
    └── hardware.jpg
```

Non inserire `secrets.yaml` nel repository. Aggiungilo al file `.gitignore`:

```gitignore
secrets.yaml
.esphome/
```

---

## Roadmap

- caricamento dinamico delle radio preferite tramite `music_assistant.get_library`;
- paginazione e ricerca sul display;
- playlist e artisti preferiti;
- schermata Now Playing con titolo e artista;
- copertina del solo elemento in riproduzione;
- gestione della coda Music Assistant;
- selezione del player o del gruppo di stanze;
- configurazione delle radio tramite entità Home Assistant anziché modifica del YAML.

---

## Crediti

Il progetto nasce dal lavoro e dalle sperimentazioni della community Home Assistant ed ESPHome.

Ringraziamenti a:

- **HackMyHome / MarcoFre** per il progetto Aura e gli asset grafici;
- **Sanji78** per la verifica del codice;
- **CaptainMustard** per il progetto di base del voice speaker Waveshare;
- **sw3Dan** per il componente ESPHome ES8311;
- i progetti **ESPHome**, **Home Assistant**, **Music Assistant** e **LVGL**;
- **Waveshare** per l’hardware ESP32-S3 Touch LCD 1.85C.

---

## Nota sullo stato del progetto

Il progetto è in sviluppo attivo. Prima di applicare aggiornamenti importanti conserva sempre una copia del file YAML funzionante e verifica le modifiche su un dispositivo di test.

