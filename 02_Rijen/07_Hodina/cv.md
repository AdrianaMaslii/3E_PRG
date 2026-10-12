## Úloha 1 – Inventář dobrodruha

Vytvořte jednoduchý inventář hráče, který uchovává názvy pěti předmětů.

**Zadání:**

1. Vytvořte pole `string[]` o délce 5.
2. Pomocí cyklu `for` nechte uživatele zadat názvy pěti předmětů.
3. Vypište obsah inventáře pomocí cyklu `foreach`.
4. Požádejte uživatele o název předmětu, který chce zahodit.
5. Pomocí `Array.IndexOf()` vyhledejte předmět v inventáři.
6. Pokud předmět existuje, nahraďte jej textem `"Prázdný slot"`. Pokud neexistuje, vypište chybovou hlášku.
7. Vypište aktualizovaný inventář.

**Příklad výstupu:**

```text
INVENTÁŘ

1. Meč
2. Luk
3. Lektvar
4. Štít
5. Pochodeň

Jaký předmět chcete zahodit?
Luk

Předmět Luk byl zahozen.

INVENTÁŘ
1. Meč
2. Prázdný slot
3. Lektvar
4. Štít
5. Pochodeň
```

## Úloha 2 – Hod kostkami

Vytvořte simulátor hodů šestistěnnou kostkou, který umožní vyhodnotit výsledky jednotlivých hodů.

**Zadání:**

1. Požádejte uživatele o počet hodů kostkou.
2. Vytvořte celočíselné pole `int[]` odpovídající délky.
3. Pomocí `Random` vygenerujte náhodné číslo od 1 do 6 pro každý hod a uložte jej do pole.
4. Vypište všechny výsledky hodů.
5. Vypočítejte součet všech hodů a jejich průměr.
6. Zjistěte nejvyšší a nejnižší hozenou hodnotu.
7. Spočítejte, kolikrát padla šestka.

**Příklad výstupu:**

```text
Kolikrát chcete hodit kostkou?
8

Výsledky:
3 6 2 4 6 1 5 6

Součet: 33
Průměr: 4,125
Nejvyšší hod: 6
Nejnižší hod: 1
Počet šestek: 3
```

**Bonus:** Seřaďte výsledky vzestupně pomocí `Array.Sort()` a vypište je.

## Úloha 3 – Žebříček hráčů

Vytvořte jednoduchý systém pro správu nejlepších výsledků v počítačové hře.

**Zadání:**

1. Vytvořte pole obsahující následující výsledky:

   ```csharp
   int[] scores = { 150, 320, 80, 450, 210 };
   ```

2. Vypište všechny výsledky.
3. Seřaďte výsledky od nejvyššího po nejnižší pomocí `Array.Sort()` a `Array.Reverse()`.
4. Vypište tři nejlepší výsledky.
5. Požádejte uživatele o zadání nového výsledku.
6. Pomocí `Array.Resize()` zvětšete pole o jeden prvek a nový výsledek do něj vložte.
7. Znovu seřaďte výsledky a vypište aktualizovaný žebříček.

**Příklad výstupu:**

```text
ŽEBŘÍČEK
1. 450 bodů
2. 320 bodů
3. 210 bodů
4. 150 bodů
5. 80 bodů

TOP 3:
1. 450 bodů
2. 320 bodů
3. 210 bodů

Zadejte nový výsledek:
500

AKTUALIZOVANÝ ŽEBŘÍČEK
1. 500 bodů
2. 450 bodů
3. 320 bodů
4. 210 bodů
5. 150 bodů
6. 80 bodů
```