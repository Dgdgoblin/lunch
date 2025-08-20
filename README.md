# Dagens lunch by PMO IT — statisk HTML

Detta repo genererar **`index.html`** med endast **dagens** luncher från:
- FEI — https://www.fei.se/meny-fei-restaurant-lounge
- Cirkeln — https://cirkelnstockholm.se/restauranger/restaurang-cirkeln/

Sidan är helt statisk och kan publiceras via GitHub Pages. Uppdatering sker automatiskt varje vardag via GitHub Actions.

## Snabbstart (GitHub Pages)
1. Skapa ett nytt GitHub-repo och ladda upp dessa filer.
2. Gå till **Settings → Pages** och välj att publicera från `main`-branchen, rotmappen (`/`). Spara.
3. Gå till **Actions** och aktivera workflows om GitHub ber om det.
4. Workflown körs varje vardag kl **06:30** Stockholmstid (cron 04:30 UTC sommartid). Du kan även starta manuellt via **Actions → Bygg lunch-sida → Run workflow**.
5. Din sida nås på: `https://<ditt-användarnamn>.github.io/<repo-namn>/`

> `index.html` har `<meta http-equiv="refresh" content="1800">` och laddas om var 30:e minut i webbläsaren.

## Lokalt (utan GitHub)
```bash
pip install -r requirements.txt
python build.py
# Öppna index.html i valfri webbläsare
```
Vill du uppdatera automatiskt lokalt: kör `python build.py` med cron (Linux/macOS) eller Schemalagda aktiviteter (Windows). Exempel cron (vardagar 06:30):
```
30 6 * * 1-5 /usr/bin/python3 /path/till/repo/build.py
```

## Lägg till fler restauranger
- Öppna `build.py`
- Lägg in URL i `RESTAURANTS`-dicten
- Implementera en `parse_xxx`-funktion eller återanvänd de befintliga beroende på sidans struktur.

## Felsökning
- Om sidan inte uppdateras, kontrollera senaste Actions-körning i GitHub → Actions.
- Om menyerna på källsidorna ändrat struktur kan parsern behöva justeras.
