<div align="center">

# HackMyHome Voice Assistant

### Aura · Waveshare ESP32-S3 Touch LCD 1.85C

Un satellite vocale per **Home Assistant** basato su **ESPHome**, con interfaccia **LVGL**, personaggio animato Aura, microWakeWord locale, media player, timer, sveglia, controlli touch e radio integrate tramite **Music Assistant**.

[![ESPHome](https://img.shields.io/badge/ESPHome-2026.6.3%2B-03A9F4?style=for-the-badge&logo=esphome&logoColor=white)](#)
[![Home Assistant](https://img.shields.io/badge/Home%20Assistant-Voice%20Assistant-41BDF5?style=for-the-badge&logo=homeassistant&logoColor=white)](#)
[![Music Assistant](https://img.shields.io/badge/Music%20Assistant-Radio-7C3AED?style=for-the-badge)](#)
[![LVGL](https://img.shields.io/badge/UI-LVGL-22D3EE?style=for-the-badge)](#)
[![Board](https://img.shields.io/badge/Waveshare-ESP32--S3%201.85C-111827?style=for-the-badge)](#)
[![Project](https://img.shields.io/badge/HackMyHome-Aura-8B5CF6?style=for-the-badge)](#)

<a href="https://github.com/MarcoFre/images-aura/blob/main/aura_half_smile.png">
  <img src="https://raw.githubusercontent.com/MarcoFre/images-aura/main/aura_half_smile.png" alt="Aura con mezzo sorriso" width="280">
</a>

<em>Aura — frame “half smile”. Clicca sull’immagine per aprire l’asset originale.</em>

</div>

---

## 📦 Oggetto usato

| Voce | Dettaglio |
|---|---|
| **Prodotto** | Waveshare ESP32-S3 Touch LCD 1.85C / 1.85C-BOX |
| **Link Amazon** | [Waveshare ESP32-S3 Touch LCD 1.85C / 1.85C-BOX](https://amzn.to/4dHuK3w) |
| **Link Waveshare** | [Waveshare ESP32-S3 Touch LCD 1.85C / 1.85C-BOX](https://www.waveshare.com/esp32-s3-touch-lcd-1.85c.htm?sku=30684&aff_id=HackMyHome) |
| **Documentazione ufficiale** | [Waveshare Wiki](https://docs.waveshare.com/ESP32-S3-Touch-LCD-1.85C) |
| **Firmware base** | ESPHome |
| **Interfaccia grafica** | LVGL |
| **Integrazione domotica** | Home Assistant Voice Assistant |
| **Integrazione musicale** | Music Assistant |
| **Versione YAML** | `0.3.1-lvgl-music-assistant-radio-vu` |

> [!IMPORTANT]
> Questo firmware è pensato per la variante con display **ST77916 / JC3636W518V2**, touch **CST816T**, codec audio **ES8311** e microfoni tramite **ES7210**. Prima di compilare, verifica la revisione hardware della board.

---

## 🧭 Indice

- [Cosa fa questo progetto](#-cosa-fa-questo-progetto)
- [Caratteristiche principali](#-caratteristiche-principali)
- [Hardware supportato](#-hardware-supportato)
- [Pinout principale](#-pinout-principale)
- [Architettura firmware](#-architettura-firmware)
- [Aura e interfaccia LVGL](#-aura-e-interfaccia-lvgl)
- [Interfaccia touch](#-interfaccia-touch)
- [Voice Assistant](#-voice-assistant)
- [Music Assistant e radio](#-music-assistant-e-radio)
- [Modalità musica e VU meter](#-modalità-musica-e-vu-meter)
- [Timer e sveglia](#-timer-e-sveglia)
- [Rilevamento rumore e antifurto](#-rilevamento-rumore-e-antifurto)
- [Entità Home Assistant](#-entità-home-assistant)
- [Azioni API](#-azioni-api)
- [Installazione rapida](#-installazione-rapida)
- [Configurazione Music Assistant](#-configurazione-music-assistant)
- [Asset grafici Aura](#-asset-grafici-aura)
- [Troubleshooting](#-troubleshooting)
- [Struttura consigliata del repository](#-struttura-consigliata-del-repository)
- [Roadmap](#-roadmap)
- [Crediti](#-crediti)

---

## 🏠 Cosa fa questo progetto

Questo firmware trasforma la **Waveshare ESP32-S3 Touch LCD 1.85C** in un assistente vocale da scrivania per Home Assistant.

L’obiettivo non è soltanto far parlare la board, ma creare un piccolo oggetto interattivo in stile **HackMyHome**, con:

- personaggio Aura animato sul display;
- stati visivi dedicati alle fasi del Voice Assistant;
- wake word locale tramite microWakeWord;
- ascolto singolo o continuo;
- animazione della bocca sincronizzata con il TTS;
- timer e sveglia;
- controlli touch locali;
- media player integrato;
- modalità musica con pose Dance, note animate e VU meter;
- pagina radio collegata a Music Assistant;
- rilevamento del rumore per la modalità antifurto;
- download guidato degli asset grafici durante il boot.

---

## ✨ Caratteristiche principali

| Area | Funzione |
|---|---|
| 🎙️ **Voice Assistant** | Integrazione con Assist di Home Assistant |
| 🧠 **Wake word locale** | microWakeWord con modelli configurabili |
| 👩 **Aura** | Espressioni, blink, movimento occhi, sonno e bocca animata |
| 🔊 **Audio** | Speaker I2S con codec ES8311 e mixer media/annunci |
| 🎧 **Microfoni** | ES7210 via I2S per acquisizione audio |
| 🖥️ **Display** | Display rotondo 360×360 QSPI con UI LVGL |
| 👆 **Touch** | Swipe, pulsanti e slider volume locale |
| 📻 **Music Assistant** | Pagina radio con sei stazioni configurabili |
| 🎵 **Modalità musica** | Pose Dance, note animate e VU meter circolare RMS |
| ⏱️ **Timer** | Visualizzazione timer attivo e gestione timer scaduto |
| ⏰ **Sveglia** | Ora e azione configurabili da Home Assistant |
| 🛡️ **Antifurto** | Rilevamento del rumore sopra soglia |
| 🌙 **Sonno** | Aura si addormenta automaticamente durante la quiete |
| 📥 **Asset online** | Download di 16 immagini Aura con barra di avanzamento |
| 🔄 **OTA** | Aggiornamento firmware via ESPHome |
| 🧩 **API HA** | Azioni richiamabili da Home Assistant |

---

## 🔧 Hardware supportato

| Componente | Dettaglio |
|---|---|
| MCU | ESP32-S3 dual core, 240 MHz |
| Flash | 16 MB |
| PSRAM | 8 MB Octal PSRAM |
| Display | 1.85” rotondo, 360×360 |
| Driver display | ST77916 / JC3636W518V2 |
| Bus display | QSPI / Quad SPI |
| Touch | CST816T su I2C |
| Codec speaker | ES8311 |
| Codec microfoni | ES7210 |
| Amplificatore | PA control su GPIO15 |
| Expander I/O | PCA9554, indirizzo `0x20` |
| Connettività | Wi-Fi 2.4 GHz |

---

## 🧷 Pinout principale

### Display ST77916 QSPI

| Segnale | Pin |
|---|---|
| CLK | `GPIO40` |
| D0 | `GPIO46` |
| D1 | `GPIO45` |
| D2 | `GPIO42` |
| D3 | `GPIO41` |
| CS | `GPIO21` |
| Backlight | `GPIO5` |
| Reset LCD | `PCA9554` pin `1` |

### Touch CST816T

| Segnale | Pin / indirizzo |
|---|---|
| SDA | `GPIO11` |
| SCL | `GPIO10` |
| INT | `GPIO4` |
| Address | `0x15` |
| Reset touch | `PCA9554` pin `0` |

### Audio I2S

| Segnale | Pin |
|---|---|
| MCLK | `GPIO2` |
| BCLK | `GPIO48` |
| LRCLK | `GPIO38` |
| DOUT speaker | `GPIO47` |
| DIN microfono | `GPIO39` |
| PA CTRL | `GPIO15` |

---

## 🧱 Architettura firmware

```text
ESP32-S3
├─ Display ST77916 QSPI
│  └─ Interfaccia LVGL 360×360
├─ Touch CST816T
├─ Online Image
│  └─ 16 asset Aura scaricati da GitHub
├─ Audio Codec ES8311
├─ Microphone ADC ES7210
├─ Speaker Pipeline
│  ├─ Media pipeline
│  └─ Announcement / TTS pipeline
├─ Voice Assistant
│  ├─ microWakeWord
│  ├─ STT / TTS Home Assistant
│  ├─ timer
│  └─ stati assistente
├─ Music Assistant
│  └─ azioni Home Assistant per radio e stop
├─ Sound Level
│  ├─ RMS per VU meter
│  └─ Peak per rilevamento rumore
└─ Home Assistant API actions
```

### Fasi del Voice Assistant

Il display e la logica interna usano la variabile globale `voice_assistant_phase`.

| Valore | Stato | Significato |
|---:|---|---|
| `1` | Idle | Assistente pronto alla wake word |
| `2` | Waiting | Wake word rilevata, attesa comando |
| `3` | Listening | L’utente sta parlando |
| `4` | Thinking | Comando in elaborazione |
| `5` | Replying | Risposta TTS in corso |
| `10` | Not ready | Assistente non pronto |
| `11` | Error | Errore nella pipeline |

---

## 👩 Aura e interfaccia LVGL

Aura cambia aspetto in base allo stato del dispositivo.

| Stato | Comportamento visivo |
|---|---|
| Idle | Blink naturale ed espressioni casuali |
| Wake word | Aura si risveglia e attende il comando |
| Listening | Espressione dedicata all’ascolto |
| Thinking | Occhi rivolti verso l’alto |
| Replying | Bocca animata in funzione del livello TTS |
| Timer scaduto | Colori di allarme e stato dedicato |
| Musica | Pose Dance, note animate e VU meter |
| Sonno | Occhi chiusi, `Zzz...`, scena attenuata |
| Errore | Stato visivo e cromatico dedicato |

### Boot grafico

Durante l’avvio il display mostra:

1. attesa della connessione Wi-Fi;
2. attesa della connessione a Home Assistant;
3. download delle 16 immagini Aura;
4. barra di avanzamento dal rosso al verde;
5. passaggio automatico alla pagina principale quando tutto è pronto.

---

## 👆 Interfaccia touch

### Gesture principali

| Pagina | Gesture | Azione |
|---|---|---|
| Aura | Swipe verso l’alto | Apre la pagina controlli |
| Aura | Swipe verso destra | Apre la pagina radio Music Assistant |
| Radio | Swipe verso sinistra | Torna alla pagina Aura |
| Controlli | Swipe verso il basso | Torna alla pagina Aura |
| Qualsiasi pagina | Touch | Risveglia Aura e rinnova il timeout UI |

### Pagina controlli

```text
             CONTROLLI AURA

      VOLUME  [────────────]  50%

       LUMINOSITÀ       AUDIO ON

         AVVIA VA       ALLARME OFF

              TORNA AD AURA
```

| Controllo | Azione |
|---|---|
| Slider volume | Imposta il volume del media player |
| Luminosità | Cicla tra luminosità bassa, media e massima |
| Audio | Mute / unmute del media player |
| Avvia VA | Avvia o ferma il Voice Assistant |
| Allarme | Attiva o disattiva la modalità antifurto |
| Torna ad Aura | Chiude la pagina controlli |

La pagina controlli resta visibile per circa 15 secondi dall’ultima interazione. La pagina radio utilizza un timeout più lungo.

---

## 🎙️ Voice Assistant

Il firmware usa il componente `voice_assistant` di ESPHome con microfono I2S e media player speaker.

### Funzioni incluse

- avvio da wake word locale;
- modalità singola o continua;
- avvio e stop da touch o API;
- ducking dell’audio mentre l’assistente ascolta;
- eventi Home Assistant per testo STT e URI TTS;
- animazione della bocca durante la risposta;
- gestione timer e suono di fine timer;
- stop word temporanea per interrompere timer e annunci;
- ripartenza controllata di microWakeWord.

### Wake word configurate

| Modello | Uso |
|---|---|
| `okay_nabu` | Wake word principale |
| `kenobi` | Wake word alternativa |
| `hey_jarvis` | Wake word alternativa |
| `stop` | Modello interno per stop timer/annunci |

### Sensibilità wake word

Da Home Assistant è disponibile il selettore:

```text
WakeWord - Sensibilita
├─ Poco sensibile
├─ Medio
└─ Molto sensibile
```

### Comandi locali

Alcuni comandi vengono intercettati direttamente dal firmware.

| Intento | Frasi esempio |
|---|---|
| Volume su | “alza volume”, “aumenta volume” |
| Volume giù | “abbassa volume”, “riduci volume” |
| Modalità silenziosa | “modalità silenziosa” |
| Antifurto ON | “attiva antifurto”, “inserisci antifurto” |
| Antifurto OFF | “disattiva antifurto”, “disinserisci antifurto” |

---

## 📻 Music Assistant e radio

Uno swipe verso destra dalla pagina Aura apre una pagina LVGL dedicata alle radio.

La versione attuale contiene sei pulsanti statici:

1. Radio Number One;
2. Radio Deejay;
3. Radio Italia;
4. Radio Kiss Kiss;
5. R101;
6. Ambient Sleeping Pill.

Il tap su una radio richiama direttamente:

```yaml
action: music_assistant.play_media
```

Il firmware passa a Home Assistant:

- entità del player Music Assistant;
- URI della radio;
- tipo media `radio`;
- modalità coda `play`.

Dopo l’avvio riuscito, la UI torna automaticamente ad Aura e attiva la modalità musica.

### Perché la lista è statica

La lista è volutamente configurata nel file YAML per:

- ridurre l’uso di RAM;
- evitare il trasferimento dell’intera libreria Music Assistant;
- rendere la pagina immediata;
- evitare parsing JSON complesso sull’ESP32.

La roadmap prevede il caricamento dinamico dei preferiti tramite `music_assistant.get_library`.

---

## 🎵 Modalità musica e VU meter

Quando il media player entra nello stato `playing`, Aura attiva automaticamente la modalità musica:

- alterna tre pose Dance;
- evita la ripetizione consecutiva della stessa posa;
- esegue blink casuali;
- mostra sei note animate;
- muove leggermente il personaggio seguendo il livello audio;
- visualizza un VU meter circolare;
- nasconde temporaneamente orologio e timer.

### VU meter RMS

Il VU meter usa il valore `playback_rms`, non soltanto il picco.

```cpp
float normalized = (rms_db + 58.0f) / 57.0f;

if (normalized < 0.0f) normalized = 0.0f;
if (normalized > 1.0f) normalized = 1.0f;

real_level = powf(normalized, 1.55f);
```

Scala utilizzata:

| Livello RMS | VU meter |
|---:|---:|
| `-58 dB` o inferiore | `0%` |
| Valori intermedi | Curva progressiva |
| `-1 dB` o superiore | `100%` |

Lo smoothing applica un attacco rapido e un rilascio più lento:

```cpp
const float alpha =
  target > id(aura_music_level) ? 0.58f : 0.14f;
```

Le soglie colore sono:

- verde sotto il 70%;
- giallo dal 70%;
- arancione/rosso dal 90%.

---

## ⏱️ Timer e sveglia

### Timer Voice Assistant

Il firmware mantiene le informazioni del primo timer attivo:

- nome;
- durata totale;
- secondi rimanenti;
- stato attivo;
- aggiornamento periodico della UI.

Alla scadenza:

- viene riprodotto il suono configurato;
- viene abilitata temporaneamente la stop word;
- Aura mostra lo stato `TIMER SCADUTO`;
- il media viene sottoposto a ducking.

### Sveglia locale

Sono disponibili:

- ora sveglia in formato `HH:MM`;
- switch `Sveglia attiva`;
- scelta dell’azione;
- fuso orario POSIX configurabile tramite API.

Azioni disponibili:

| Opzione | Comportamento |
|---|---|
| Riproduci suono | Riproduce il suono locale |
| Invia evento | Invia un evento a Home Assistant |
| Suono ed evento | Esegue entrambe le azioni |

---

## 🛡️ Rilevamento rumore e antifurto

Il componente `sound_level` misura:

- `RMS`, usato dalla modalità musica;
- `Peak`, usato dal rilevamento del rumore.

La soglia è configurabile da Home Assistant tra `-75 dB` e `-25 dB`.

Per evitare falsi trigger, il rilevamento viene ignorato quando:

- Aura sta già riproducendo musica;
- è in corso un annuncio o TTS;
- il timer sta suonando;
- è già in corso un allarme.

Quando `Modalità antifurto` è attiva e viene superata la soglia, il firmware esegue lo script di allarme e aggiorna la UI.

> [!NOTE]
> Questa funzione è sperimentale e non sostituisce un sistema antifurto certificato.

---

## 🧩 Entità Home Assistant

<details>
<summary><strong>Select</strong></summary>

| Entità | Funzione |
|---|---|
| `Display - Emozione` | Forza l’espressione di Aura |
| `WakeWord - Sensibilita` | Regola la sensibilità di `okay_nabu` |
| `Livello log` | Cambia il livello log ESPHome |
| `Sveglia - Azione` | Sceglie cosa fare quando suona la sveglia |

</details>

<details>
<summary><strong>Switch</strong></summary>

| Entità | Funzione |
|---|---|
| `Modalità antifurto` | Attiva/disattiva antifurto acustico |
| `Assistente - Ascolto continuo` | Abilita la modalità conversazione continua |
| `Amplificatore` | Controlla PA / speaker amp |
| `Microfono disattivato` | Mute microfono e stop wake word |
| `Suono Mute-Unmute` | Abilita feedback sonoro mute |
| `Suono Wake Word` | Abilita il suono alla wake word |
| `Sveglia attiva` | Abilita la sveglia locale |
| `Controllo nuovo firmware` | Abilita il controllo versione remoto |

</details>

<details>
<summary><strong>Number</strong></summary>

| Entità | Range | Funzione |
|---|---:|---|
| `Soglia Rumore` | `-75` → `-25 dB` | Soglia antifurto / rilevamento rumore |
| `Mic-Guadagno` | `0` → `42` | Guadagno ES7210 |
| `VA-Guadagno` | `1` → `64` | Gain factor del microfono VA |
| `Sopp. Rumore` | `0` → `4` | Noise suppression Voice Assistant |

</details>

<details>
<summary><strong>Sensor / Binary Sensor / Text Sensor</strong></summary>

| Entità | Tipo | Funzione |
|---|---|---|
| `Prossimo timer` | sensor | Secondi rimanenti del primo timer attivo |
| `Prossimo timer - Nome` | text_sensor | Nome del timer attivo |
| `Ora sveglia` | text_sensor | Ora sveglia impostata |
| `Ora dispositivo` | text_sensor | Ora locale del dispositivo |
| `Rilevamento rumore` | binary_sensor | Rumore sopra la soglia configurata |

I sensori interni RMS e Peak non sono esposti normalmente nell’interfaccia Home Assistant.

</details>

<details>
<summary><strong>Light / Media Player</strong></summary>

| Entità | Funzione |
|---|---|
| `Display Backlight` | Controlla la retroilluminazione |
| Media player Aura | Riproduzione media e annunci TTS |

</details>

<details>
<summary><strong>Button</strong></summary>

| Entità | Funzione |
|---|---|
| `Test antifurto` | Simula il trigger antifurto |
| `Ripristino di fabbrica` | Factory reset interno/diagnostico |
| `Riavvia` | Riavvia ESP32 |
| `Controlla nuovo firmware` | Avvia il controllo versione remoto |

</details>

---

## 🔌 Azioni API

Il firmware espone alcune azioni richiamabili da Home Assistant.

| Azione | Parametri | Descrizione |
|---|---|---|
| `set_led_color` | `red`, `green`, `blue` | Aggiorna il colore logico usato dal firmware |
| `start_va` | — | Avvia il Voice Assistant |
| `stop_va` | — | Ferma il Voice Assistant |
| `set_alarm_time` | `alarm_time_hh_mm` | Imposta la sveglia in formato `HH:MM` |
| `set_time_zone` | `posix_time_zone` | Imposta il timezone POSIX |

Esempio:

```yaml
action: esphome.home_assistant_voice_speaker_02_start_va
```

> Il nome reale dell’azione dipende da `device_name` configurato nelle substitutions.

---

## 🚀 Installazione rapida

### Requisiti

- Home Assistant con ESPHome configurato;
- ESPHome **2026.6.3 o successivo**;
- pipeline Assist configurata in Home Assistant;
- Music Assistant configurato, per utilizzare la pagina radio;
- accesso a Internet durante il primo avvio, per scaricare gli asset Aura.

### Procedura

1. Crea un nuovo dispositivo in ESPHome.
2. Copia il file YAML del firmware.
3. Sostituisci credenziali e dati personali.
4. Configura il player e gli URI Music Assistant.
5. Valida il file YAML.
6. Compila con ESPHome.
7. Collega la board via USB-C.
8. Esegui il primo flash via USB.
9. Attendi il completamento del boot grafico e del download delle immagini.
10. Verifica in Home Assistant:
    - Wi-Fi connesso;
    - API connessa;
    - display acceso;
    - touch funzionante;
    - media player presente;
    - microfono e wake word funzionanti;
    - pagina radio operativa.

### Protezione delle credenziali

> [!CAUTION]
> Non pubblicare su GitHub password Wi-Fi, chiavi API, password OTA, indirizzi IP privati o altri segreti presenti nel file YAML.

Usa `secrets.yaml`:

```yaml
substitutions:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
  api_key: !secret aura_api_key
  ota_key: !secret aura_ota_password
```

Esempio di `secrets.yaml`:

```yaml
wifi_ssid: "NOME_RETE"
wifi_password: "PASSWORD_WIFI"
aura_api_key: "CHIAVE_API_BASE64"
aura_ota_password: "PASSWORD_OTA"
```

### Substitutions minime da personalizzare

```yaml
substitutions:
  device_name: home-assistant-voice-speaker-02
  friendly: "Speaker-04"
  fw_version: "0.3.1-lvgl-music-assistant-radio-vu"

  ip: "192.168.xxx.xxx"
  gateway: "192.168.xxx.xxx"
  subnet: "255.255.255.0"
  dns: "192.168.xxx.xxx"
```

È possibile rimuovere `manual_ip` dal blocco `wifi:` per utilizzare DHCP.

---

## ⚙️ Configurazione Music Assistant

### 1. Importa il player ESPHome

In Music Assistant apri:

```text
Settings → Player providers → Home Assistant Media Players
```

Abilita il media player ESPHome esposto da Aura. Music Assistant creerà una propria entità media player, per esempio:

```text
media_player.home_assistant_voice_speaker_02_media_player_2
```

Inserisci l’entità nella substitution:

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

Senza questa autorizzazione i pulsanti radio non possono richiamare `music_assistant.play_media`.

### 3. Recupera gli URI delle radio

In **Strumenti per sviluppatori → Azioni**, esegui:

```yaml
action: music_assistant.get_library
data:
  config_entry_id: ID_DELLA_TUA_ISTANZA_MA
  media_type: radio
  limit: 20
  offset: 0
  album_artists_only: false
  order_by: name
  search: Number
```

Esempio di risposta:

```yaml
items:
  - media_type: radio
    uri: library://radio/12
    name: Radio Number One
    favorite: true
```

### 4. Configura le radio nel file YAML

```yaml
substitutions:
  ma_radio_number_one_uri: "library://radio/12"
  ma_radio_deejay_uri:     "library://radio/6"
  ma_radio_italia_uri:     "library://radio/11"
  ma_radio_kiss_kiss_uri:  "library://radio/7"
  ma_radio_r101_uri:       "library://radio/1"
  ma_radio_ambient_uri:    "library://radio/10"
```

> [!WARNING]
> Gli identificativi `library://radio/...` appartengono alla singola libreria Music Assistant e possono essere diversi su ogni installazione.

### 5. Verifica la riproduzione

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

## 🖼️ Asset grafici Aura

Gli asset vengono scaricati dal repository:

[MarcoFre/images-aura](https://github.com/MarcoFre/images-aura)

La sequenza attuale contiene 16 immagini:

- idle;
- blink a metà;
- occhi chiusi;
- occhi a sinistra;
- occhi a destra;
- occhi in alto;
- viso in alto;
- viso in basso;
- mezzo sorriso;
- sorriso completo;
- bocca poco aperta;
- bocca aperta;
- bocca molto aperta;
- Dance 01;
- Dance 02;
- Dance 03.

Le immagini sono PNG 360×360 e vengono convertite in RGB565 dal componente `online_image`.

Il download è sequenziale per limitare i picchi di memoria. La barra di boot mostra lo stato di ogni passaggio.

Per usare un repository differente, modifica gli URL nella sezione:

```yaml
online_image:
```

---

## 🛠️ Troubleshooting

### Display nero

Controlla:

- backlight su `GPIO5`;
- reset display su `PCA9554` pin `1`;
- bus QSPI corretto;
- modello `JC3636W518V2`;
- PSRAM Octal attiva;
- `data_rate: 80MHz`, eventualmente prova temporaneamente `40MHz`;
- configurazione di rotazione e inversione colori.

### Touch non risponde

Controlla:

- indirizzo `0x15`;
- interrupt su `GPIO4`;
- reset touch su `PCA9554` pin `0`;
- I2C su `GPIO10/GPIO11`;
- `skip_probe: true`;
- orientamento e trasformazioni del touch.

### Audio assente

Controlla:

- ES8311 su `0x18`;
- ES7210 su `0x40`;
- `PA_CTRL` su `GPIO15`;
- modalità I2S primary/secondary;
- volume del media player;
- amplificatore abilitato;
- sample rate e clock condivisi.

### Wake word non riparte

Lo script di ripristino microWakeWord verifica che:

- API e Voice Assistant siano connessi;
- il microfono non sia disattivato;
- il timer non stia suonando;
- il Voice Assistant non sia già in esecuzione;
- non sia in corso una condizione che richiede lo stop temporaneo.

### I pulsanti radio restituiscono errore

Verifica che:

- Music Assistant sia online;
- Aura sia abilitata nel provider Home Assistant Media Players;
- `ma_player_entity` contenga l’entità Music Assistant, non quella ESPHome originale;
- il dispositivo ESPHome sia autorizzato a eseguire azioni Home Assistant;
- l’URI della radio esista nella tua libreria.

### La radio parte da Home Assistant ma non dal display

Controlla i log ESPHome. La pagina mostra anche uno stato sintetico:

- `Avvio ...`;
- `In riproduzione ...`;
- `Errore avvio ...`.

### Il boot resta sul download degli asset

Verifica:

- accesso a Internet;
- risoluzione DNS;
- raggiungibilità di `raw.githubusercontent.com`;
- data e ora corrette per TLS;
- disponibilità degli asset nel repository GitHub.

### Errori `no mem`

- mantieni la PSRAM in modalità Octal a 80 MHz;
- non aumentare contemporaneamente numero e dimensione degli asset;
- evita il download permanente di copertine radio dinamiche;
- non trasferire l’intera libreria Music Assistant all’ESP32;
- limita i buffer audio e grafici alle dimensioni realmente necessarie;
- usa una lista radio statica o risultati paginati.

### VU meter sempre a fondo scala

Verifica che il codice utilizzi:

- `playback_rms`;
- scala `-58 dB` → `-1 dB`;
- curva `powf(normalized, 1.55f)`;
- smoothing `0.58 / 0.14`.

---

## 📁 Struttura consigliata del repository

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

Aggiungi al `.gitignore`:

```gitignore
secrets.yaml
.esphome/
```

---

## 🗺️ Roadmap

- [ ] Caricamento dinamico delle radio preferite tramite `music_assistant.get_library`.
- [ ] Paginazione e ricerca sul display.
- [ ] Playlist e artisti preferiti.
- [ ] Schermata Now Playing con titolo e artista.
- [ ] Copertina del solo elemento in riproduzione.
- [ ] Gestione della coda Music Assistant.
- [ ] Selezione del player o del gruppo di stanze.
- [ ] Configurazione delle radio tramite entità Home Assistant.
- [ ] Modalità notte con luminosità adattiva.
- [ ] Pagina diagnostica hardware.
- [ ] Ottimizzazione ulteriore dei download degli asset.

---

## 🙌 Crediti

| Ruolo | Nome / progetto |
|---|---|
| Progetto e integrazione | HackMyHome / MarcoFre |
| Personaggio e asset grafici | Aura · [images-aura](https://github.com/MarcoFre/images-aura) |
| Verifica codice | Sanji78 |
| Codice voice speaker di riferimento | CaptainMustard |
| Componente ES8311 | [sw3Dan/waveshare-s2-audio_esphome_voice](https://github.com/sw3Dan/waveshare-s2-audio_esphome_voice) |
| Hardware | Waveshare ESP32-S3 Touch LCD 1.85C |
| Firmware | ESPHome |
| Domotica e Voice Assistant | Home Assistant |
| Gestione musicale | Music Assistant |
| Interfaccia grafica | LVGL |

---

## ⚠️ Disclaimer

Questo progetto è sperimentale e pensato per uso maker e domotico. Verifica sempre alimentazione, pinout, revisione hardware e configurazioni audio prima dell’uso continuativo.

La funzione di rilevamento rumore non sostituisce un impianto antifurto certificato.

Non pubblicare mai su GitHub password Wi-Fi, chiavi API, chiavi OTA o indirizzi IP privati reali.


