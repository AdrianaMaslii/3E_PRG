# Seznamy (`List<T>`) v C#

---

# 1. Co je `List<T>`

- **`List<T>`** je kolekce, která uchovává prvky stejného typu v daném pořadí.
- Na rozdíl od pole se **počet prvků může měnit**: lze je přidávat a odebírat.
- `List<T>` je **referenční typ**. Písmeno `T` představuje typ ukládaných prvků, například `int` nebo `string`.
- Indexuje se od **0**, stejně jako pole.
- Počet prvků udává vlastnost **`Count`**, nikoli `Length`.
- Pro práci se seznamem používáme `System.Collections.Generic` (v novějších projektech může být tento prostor názvů dostupný automaticky).

```csharp
using System.Collections.Generic;

List<int> numbers = new List<int>();       // prázdný seznam
List<string> names = new() { "Anna", "Petr" }; // 2 prvky
List<int> scores = new() { 10, 20, 30 };

Console.WriteLine(numbers.Count); // 0
Console.WriteLine(names.Count);   // 2
```

**Srovnání s polem:**

```csharp
int[] array = { 10, 20, 30 };       // pevná délka
List<int> list = new() { 10, 20, 30 }; // měnitelný počet prvků

Console.WriteLine(array.Length); // 3
Console.WriteLine(list.Count);   // 3
```

### Otázky

1. Jaký je hlavní rozdíl mezi polem a `List<T>`?
2. Jak zjistíte počet prvků seznamu?

### Krátký úkol

Vytvořte seznam `List<string>` se třemi názvy her a vypište počet jeho prvků.

---

# 2. Přístup k prvkům a změna hodnot

- Ke konkrétnímu prvku přistupujeme pomocí **indexu v hranatých závorkách**.
- Prvky můžeme číst a přepisovat.
- Poslední platný index je `Count - 1` (pokud seznam není prázdný).
- Neplatný index vyvolá **`ArgumentOutOfRangeException`**.

```csharp
List<int> hp = new() { 100, 80, 50 };

int first = hp[0];    // 100
hp[1] = 75;          // {100, 75, 50}
int last = hp[hp.Count - 1]; // 50

// int error = hp[3]; // chyba: existují jen indexy 0, 1, 2
```

**Pozor na prázdný seznam:**

```csharp
List<int> empty = new();

if (empty.Count > 0)
{
    Console.WriteLine(empty[0]);
}
```

### Otázky

1. Jaký index má první prvek seznamu?
2. Co se stane při pokusu o přečtení `hp[3]` v uvedeném příkladu?

### Krátký úkol

Vytvořte seznam tří čísel. Druhé číslo změňte na `99` a vypište první a poslední číslo.

---

# 3. Přidávání a odebírání prvků

- **`Add(value)`** přidá prvek na konec.
- **`Insert(index, value)`** vloží prvek na určené místo; následující prvky se posunou.
- **`Remove(value)`** odstraní **první výskyt** dané hodnoty a vrací `true`, pokud se odstranění povedlo.
- **`RemoveAt(index)`** odstraní prvek podle indexu.
- **`Clear()`** odstraní všechny prvky. Na rozdíl od `Array.Clear` se počet prvků sníží na nulu.

```csharp
List<string> inventory = new() { "Meč", "Lektvar" };

inventory.Add("Klíč");         // {"Meč", "Lektvar", "Klíč"}
inventory.Insert(1, "Štít");   // {"Meč", "Štít", "Lektvar", "Klíč"}
inventory.Remove("Lektvar");   // {"Meč", "Štít", "Klíč"}
inventory.RemoveAt(0);         // {"Štít", "Klíč"}

Console.WriteLine(inventory.Count); // 2
inventory.Clear();
Console.WriteLine(inventory.Count); // 0
```

### Otázky

1. Jaký je rozdíl mezi `Remove` a `RemoveAt`?
2. Co udělá `Insert(0, "Mapa")`?
3. Co vrátí `Remove("Klíč")`, když seznam klíč neobsahuje?

### Krátký úkol

Vytvořte seznam `List<string>` se dvěma předměty inventáře. Přidejte třetí předmět, vložte jeden na začátek, odeberte jeden podle názvu a vypište seznam pomocí `string.Join(", ", inventory)`.

---

# 4. Procházení seznamu (`for` a `foreach`)

- **`for`** použijte, pokud potřebujete index nebo chcete měnit hodnoty na jednotlivých pozicích.
- **`foreach`** je vhodný pro jednoduché čtení všech prvků.
- Při procházení pomocí `foreach` **nepřidávejte ani neodebírejte** prvky daného seznamu; může dojít k `InvalidOperationException`.

```csharp
List<int> points = new() { 5, 10, 15 };

// Změna hodnot podle indexu
for (int i = 0; i < points.Count; i++)
{
    points[i] *= 2;
}

// Výpis hodnot
foreach (int point in points)
{
    Console.WriteLine(point); // 10, 20, 30 (každé na novém řádku)
}
```

**Odebírání při průchodu:** při použití `for` a mazání podle indexu často pomůže průchod odzadu.

```csharp
List<int> values = new() { 1, 2, 3, 4, 5 };

for (int i = values.Count - 1; i >= 0; i--)
{
    if (values[i] % 2 == 0)
        values.RemoveAt(i);
}
// {1, 3, 5}
```

### Otázky

1. Kdy je vhodnější `for` než `foreach`?
2. Proč při mazání podle indexu může být výhodné procházet seznam odzadu?

### Krátký úkol

Vytvořte seznam pěti čísel. Pomocí cyklu `for` každé číslo zvyšte o `1`. Následně celý seznam vypište pomocí `foreach`.

---

# 5. Vyhledávání, řazení a další metody

- **`Contains(value)`** zjistí, zda se prvek nachází v seznamu (`true`/`false`).
- **`IndexOf(value)`** vrátí index prvního výskytu nebo `-1`, pokud prvek neexistuje.
- **`Sort()`** seřadí prvky vzestupně (u řetězců podle výchozího porovnávání).
- **`Reverse()`** obrátí aktuální pořadí prvků; samo o sobě neřadí.

```csharp
List<int> numbers = new() { 4, 1, 7, 1, 3 };

Console.WriteLine(numbers.Contains(7)); // True
Console.WriteLine(numbers.IndexOf(1));  // 1
Console.WriteLine(numbers.IndexOf(9));  // -1

numbers.Sort();    // {1, 1, 3, 4, 7}
numbers.Reverse(); // {7, 4, 3, 1, 1}
```

### Otázky

1. Jaký je rozdíl mezi `Contains` a `IndexOf`?
2. Seřadí samotné `Reverse()` čísla od největšího po nejmenší?

### Krátký úkol (3 minuty)

Vytvořte seznam známek `{ 3, 1, 4, 2, 1 }`. Zjistěte, zda obsahuje známku `5`, potom seznam seřaďte a vypište.

---

# 6. Převod na pole

- Seznam si při přidávání podle potřeby zajišťuje větší kapacitu automaticky.
- **`ToArray()`** vytvoří nové pole s kopií prvků seznamu.
- **`new List<int>(array)`** vytvoří seznam z prvků pole.

```csharp
List<int> numbers = new() { 10, 20, 30 };

Console.WriteLine(numbers.Count);    // 3
Console.WriteLine(numbers.Capacity); // alespoň 3 (přesná hodnota se může lišit)

int[] array = numbers.ToArray();       // nové pole {10, 20, 30}
List<int> copy = new List<int>(array); // nový seznam {10, 20, 30}
```

### Otázky

1. Znamená `Capacity == 10`, že má seznam deset uložených prvků?
2. Co vznikne voláním `ToArray()`?

### Krátký úkol

Vytvořte seznam tří čísel, převeďte ho na pole pomocí `ToArray()` a vypište délku nového pole.

---

# 7. Kopírování, sdílení reference a předávání metodám

- Při přiřazení `=` se **nekopírují prvky**. Obě proměnné odkazují na tentýž seznam.
- `new List<int>(original)` vytvoří **nový seznam** se stejnými prvky (mělká kopie; u referenčních prvků se sdílejí samotné objekty).
- Metoda dostává běžně **kopii reference**. Změny obsahu seznamu se projeví i mimo metodu.
- Přiřazení nového seznamu samotnému parametru však nepřesměruje proměnnou volajícího.

```csharp
List<int> original = new() { 1, 2, 3 };
List<int> alias = original;
List<int> copy = new List<int>(original);

alias[0] = 99;
Console.WriteLine(original[0]); // 99

copy[1] = 77;
Console.WriteLine(original[1]); // 2
```

```csharp
static void AddBonus(List<int> scores)
{
    scores.Add(100); // změní původní seznam
    scores = new List<int> { 0 }; // změní jen místní proměnnou
}

List<int> scores = new() { 10, 20 };
AddBonus(scores);
Console.WriteLine(string.Join(", ", scores)); // 10, 20, 100
```

### Otázky

1. Proč se po `alias[0] = 99` změní také `original[0]`?
2. Projeví se přidání prvku uvnitř metody také u volajícího?

### Krátký úkol

Vytvořte seznam čísel a jeho kopii pomocí `new List<int>(original)`. V kopii změňte první prvek. Vypište první prvek obou seznamů a ověřte, že se původní nezměnil.

---

# 8. Praktický minipříklad – evidence skóre

Následující příklad kombinuje vytvoření seznamu, přidání hodnot, vyhledávání, řazení a výpis.

```csharp
List<int> scores = new() { 120, 80, 150 };

scores.Add(100);

if (scores.Contains(80))
{
    scores.Remove(80);
}

scores.Sort();
scores.Reverse();

Console.WriteLine($"Počet skóre: {scores.Count}");
Console.WriteLine($"Skóre: {string.Join(", ", scores)}");

if (scores.Count > 0)
{
    Console.WriteLine($"Nejvyšší skóre: {scores[0]}");
}
```

**Výstup:**

```text
Počet skóre: 3
Skóre: 150, 120, 100
Nejvyšší skóre: 150
```

### Otázky

1. Proč po `Sort()` následuje `Reverse()`?
2. Proč se před čtením `scores[0]` kontroluje `scores.Count > 0`?

### Krátký úkol

Upravte příklad tak, aby po přidání nového skóre `200` program vypisoval také **nejnižší skóre**. Použijte již seřazený seznam a jeho indexy.

---

# Shrnutí

| Pole (`T[]`) | Seznam (`List<T>`) |
|---|---|
| Pevný počet prvků | Počet prvků lze měnit |
| `Length` | `Count` |
| `array[i]` | `list[i]` |
| Zvětšení vyžaduje vytvoření nového pole (např. `Array.Resize`) | `Add()`, `Insert()`, `Remove()`, `RemoveAt()` |
| `Array.Sort(array)` | `list.Sort()` |
