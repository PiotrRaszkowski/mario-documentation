---
title: Integracja z Allegro
---

# MarioTheAgent — integracja z Allegro

[← Wszystkie integracje](../)

## Czym jest MarioTheAgent

MarioTheAgent to prywatne narzędzie jednego sprzedawcy, służące do ewidencji dostaw towaru i sprzedaży. Aplikacja nie
jest oferowana innym sprzedawcom i działa wyłącznie na koncie swojego właściciela.

## Jak aplikacja korzysta z Allegro REST API

Aplikacja **wyłącznie odczytuje** dane o zamówieniach. Niczego w Allegro nie tworzy, nie zmienia ani nie usuwa.

| Wywołanie | Cel |
|---|---|
| `GET /order/checkout-forms` | pierwsze wczytanie zamówień oraz nocne uzgodnienie stanu |
| `GET /order/checkout-forms/{checkoutFormId}` | pobranie pojedynczego zamówienia, którego dotyczy zdarzenie |
| `GET /order/events` | bieżące zmiany w zamówieniach, odpytywane co kilka minut |
| `GET /order/event-stats` | punkt startowy dziennika zdarzeń |

Wymagany zakres uprawnień: `allegro:api:orders:read`.

## Autoryzacja

Aplikacja używa OAuth 2.0 Device Flow (`device_code`): pokazuje kod i link, a właściciel konta potwierdza dostęp
w przeglądarce. Tokeny są przechowywane wyłącznie na serwerze właściciela i odświeżane za pomocą `refresh_token`.
Dostęp można w każdej chwili cofnąć w ustawieniach konta Allegro.

## Dane

Pobrane dane trafiają wyłącznie do bazy danych właściciela. Z danych kupującego zapisywane są tylko identyfikator
i login Allegro (bez imienia, nazwiska, adresu, e-maila i telefonu). Dane nie są udostępniane osobom trzecim ani
wykorzystywane w innym celu niż ewidencja sprzedaży.

## Kontakt

Pytania i zgłoszenia: [Issues repozytorium dokumentacji](https://github.com/PiotrRaszkowski/mario-documentation/issues).
