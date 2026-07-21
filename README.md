# ezamowienia-mcp

> Autonomiczny monitoring zamówień publicznych (BZP + TED) dla asystentów AI —
> konektor [Model Context Protocol](https://modelcontextprotocol.io).

![status: production](https://img.shields.io/badge/status-production-brightgreen)
![source: proprietary](https://img.shields.io/badge/source-proprietary-red)
![protocol: MCP](https://img.shields.io/badge/protocol-MCP-8A2BE2)
![built by App4You](https://img.shields.io/badge/built%20by-App4You-0A66C2)

---

## 🔒 Kod źródłowy prywatny

To repozytorium jest **wizytówką projektu**. Implementacja jest własnością
**App4You** i **nie jest publicznie dostępna**. Dostęp komercyjny, wdrożenie,
prezentacja na żywo oraz wgląd w kod są dostępne po ustaleniu warunków (NDA).

**Chcesz kupić dostęp lub zamówić wdrożenie?** Napisz na
[biuro@app4you.dev](mailto:biuro@app4you.dev) · [app4you.dev](https://app4you.dev)

---

## Co to jest

`ezamowienia-mcp` to serwer **Model Context Protocol**, który daje asystentowi
AI (np. Claude lub Codex) samodzielny dostęp do polskiego i unijnego rynku zamówień
publicznych. Zamiast ręcznie przeglądać portale, asystent codziennie pobiera
nowe ogłoszenia, ocenia ich dopasowanie do Twojej oferty i prowadzi trwały
rejestr decyzji — fundament pod w pełni autonomicznego agenta przetargowego.

## Co potrafi

- **Dwa źródła w jednym** — ogłoszenia krajowe z **Biuletynu Zamówień
  Publicznych** (e-Zamówienia) i progu unijnego z **TED** (Tenders Electronic
  Daily), przez oficjalne, bezpłatne API odczytu.
- **Ocena dopasowania przez AI** — filtrowanie po zarządzanym profilu słów
  kluczowych i kodów CPV, z podpowiedziami pod polską odmianę, tak by nie
  przeoczyć trafnych postępowań.
- **Współdzielony rejestr statusów** — przetarg odrzucony lub zakończony w
  jednej sesji nigdy nie wraca w kolejnej; statusy prowadzą deal przez cały
  cykl (`nowy → w toku → złożony → wezwanie → zarchiwizowany`, a przegrany,
  anulowany lub przedawniony trafia do `zakończonych`).
- **Pilnowanie wyników złożonych ofert** — rejestry nie zapowiadają daty
  rozstrzygnięcia, więc system sam wykrywa moment publikacji wyniku i
  raportuje zwycięzcę oraz rozstrzygnięcie (dopasowanie po identyfikatorze
  postępowania — dokładne, nie po tytule).
- **Monitoring zmian** — przed wyszukiwaniem nowych szans odświeża aktywne
  postępowania, porównuje terminy, wymagania i załączniki oraz nadaje zmianom
  priorytet `KRYTYCZNA`, `WAŻNA` albo `INFO`.
- **Pełna treść i dokumenty** — pobiera, zapisuje i analizuje publiczne
  załączniki z platform e-Zamówienia, OpenNexus/platformazakupowa.pl, ZETO oraz
  Marketplanet/eZamawiający. Obsługuje PDF, DOC, DOCX, RTF, ZIP i pliki tekstowe.
- **Podsumowania i różnice dokumentów** — zwraca krótkie podsumowanie oraz diff
  względem poprzedniej wersji; jawnie oznacza metadane jako świeże lub
  nieaktualne, jeśli platforma chwilowo nie odpowiada.
- **Obsługa wezwania** — przechowuje termin wezwania, URL platformy,
  identyfikator postępowania i liczbę dni do najbliższego operacyjnego terminu.
- **Filtr pilności** — skrót do postępowań z terminem składania w najbliższych
  dniach, gotowy pod rutynę harmonogramu.
- **Gotowy pod automatyzację** — działa jako lokalny konektor w Claude Desktop,
  Claude Code i Codex Desktop oraz jako uwierzytelniany serwer zdalny. Rutyna
  może monitorować i przygotowywać materiały do decyzji właściciela; narzędzie
  nie składa ofert, nie podpisuje dokumentów i niczego nie wysyła.

## Pod maską

| | |
|---|---|
| Język | TypeScript (ES modules), Node.js ≥ 20 |
| Protokół | Oficjalne SDK Model Context Protocol |
| Transporty | stdio (lokalnie) + Streamable HTTP (zdalnie, uwierzytelniany) |
| Walidacja | Zod — schematy wejścia dla każdego narzędzia |
| Jakość | 140 testów jednostkowych/integracyjnych, CI na Node 20, 22, 24 i 26 |
| Platformy dokumentów | e-Zamówienia, OpenNexus, ZETO, Marketplanet/eZamawiający |
| Bezpieczeństwo | bramka regulaminu API, ścisłe listy hostów i ścieżek, uwierzytelnianie stałoczasowe, sanityzacja zapytań, limity pobrań i archiwów |

## Zgodność i etyka integracji

Narzędzie korzysta z oficjalnych publicznych API odczytu BZP i TED oraz z
publicznych, nieuwierzytelnionych powierzchni odczytu platform wykonawczych do
listowania i pobierania dokumentów. Każdy adapter ma ścisłą listę dozwolonych
hostów i ścieżek; klient limituje tempo i rozmiar zapytań, nie omija kontroli
dostępu i respektuje warunki korzystania.

---

## O autorze

**App4You** — oprogramowanie na zamówienie: aplikacje mobilne, systemy webowe i
rozwiązania AI dla sektora publicznego i biznesu.

Zakup dostępu, licencja, integracja lub prezentacja:
[biuro@app4you.dev](mailto:biuro@app4you.dev) · [app4you.dev](https://app4you.dev)

---

<sub>© 2026 App4You. Wszelkie prawa zastrzeżone. Kod źródłowy stanowi własność
prywatną i nie jest objęty żadną licencją open source.</sub>
