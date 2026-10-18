# Mr. Robot 🤖

**[ ENG ](./README.md)** | **[ RUS ](./README.ru.md)** | **[ PL ](./README.pl.md)**

> **Działający prototyp do pracy z plikami magazynowymi** — jeden plik HTML, który przyspiesza rutynowe zadania bardziej niż makra w Excelu i ręczne kopiuj-wklej.

To nie jest skończony produkt, ale nie jest to też makieta. Wszystko, co tu opisano, działa i możesz sprawdzić to od razu w przeglądarce. Projekt jest udostępniony, żeby inni, którzy budują podobne narzędzia, mogli czerpać z niego pomysły — i żeby każdy, kto widzi lepsze rozwiązanie, mógł odesłać opinię lub kod.

Jeśli Ci to pomoże — dobrze. Jeśli chcesz pomóc temu rosnąć — też dobrze.

![status](https://img.shields.io/badge/status-working%20prototype-success)
![version](https://img.shields.io/badge/version-3.6.4-blue)
![Auto-update](https://img.shields.io/badge/auto--update-enabled-brightgreen?style=flat-square)
![runs in](https://img.shields.io/badge/runs%20in-your%20browser-0a84ff)
![offline](https://img.shields.io/badge/offline-ready-success)
![single file](https://img.shields.io/badge/single--file-HTML-orange)
![vue](https://img.shields.io/badge/vue-3-42b883)
![Privacy](https://img.shields.io/badge/privacy-100%25_local-blue?style=flat-square)

> **Wypróbuj teraz:** [otwórz wersję live](https://horkiroman4408-cyber.github.io/Mr.Robot/) — działa w całości w przeglądarce, bez instalacji i bez rejestracji.

---

## 📖 Spis treści

- [Czym to jest](#czym-to-jest)
- [Wypróbuj](#wypróbuj)
- [Po co to istnieje](#po-co-to-istnieje)
- [Szybkość i wydajność](#szybkość-i-wydajność)
- [Moduły (szczegóły)](#moduły)
- [Jak to jest zbudowane (pod maską)](#jak-to-jest-zbudowane)
- [Uruchamianie](#uruchamianie)
- [Pomagajmy sobie](#pomagajmy-sobie)
- [Co dalej](#co-dalej)
- [Podziękowania](#podziękowania)

---

## 💡 Czym to jest

Mr. Robot to aplikacja w przeglądarce do pracy z plikami magazynowymi — parsowanie raportów, porównywanie dwóch dużych arkuszy, filtrowanie lokalizacji, liczenie KPI, eksport czystych wyników.

To działający prototyp. Nie koncepcja, nie prezentacja. Możesz otworzyć go teraz i użyć na prawdziwych plikach.

To jeden plik. Bez instalacji, bez serwera, bez etapu budowania. Otwierasz `index.html` i działa. Wszystko wykonuje się na Twoim komputerze; nic nie jest nigdzie wysyłane. Wczytane pliki zostają w przeglądarce i są tam nadal po odświeżeniu strony.

**Zawsze aktualne.** Nie musisz pobierać pliku ponownie, żeby dostać najnowsze funkcje. Aplikacja automatycznie sprawdza aktualizacje w tle. Jeśli wdrożono nowszą wersję, w rogu pojawi się plakietka **„New”**. Wystarczy odświeżyć stronę, żeby wczytać najnowszą wersję. Zapisane pliki i dane pozostają bezpieczne w pamięci lokalnej przeglądarki.

Nie chodzi o to, że to największe ani najbardziej dopracowane narzędzie. Chodzi o to, że to coś, co jedna osoba może dziś złożyć w przeglądarce — i że zmienia to wyobrażenie o tym, czym może być „szybkie narzędzie wewnętrzne”.

---

## 🚀 Wypróbuj

Wersja live — działa w całości w przeglądarce, bez instalacji i bez konta:
**[Otwórz Mr. Robot](https://horkiroman4408-cyber.github.io/Mr.Robot/)**

Możesz też pobrać `index.html` i otworzyć go lokalnie. Działa w pełni offline. *(Uwaga: automatyczne sprawdzanie aktualizacji działa tylko w wersji hostowanej online).*

---

## 🔥 Po co to istnieje

Jeśli pracowałeś z raportami magazynowymi, znasz ten schemat. Przychodzi plik `.xlsx`. Ktoś otwiera go w Excelu, nakłada filtry, kopiuje kolumny do innego pliku, uruchamia makro VBA — aż makro się psuje po aktualizacji Excela. Potem każdy robi to trochę inaczej i nikt nie dostaje tych samych liczb.

Chciałem sprawdzić, co się stanie, jeśli cała ta pętla będzie żyć w przeglądarce. Co, jeśli parsowanie 50 tys. wierszy zajmie mniej niż sekundę? Co, jeśli filtry będą zdefiniowane raz, w kodzie, żeby każdy dostawał ten sam wynik? Co, jeśli codzienna rutyna, która zajmuje pół godziny, da się zrobić jednym kliknięciem?

Ten prototyp próbuje odpowiedzieć na te pytania. To nie zamiennik prawdziwego systemu produkcyjnego — to działający szkic tego, jak taki system mógłby wyglądać.

### Otwarte z założenia
To nie jest zamknięte narzędzie wewnętrzne. Jest udostępnione, żeby rosło w obie strony — z tego, co wiedzą inni, i ku temu, czego inni potrzebują. Jeśli rozwiązałeś podobny problem mądrzej, chcę o tym usłyszeć. Jeśli coś tutaj oszczędzi Ci tygodnia prób i błędów, po prostu to weź — bez konieczności podawania autora.

---

## ⚡ Szybkość i wydajność

To najważniejsza część.

### Co zwykle spowalnia ludzi
| Zadanie | Zwykły sposób |
|------|---------------|
| Otwarcie `.xlsx` z 50 000 wierszy | 10–30 sekund, czasem zawieszenie |
| Nakładanie filtrów i remapowanie kolumn | Ręcznie, z błędami |
| Porównanie dwóch dużych plików | Kopiuj-wklej, VLOOKUP, czekanie |
| Wygenerowanie czystego eksportu | Ręczne formatowanie za każdym razem |
| Powtórzenie tego jutro | Znowu tyle samo czasu |

### Co robi ten prototyp
| Zadanie | Mr. Robot |
|------|-----------|
| Otwarcie `.xlsx` z 50 000 wierszy | Parsowane poza głównym wątkiem — UI pozostaje responsywne |
| Filtry i mapowanie kolumn | Zdefiniowane raz w kodzie — zawsze ten sam wynik |
| Porównanie dwóch dużych plików | Mapy hash w pamięci — wyszukiwanie liniowe |
| Wygenerowanie czystego eksportu | Jedno kliknięcie → sformatowany `.xlsx` lub `.csv` |
| Powtórzenie tego jutro | Filtry i pliki są zapamiętane |

### Przybliżone liczby
To nie są dokładne benchmarki — tylko ogólna skala różnicy zauważona podczas budowy:
- Parsowanie dużych plików Excel: sekundy → znacznie poniżej sekundy, bez zamrażania strony.
- Porównanie dwóch plików po 100 tys. wierszy: minuty VLOOKUP-a → natychmiast.
- Codzienna rutyna (otwórz → filtruj → eksportuj): około 15–30 minut → około 30 sekund.
- Powtarzalność: ręczne kroki zastąpione deterministycznym kodem, więc błędy kopiuj-wklej przestają się zdarzać.

Teza nie brzmi „to najszybsze narzędzie świata”. Teza brzmi: przeglądarka już to potrafi — w jednym pliku, offline, bez instalacji — i to samo w sobie zmienia to, czym może być małe narzędzie wewnętrzne.

---

## 🧩 Moduły (szczegóły)

Aplikacja to hub z czterema sekcjami. Każda zastępuje powtarzalne zadanie.

### 1. KPI Norms — wydajność pracowników
Wczytaj raporty `.xlsx` przez przeciągnięcie, połącz je z plikiem grafiku (`Grafik.xlsx`), filtruj po grupie, procesie lub zmianie i czytaj liczby.

**Podmoduły:**
- **Audyt** — rozbicie KPI i INFO.
- **Scalanie** — KPI dla scalania / picking.
- **Rozkładanie** — KPI dla rozkładania, z wykrywaniem RSORT i Returns.
- **NADWE / VAS** — KPI z dwoma wierszami na login.
- **Statystyki** — jeden widok na wszystkie procesy: rankingi, efektywność, mediana, średnia.

**Co robi dobrze:**
- Progi norm oparte na medianie, regulowane per proces.
- Rankingi Top-3 / Top-5 / Top-10.
- Kolorowy eksport do Excela z formatowaniem warunkowym.
- Filtry budowane z pliku grafiku (grupa, proces, zmiana).

### 2. RS — Tote Finder
Porównuje dwie duże bazy w pamięci.

**Podmoduły:**
- **MP → RS Tote Finder** — dopasowuje EAN-y z MP do lokalizacji TOTE w RS.
- **Szukanie TOTE po EAN** — wklej listę, dostaniesz TOTE i ilość w inwentarzu.
- **AUDYT GEEK** — czyta plik zamówienia Stocktake i raportuje bez eksportu.

**Szczegóły, które mają znaczenie:**
- Strategia mediany lub minimalnej ilości przy wyborze TOTE.
- Wykrywanie i filtrowanie wielu TOTE.
- Świadomość 2×2 pop-tote.
- Kopiowanie do schowka i eksport do Excela.

### 3. MP — audyt i scalanie
**Podmoduły:**
- **AL_AUDYT** — KPI i INFO z raportu audytu.
- **FORMATKA_59** — format kontroli jakości z własnymi metrykami.
- **GODZINY_MDT** — analiza MDT, półka 1/1, listy lokalizacji.
- **STOCK** — raporty lokalizacji grupowane po godzinach przyjęcia.
- **Scalanie** — filtrowanie lokalizacji po półce, ABC, zakresie SKU.
- **Konsolidacja** — znajdowanie małych lokalizacji wartych konsolidacji.

**Uwagi:**
- Tam, gdzie istniało już makro VBA, logika jest dopasowana do niego, żeby liczby zgadzały się z tym, do czego ludzie przywykli.
- Kopiowanie do schowka jest po to, żeby wyniki dało się wkleić prosto do Excela lub WMS.
- Pliki CSV są eksportowane z dokładnie takimi nazwami, jakich oczekują narzędzia downstream.

### 4. Inne
- **Analiza_Przestojów** — analiza przestojów per USER ID, od 8 do 300 minut.
- **ARTLTT** — wklej nazwy produktów, dostań pliki LTT jako CSV.
- **TH Reports** — generowanie i parsowanie raportów (w toku).

---

## ⚙️ Jak to jest zbudowane (pod maską)

Kilka decyzji, które czynią to szybkim:
- **Wszystko mieści się w jednym pliku.** Vue, Tailwind, SheetJS i Web Workery są wbudowane. Bez CDN, bez etapu budowania, bez zależności runtime.
- **Parsowanie Excela działa w Web Workerze**, więc interfejs nie zamarza na dużych plikach.
- **Porównywanie wykorzystuje mapy hash**, co zamienia powtarzane wyszukiwania w pracę liniową.
- **Stan jest reaktywny w pamięci**, a pliki są utrwalane w IndexedDB, żeby odświeżenie nie traciło kontekstu.
- **Inteligentne auto-aktualizacje.** Aplikacja okresowo pobiera w tle własny `index.html`, czyta tag wersji i porównuje go z uruchomioną instancją. Jeśli wykryje nowszą wersję, pojawia się plakietka powiadomienia.
- **Logika jest deterministyczna** — ten sam input, ten sam output, dla każdego, kto z tego korzysta.

---

## 🏃 Uruchamianie

**Wersja live:**
**[Otwórz Mr. Robot](https://horkiroman4408-cyber.github.io/Mr.Robot/)**

**Albo uruchom sam:**
1. Pobierz `index.html`.
2. Kliknij dwukrotnie albo przeciągnij do przeglądarki.
3. To wszystko.

Żeby hostować samodzielnie, zrób fork repo i włącz GitHub Pages w **Settings → Pages**.
Potrzebna jest nowoczesna przeglądarka — Chrome, Edge, Safari lub Firefox. Nic więcej.

---

## 🤝 Pomagajmy sobie

To repo to prototyp, udostępniony otwarcie. Może działać w obie strony.

### Co to może dać Tobie
Jeśli budujesz coś do pracy magazynowej lub inwentaryzacyjnej, oto pomysły najbardziej warte podjęcia:
- Jeden `index.html`, który każdy może uruchomić, bije repo wymagające Node, Dockera i CI dla narzędzia używanego przez pięć osób.
- Parsowanie `.xlsx` obciąża CPU. Przeniesienie go do Web Workera utrzymuje płynność UI na ogromnych plikach.
- Dwa duże pliki łączone w pamięci biją każdy VLOOKUP, jaki kiedykolwiek napiszesz.
- IndexedDB sprawia, że odświeżenie strony wygląda, jakby nic się nie stało.
- Filtry i formuły w kodzie oznaczają, że każdy dostaje te same liczby.
- Jeśli rutyna wymaga dwudziestu kliknięć, każdy zrobi ją inaczej. Jeśli jednego — wszyscy tak samo.

Korzystaj, adaptuj, przepisuj we własnym stacku. Jeśli coś z tego trafi do tego, co budujesz — notka, link zwrotny albo po prostu wiadomość „cześć” będą naprawdę docenione. Nie jest to wymagane, ale sprawia, że praca wydaje się warta dzielenia.

### Co pomogłoby temu projektowi
Jeśli chcesz pomóc mu rosnąć, oto co jest naprawdę przydatne:
- **Pomysły.** Mądrzejszy sposób filtrowania, brakujący moduł, przepływ, którego jeszcze nie ma.
- **Zgłoszenia błędów.** Plik, który nie parsuje się poprawnie, KPI, który wygląda podejrzanie, przypadek brzegowy, który coś psuje.
- **Pull requesty.** Drobne poprawki, nowe filtry albo zupełnie nowy podmoduł.
- **Opinia o designie.** Co jest mylące, co wydaje się wolne, co wydaje się nie tak.
- **Inne języki.** UI jest po polsku i angielsku. Więcej mile widziane.
- **Prawdziwe dane.** Prototyp działa najlepiej, gdy jest popychany prawdziwymi plikami z prawdziwych magazynów.

Jeśli pracujesz nad czymś podobnym, otwórz issue i się przywitaj. Wolę wymieniać notatki niż pracować w izolacji.

---

## 🛣️ Co dalej

**Zrobione do tej pory:**
- [x] Panel KPI ze statystykami i rankingami
- [x] Porównywanie wielu plików (Tote Finder)
- [x] Analiza audytu w aplikacji bez eksportu do Excela
- [x] Trwałe przechowywanie plików z IndexedDB
- [x] Parsowanie Excela poza wątkiem z Web Workerami
- [x] Sprawdzanie auto-aktualizacji w tle

**Planowane lub rozważane:**
- [ ] Moduł TH Reports
- [ ] Eksport do PDF
- [ ] Przetwarzanie wsadowe wielu plików
- [ ] Formuły i filtry definiowane przez użytkownika
- [ ] Opcjonalna synchronizacja w chmurze (opt-in)

---

## 🏆 Podziękowania

Ten prototyp można swobodnie czytać, uczyć się z niego i budować na nim. Nie ma bramki licencyjnej ani prawnego wymogu wymieniania autora.

To powiedziawszy — jeśli bierzesz stąd kod, pomysły lub całe moduły i wkładasz je do czegoś swojego, byłoby naprawdę miło zostawić gdzieś małe podziękowanie (link, nazwisko, wzmianka w README). Nie dlatego, że się należy, ale dlatego, że tak małe otwarte projekty zachowują motywację do dalszego dzielenia się.

Jeśli wolisz po prostu się przywitać i powiedzieć, co z tym zbudowałeś — to też działa. Otwórz issue albo napisz — chcę to zobaczyć.

---

## 👨‍💻 Autor

**Raman Horki**
> *Jeśli robisz to samo dwa razy — zautomatyzuj to.*

Otwarty na opinie i współpracę. Jeśli masz przemyślenia, otwórz issue w tym repozytorium.

© 2026 Mr. Robot · Made by Raman Horki ·
