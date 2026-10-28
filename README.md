# Waybar Minimal Dark Theme (Arch Linux / Hyprland)

Configurazione pulita, elegante e ultra-leggera per **Waybar**, studiata appositamente per **Arch Linux + Hyprland** su dispositivi come **Surface Pro 3**.

---

## Caratteristiche Principali

- **Consumo Risorse Minimo**: Nessuna animazione CSS pesante, nessun demone o script esterno in polling continuo. Tutti i moduli sono nativi in C++ di Waybar.
- **Estetica Dark Minimale**: Celle nere (`#0e0e0e`) con bordo grigio da 2px (`#3c3c3c`) e angoli smussati (`border-radius: 8px`).
- **Design Compatto**: Profilo ribassato (30px) e margini verticali ridotti per minimizzare lo spazio tra Waybar e le finestre.
- **Font**: Utilizza il font di sistema **JetBrains Mono**.
- **Layout delle sezioni**:
  - **In alto a sinistra (3 celle)**:
    1. Scritta statica `Arch Linux`
    2. Percentuale `RAM` in uso
    3. Percentuale `CPU` in uso
  - **In centro (1 cella)**:
    - 5 Workspace Hyprland fissi (1, 2, 3, 4, 5).
    - **Workspace corrente**: evidenziato con sfondo bianco pieno e testo nero.
    - **Workspace occupati**: colore azzurro/ciano distinto (`#61afef`).
    - **Workspace vuoti**: grigio scuro discreto (`#555555`).
  - **In alto a destra (3 celle)**:
    1. `BAT` (Percentuale batteria): configurato per `BAT1` (specifico per Surface Pro 3). Sotto il 10% (stato critico), il testo e il bordo da 2px diventano rossi (`#e06c75`) mantenendo lo sfondo nero. Mostra `⚡` e verde se in ricarica.
    2. `Ora` (`HH:MM`): passando con il cursore (hover), mostra un popup coordinato con data estesa e calendario mensile interattivo.
    3. `Wi-Fi` (4 barre di segnale progressive `▂▄▆█`): si riempiono in bianco in base alla qualità del segnale. In hover mostra SSID, segnale % e IP locale.

---

## Installazione e Aggiornamento

Copia la cartella nella configurazione utente:

```bash
cp -r waybar ~/.config/
```

Per riavviare Waybar e applicare le modifiche:

```bash
killall waybar && waybar &
```

---

## Risoluzione Problemi Comuni

### 1. Batteria non visibile o testo vuoto
La configurazione ora lascia a Waybar l'auto-rilevamento della batteria presente (di solito `BAT0` sui portatili standard, oppure `BAT1`).
Inoltre, sono stati gestiti esplicitamente tutti gli stati energetici del kernel Linux (`format-not-charging`, `format-full`, `format-charging`, `format-discharging`): in questo modo, quando il portatile è collegato alla corrente o raggiunge il 100%, l'etichetta non scompare mai e continua a mostrare la percentuale.
Se per qualsiasi motivo sul tuo hardware volessi forzare il dispositivo, controlla il nome con:
```bash
ls /sys/class/power_supply
```
E se necessario puoi aggiungere `"bat": "BAT0"` (o il nome visualizzato) dentro il blocco `"battery"` in `config.jsonc`.

### 2. Spazio vuoto eccessivo tra Waybar e il terminale / applicazioni
Questo spazio dipende principalmente da **Hyprland**, che di default applica dei margini esterni ampi (`gaps_out = 20`).
Per ridurre lo spazio e avvicinare le finestre alla barra:
1. Apri `~/.config/hypr/hyprland.conf`.
2. Trova la sezione `general` e modifica `gaps_out`:
```ini
general {
    gaps_in = 4
    gaps_out = 4    # <--- Riduci questo valore (es. a 4 o 2 per attaccarle alla barra)
    ...
}
```
Salva il file e Hyprland aggiornerà istantaneamente il layout senza riavviare.
