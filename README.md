# Mario — integracja z Allegro REST API

Mario to prywatne narzędzie jednego sprzedawcy do ewidencji dostaw towaru i sprzedaży. Aplikacja nie jest
udostępniana innym sprzedawcom i działa wyłącznie na koncie swojego właściciela.

## Co robi z Allegro

Mario **tylko odczytuje** zamówienia z konta sprzedawcy, żeby pokazać je obok danych o dostawach i kosztach zakupu.
Niczego w Allegro nie tworzy, nie zmienia ani nie usuwa.

| Wywołanie | Cel |
|---|---|
| `GET /order/checkout-forms` | pobranie zamówień (pierwsze wczytanie i nocne uzgodnienie) |
| `GET /order/events` | bieżące zmiany zamówień, odpytywane co kilka minut |
| `GET /order/event-stats` | punkt startowy dziennika zdarzeń |

Wymagane uprawnienie: `allegro:api:orders:read`.

## Autoryzacja

Konto łączy się przez OAuth 2.0 Device Flow (`grant_type: device_code`): Mario pokazuje kod i link do strony Allegro,
a właściciel konta potwierdza dostęp w przeglądarce. Tokeny są przechowywane wyłącznie na serwerze właściciela
i odświeżane przez `refresh_token`. Dostęp można cofnąć w każdej chwili w ustawieniach konta Allegro.

## Dane

Dane zamówień trafiają tylko do bazy na serwerze właściciela. Nie są przekazywane osobom trzecim ani wykorzystywane
w innym celu niż prowadzenie ewidencji sprzedaży.

## Kontakt

Pytania dotyczące aplikacji: [Issues tego repozytorium](https://github.com/PiotrRaszkowski/mario-allegro/issues).
