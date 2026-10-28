# Waybar Minimal Dark Theme (Arch Linux / Hyprland)

Configurazione pulita, elegante e ultra-leggera per **Waybar**, studiata appositamente per **Arch Linux + Hyprland** su dispositivi come **Surface Pro 3**.

---

## Caratteristiche Principali

- **Consumo Risorse Minimo**: Nessuna animazione CSS pesante, nessun demone o script esterno in polling continuo. Tutti i moduli sono nativi in C++ di Waybar.
- **Estetica Dark Minimale**: Celle nere (`#0e0e0e`) con bordo grigio da 2px (`#3c3c3c`) e angoli smussati (`border-radius: 8px`).
- **Font**: Utilizza il font di sistema **JetBrains Mono**.
- **Layout delle sezioni**:
  - **In alto a sinistra (3 celle)**:
    1. Scritta statica `Arch Linux`
    2. Percentuale `RAM` in uso (aggiornata ogni 10s per non svegliare inutilmente la CPU)
    3. Percentuale `CPU` in uso (aggiornata ogni 3s)
  - **In centro (1 cella)**:
    - 5 Workspace Hyprland fissi (1, 2, 3, 4, 5).
    - **Workspace corrente**: evidenziato con sfondo bianco pieno e testo nero.
    - **Workspace occupati** (con finestre aperte ma non correnti): colore azzurro/ciano distinto (`#61afef`).
    - **Workspace vuoti**: grigio scuro discreto (`#555555`).
  - **In alto a destra (3 celle)**:
    1. `BAT` (Percentuale batteria): mantiene l'estetica nera; quando la batteria scende sotto il 10% (stato critico), il testo e il bordo da 2px diventano rossi (`#e06c75`) senza sfondi accecanti. Sottile indicatore verde quando in ricarica.
    2. `Ora` (`HH:MM`): passando con il cursore (hover), mostra un popup coordinato con data estesa e calendario mensile interattivo.
    3. `Wi-Fi` (4 barre di segnale progressive `▂▄▆█`): si riempiono in bianco in base alla qualità del segnale e restano grigie per i livelli non raggiunti. Passando sopra con il cursore viene mostrato il nome della rete (`SSID`), potenza in % e IP locale.

---

## Installazione sul portatile

Quando scarichi la cartella sul tuo Surface Pro 3, copiala direttamente dentro `~/.config/waybar`:

```bash
# Copia la cartella nella configurazione utente
cp -r waybar ~/.config/
```

Assicurati che i file siano posizionati in:
- `~/.config/waybar/config.jsonc`
- `~/.config/waybar/style.css`

---

## Avvio ed Esecuzione con Hyprland

Per avviare automaticamente Waybar all'accesso in Hyprland, aggiungi questa riga nel tuo `~/.config/hypr/hyprland.conf`:

```ini
exec-once = waybar
```

Per ricaricare Waybar dopo aver modificato i file senza riavviare la sessione:

```bash
killall waybar && waybar &
```

---

## Dipendenze e Requisiti

- **Nessuna applicazione esterna aggiuntiva richiesta**: non servono script python, playerctl, nm-applet o pacchetti pesanti.
- **Font di sistema**: Il pacchetto standard di JetBrains Mono su Arch:
  ```bash
  sudo pacman -S ttf-jetbrains-mono
  ```
  *(Se lo usi già come font di sistema, sei già a posto senza dover installare nulla!)*

