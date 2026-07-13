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
**App4You** i **nie jest publicznie dostępna**. Prezentacja na żywo oraz wgląd
w kod — na życzenie, po ustaleniu warunków (NDA).

**Kontakt:** [biuro@app4you.dev](mailto:biuro@app4you.dev) · [app4you.dev](https://app4you.dev)

---

## Co to jest

`ezamowienia-mcp` to serwer **Model Context Protocol**, który daje asystentowi
AI (np. Claude) samodzielny dostęp do polskiego i unijnego rynku zamówień
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
  cykl (`nowy → w toku → złożony → zakończony / odrzucony`).
- **Pilnowanie wyników złożonych ofert** — rejestry nie zapowiadają daty
  rozstrzygnięcia, więc system sam wykrywa moment publikacji wyniku i
  raportuje zwycięzcę oraz rozstrzygnięcie (dopasowanie po identyfikatorze
  postępowania — dokładne, nie po tytule).
- **Pełna treść i dokumenty** — dostęp do całej treści ogłoszenia i linków do
  dokumentów postępowania (SWZ, załączniki).
- **Filtr pilności** — skrót do postępowań z terminem składania w najbliższych
  dniach, gotowy pod rutynę harmonogramu.
- **Gotowy pod automatyzację** — działa jako konektor w Claude Code; jedna
  zaplanowana rutyna potrafi pobierać, oceniać i oznaczać deale bez nadzoru.

## Pod maską

| | |
|---|---|
| Język | TypeScript (ES modules), Node.js ≥ 20 |
| Protokół | Oficjalne SDK Model Context Protocol |
| Transporty | stdio (lokalnie) + Streamable HTTP (zdalnie, uwierzytelniany) |
| Walidacja | Zod — schematy wejścia dla każdego narzędzia |
| Jakość | 99 testów jednostkowych/integracyjnych, CI na Node 20 i 22 |
| Bezpieczeństwo | bramka regulaminu API, uwierzytelnianie stałoczasowe, sanityzacja zapytań, twarde limity zakresu |

## Zgodność i etyka integracji

Narzędzie korzysta **wyłącznie z oficjalnego, publicznego API odczytu** BZP
(bezpłatnego zgodnie z regulaminem UZP) oraz z oficjalnego API TED. Świadomie
**nie sięga** po nieudokumentowane, wewnętrzne interfejsy portalu — klient jest
„grzeczny": limituje tempo zapytań i respektuje warunki korzystania.

---

## O autorze

**App4You** — oprogramowanie na zamówienie: aplikacje mobilne, systemy webowe i
rozwiązania AI dla sektora publicznego i biznesu.

📧 [biuro@app4you.dev](mailto:biuro@app4you.dev) · 🌐 [app4you.dev](https://app4you.dev)

---

<sub>© 2026 App4You. Wszelkie prawa zastrzeżone. Kod źródłowy stanowi własność
prywatną i nie jest objęty żadną licencją open source.</sub>
