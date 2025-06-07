# Nowa struktura systemu lokalizacji

System lokalizacji w RogueDungeon został rozszerzony, aby obsługiwać zarówno pojedyncze pliki jak i foldery z wieloma plikami JSON dla każdego języka.

## Obsługiwane struktury

### 1. Stara struktura (kompatybilność wsteczna)

```
StreamingAssets/Localization/
├── config.json
├── pl_PL.json
├── en_US.json
└── pl_PL.lang
```

### 2. Nowa struktura - foldery z językami

```
StreamingAssets/Localization/
├── config.json
├── pl_PL/
│   ├── menu.json
│   ├── game.json
│   ├── settings.json
│   └── common.json
└── en_US/
    ├── menu.json
    ├── game.json
    ├── settings.json
    └── common.json
```

### 3. Struktura dla modów

```
StreamingAssets/Mods/[ModName]/Localization/
├── pl_PL/
│   └── mod_content.json
└── en_US/
    └── mod_content.json
```

## Zalety nowej struktury

1. **Modularność**: Można podzielić tłumaczenia na logiczne sekcje (menu, ustawienia, gra itp.)
2. **Łatwiejsze zarządzanie**: Każdy moduł może być edytowany niezależnie
3. **Wsparcie dla modów**: Mody mogą dodawać własne pliki lokalizacji bez modyfikowania głównych plików
4. **Scalanie**: System automatycznie scala wszystkie pliki JSON dla danego języka
5. **Konflikty**: System loguje ostrzeżenia gdy ten sam klucz występuje w różnych plikach

## Jak używać

### Podział istniejącego pliku lokalizacji

1. Utwórz folder z kodem języka (np. `pl_PL/`)
2. Podziel zawartość JSON na logiczne pliki:
    - `common.json` - podstawowe elementy (on/off, przyciski)
    - `menu.json` - elementy menu
    - `game.json` - elementy gry
    - `settings.json` - ustawienia
    - itd.

### Tworzenie lokalizacji dla moda

1. Utwórz strukturę: `Mods/[NazwaModa]/Localization/[KodJęzyka]/`
2. Dodaj pliki JSON z tłumaczeniami
3. System automatycznie załaduje je podczas inicjalizacji

## Przykład wykorzystania

```csharp
// Te klucze będą działać niezależnie od tego, czy są w jednym pliku czy rozdzielone
string menuTitle = Localization.Get("menu.new_game");
string commonButton = Localization.Get("button.ok");
string modItem = Localization.Get("example_mod.items.super_sword");
```

## Migracja

System zachowuje pełną kompatybilność wsteczną. Można:

1. Używać starych pojedynczych plików
2. Stopniowo migrować do nowej struktury
3. Mieszać obie struktury

Zaleca się używanie nowej struktury dla nowych projektów i modów.
