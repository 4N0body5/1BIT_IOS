\#!/usr/bin/bash


## Projekt 1 - Analyzátor logů z obchodování na burze

**Popis úlohy**

Cílem úlohy je vytvořit skript pro analýzu záznamu systému pro obchodování na burze. Skript bude filtrovat záznamy a poskytovat statistiky podle zadání úživatele.

**Zjednodušený úvod do problematiky**

Na burze se obchoduje s cennými papíry (např. akcie společností, dluhopisy), komoditami (např. ropa, zelí) apod. Každý obchodovaný artikl má jednoznačný identifikátor, tzv. ticker (např. akcie firmy Intel mají na burze NASDAQ ticker INTC, bitcoin může mít přiřazený ticker BTC). Cena artiklů se mění v čase. Obchodník na burze vstupuje do pozic, buď tak, že koupí artikl a očekává, že jeho cena poroste, aby jej pak prodal za vyšší cenu (tzv. dlouhá pozice), nebo že artikl prodá a očekává, že jeho cena klesne, aby jej poté mohl koupit levněji (tzv. krátká pozice). Obchodník může prodat i artikl, který právě nevlastní (v reálu to funguje tak, že si ho od někoho, kdo ho vlastní, “vypůjčí”, prodá jej, a potom ho koupí za nižší cenu a “vrátí”). V našem případě budeme uvažovat, že obchodníkův systém posílá na burzu příkazy k nákupu (buy) nebo prodeji (sell) určitého množství jednotek artiklu označeného nějakým tickerem.

### **Specifikace rozhraní skriptu**

**POUŽITÍ**

`tradelog [-h|--help] [FILTR] [PŘÍKAZ] [LOG [LOG2 [...]]`

**VOLBY**

_PŘÍKAZ_ může být jeden z:
* `list-tick` – výpis seznamu vyskytujících se burzovních symbolů, tzv. “tickerů”.
* `profit` – výpis celkového zisku z uzavřených pozic.
* `pos` – výpis hodnot aktuálně držených pozic seřazených sestupně dle hodnoty.
* `last-price` – výpis poslední známé ceny pro každý ticker.
* `hist-ord` – výpis histogramu počtu transakcí dle tickeru.
* `graph-pos` – výpis grafu hodnot držených pozic dle tickeru.

_FILTR_ může být kombinace následujících:
* `-a DATETIME` – after: jsou uvažovány pouze záznamy PO tomto datu (bez tohoto data). DATETIME je formátu YYYY-MM-DD HH:MM:SS.
* `-b DATETIME` – before: jsou uvažovány pouze záznamy PŘED tímto datem (bez tohoto data).
* `-t TICKER` – jsou uvažovány pouze záznamy odpovídající danému tickeru. Při více výskytech přepínače se bere množina všech uvedených tickerů.
* `-w WIDTH` – u výpisu grafů nastavuje jejich šířku, tedy délku nejdelšího řádku na WIDTH. Tedy, WIDTH musí být kladné celé číslo. Více výskytů přepínače je chybné spuštění.
* `-h` a `--help` vypíšou nápovědu s krátkým popisem každého příkazu a přepínače.

**FORMÁT LOGU**

`DATUM A CAS;TICKER;TYP TRANSAKCE;JEDNOTKOVA CENA;MENA;OBJEM;ID`
