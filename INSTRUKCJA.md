# TECH-USLUGI — instrukcja wdrożenia

## Zawartość
- `index.html` — układ strony
- `style.css` — responsywny styl, animacje i kolory
- `script.js` — automatyczne wczytywanie danych z Pages CMS, galeria z powiększaniem, formularz
- `content/site.json` — wszystkie teksty i ustawienia firmy
- `content/gallery.json` — galeria (początkowo pusta)
- `.pages.yml` — konfiguracja Pages CMS
- `polityka-prywatnosci.html` — SZABLON wymagający uzupełnienia

## Uruchomienie na GitHub + Cloudflare Pages
1. Rozpakuj ZIP. Utwórz **osobne** repozytorium GitHub dla każdego klienta.
2. Prześlij do katalogu głównego repozytorium wszystkie pliki i foldery, **także ukryty plik `.pages.yml`**.
3. Cloudflare Dashboard → Workers & Pages → Create application → Pages → Connect to Git → wybierz repozytorium.
4. Production branch `main`, Framework preset `None`, Build command PUSTE, Build output directory `/` lub `.` (katalog główny; zależnie od formularza Cloudflare).
5. Kliknij Save and Deploy. Sprawdź wygenerowany adres `*.pages.dev`.
6. Otwórz https://app.pagescms.org/ i zaloguj się GitHub. Wybierz repozytorium. Edytuj `Treści i ustawienia` oraz `Galeria`.
7. W `Treści i ustawienia` ustaw prawdziwe dane klienta, numery, adres, teksty, godziny i usługi. Zdjęcia dodawaj w Galerii.
8. Załóż dla klienta osobny formularz na https://formspree.io/, potwierdź odbiorczy e-mail klienta, skopiuj endpoint `https://formspree.io/f/xxxxxxxx` i wpisz go w pole `form_endpoint` w Pages CMS. Bez tego formularz celowo nie wysyła zgłoszeń.
9. Wpisz numer WhatsApp jako `48` + 9 cyfr, bez `+`, np. `48500600700`.
10. Uzupełnij dokument prywatności dla faktycznej firmy i dostawców; przykładowa treść nie jest gotową polityką RODO.
11. Sprawdź stronę na telefonie, galerię, formularz testowy, linki, SEO, prawdziwe opinie.

## Domena
W Cloudflare Pages → Custom domains dodaj domenę klienta i wykonaj wskazaną konfigurację DNS. Domena jest zwykle płatna, hosting może pozostać darmowy.

## Zasady bezpiecznej sprzedaży
- Najlepiej, by domena, GitHub, Cloudflare i formularz były własnością klienta, a Ty miał dostęp jako wykonawca.
- Nie używaj fikcyjnych opinii jako prawdziwych. W `site.json` jest wyraźnie oznaczona opinia przykładowa — usuń ją przed publikacją dla klienta.
- Darmowy Formspree ma limity i może nie obsługiwać załączników. Ten szablon nie ma uploadu zdjęć; zdjęcia można wysłać przez WhatsApp.
- Szablon to statyczna witryna prezentacyjna, nie sklep z płatnościami ani system rezerwacyjny.
- Nie publikuj danych przykładowych, nie używaj cudzych zdjęć bez licencji, sprawdź zgody na cookies i inne integracje, jeśli je dodasz.

## Dostosowanie kolorów
W `style.css` zmień zmienne `--bg`, `--panel`, `--ink`, `--muted`, `--accent` w `:root`.

## Galeria
Pages CMS zapisuje `content/gallery.json` w formacie `{"images":[{"image":"/media/plik.jpg","caption":"Opis"}]}`.
Witryna automatycznie odczytuje JSON i aktualizuje się po publikacji w Cloudflare.

## Test lokalny
Z katalogu projektu uruchom `python -m http.server 8000`, następnie wejdź na http://localhost:8000. Nie otwieraj `index.html` bezpośrednio z dysku, bo przeglądarka może zablokować fetch JSON.
