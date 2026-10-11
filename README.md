# ROI Business Calculator — jeden plik HTML

Aktualna aplikacja jest w **index.html**: HTML z osadzonym CSS i JavaScriptem. Nie wymaga Reacta, Node.js, backendu, bibliotek zewnętrznych ani instalacji. Po załadowaniu nie wykonuje żądań sieciowych. Pliki poprzedniej wersji zachowano lokalnie w środowisku roboczym; nie są częścią publikowanej aplikacji HTML.

## Uruchomienie

Otwórz `index.html` w aktualnej przeglądarce albo umieść go na statycznym hostingu. W środowisku chmurowym (gdzie polityka przeglądarki blokuje file://) uruchom sam plik:

```sh
mkdir -p /tmp/roi-html-preview
cp /workspace/test/index.html /tmp/roi-html-preview/index.html
python3 -m http.server 3000 --bind 0.0.0.0 --directory /tmp/roi-html-preview
```

Python służy tylko jako opcjonalny serwer statyczny. Przeglądarka wykonuje całą logikę. Po zmianie pliku skopiuj go ponownie i odśwież stronę. Nie serwuj całego repozytorium, które może zawierać wcześniejsze dane SQLite. Polecenia npm należą do poprzedniej wersji, nie do aplikacji HTML.

## Funkcjonalności

- Polski, responsywny formularz i wyniki aktualizowane na żywo.
- ROI względem wszystkich kosztów, zysk, payback, roczna korzyść netto, koszty i korzyści.
- Wykresy SVG, tekstowe interpretacje, walidacja, ostrzeżenia o niezapisanych zmianach.
- Zapis i edycja w localStorage, odtworzenie po odświeżeniu, kopiowanie i usuwanie z potwierdzeniem; wyszukiwanie, kategorie, sortowanie.
- Prawdziwy XLSX generowany lokalnie: cztery arkusze, aktywne formuły, wyniki w cache. Dokładne kwoty źródłowe zapisano dodatkowo jako tekst w kolumnie C.
- PDF: kliknij **PDF**, następnie wybierz **Zapisz jako PDF** w oknie drukowania. Raport A4 zawiera polskie znaki, dane, wyniki, wykresy i metodologię. Dla numeracji stron włącz nagłówki i stopki przeglądarki.

Kwoty liczone są jako całkowite grosze (BigInt), bez utraty precyzji. Maks. 16 cyfr całkowitych i 2 po przecinku; obsługiwany przecinek i kropka. Wykresy używają przybliżonych liczb, Excel ma limit 15 cyfr znaczących. Model 1.0. Nieczytelne wcześniejsze dane nie są nadpisywane; zmiany w innej karcie blokują zapis do odświeżenia.

## Ograniczenia wersji HTML

To wersja lokalna: **bez firmowego SSO, serwerowej kontroli właścicieli, centralnego audytu, synchronizacji, szyfrowania danych i automatycznych kopii**. Wymagają one backendu lub zewnętrznych usług. Każdy użytkownik profilu przeglądarki ma dostęp do zapisanych analiz. Nie używaj do poufnych danych na współdzielonych urządzeniach. Wyczyszczenie pamięci przeglądarki usuwa analizy; eksportuj ważne raporty.

Analizy są przypisane do profilu przeglądarki i adresu strony. Zmiana domeny lub portu oznacza osobną pamięć. Dane wcześniejszej wersji w `data/` pozostawiono bez zmian; aplikacja HTML ich nie odczytuje ani nie migruje.

## Weryfikacja

W Chromium przez serwer statyczny przeszły: referencja PRD (38,46%, 50 000 zł, 24,0 mies.), zmiana korzyści, przypadki zerowe i nieosiągalny zwrot, walidacja i dokładność dużych kwot, zapis/odświeżenie, wyszukiwanie, kopiowanie/usuwanie, bezpieczne kodowanie nazw, odczyt XLSX niezależną biblioteką oraz układ 360 px bez poziomego przewijania. Wydruk PDF zawierał polskie znaki, poprawne wyniki i numery obu stron.

Bezpośredni test file:// zablokowała polityka zarządzanej przeglądarki chmurowej; wariant HTTP został zweryfikowany. Nie wykonano formalnego audytu WCAG ani testów innych przeglądarek. Funkcje P2 (NPV/IRR, porównanie, ERP) pozostają poza zakresem.
