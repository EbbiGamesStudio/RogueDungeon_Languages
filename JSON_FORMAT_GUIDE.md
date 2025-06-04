# Obsługa formatów lokalizacji

System lokalizacji w RogueDungeon obsługuje teraz dwa formaty plików:

## Format .lang (oryginalny)

Tradycyjny format klucz=wartość:

```ini
# Komentarz
lang=Polski
menu_new_game=Nowa gra
menu_settings=Ustawienia
game_version=wersja {0}a {1}
```

## Format .json (nowy)

Obsługuje zagnieżdżone struktury dla lepszej organizacji:

### Płaska struktura

```json
{
 "lang": "Polski",
 "menu_new_game": "Nowa gra",
 "menu_settings": "Ustawienia",
 "game_version": "wersja {0}a {1}"
}
```

### Struktura zagnieżdżona

```json
{
 "lang": "Polski",
 "menu": {
  "new_game": "Nowa gra",
  "settings": "Ustawienia"
 },
 "game": {
  "version": "wersja {0}a {1}"
 }
}
```

Zagnieżdżone klucze są automatycznie konwertowane na format kropkowy:

- `menu.new_game` → "Nowa gra"
- `game.version` → "wersja {0}a {1}"

## Używanie w kodzie

```csharp
// Dla płaskiej struktury
string newGame = Localization.Get("menu_new_game");

// Dla struktury zagnieżdżonej
string newGame = Localization.Get("menu.new_game");
string version = Localization.Get("game.version", "1.0", "alpha");
```

## Zalety JSON

1. **Lepsza organizacja** - grupowanie powiązanych tłumaczeń
2. **Wsparcie IDE** - syntax highlighting, sprawdzanie składni
3. **Łatwiejsze zarządzanie** - czytelniejsza struktura dla większych projektów
4. **Zachowanie kompatybilności** - format .lang nadal jest obsługiwany

## Migracja z .lang do .json

System automatycznie rozpoznaje format na podstawie rozszerzenia pliku. Można stopniowo migrować pliki lub używać obu formatów jednocześnie.
