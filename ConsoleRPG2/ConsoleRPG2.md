# Практическая работа №5 Одномерные массивы в C#, класс System.Array и модульная консольная RPG😁
# Разработчики: Гильметднов Роман, Бабыкин Никита
## Игра 🎮
### Выполнена в сеттинге "Древнерусская застава (Богатырский дозор)"

```csharp
using System;

// Статы всего
int currentHP = 100;
int maxHP = 100;

int currentEnrg = 35;
int maxEnrg = 100;

// Расходники
int currentHealCount = 3;
int maxHealCount = 3;
int currentEnergizer = 3;
int maxEnergizer = 3;

//статы врагов
int currentMercHP = 70;
int maxMercHP = 100;
int currentMercE = 65;
int maxMercE = 100;

int currentNjHp = 100;
int maxNjHP = 120;
int currentNjE = 80;
int maxNjE = 110;

int currentMsHP = 130;
int MaxMsHP = 170;
int currentMsE = 110;
int maxMsE = 130;

// Переменные для защиты
bool PlayerDefend = false;


Random rnd = new Random();
Console.WriteLine("===1-ЫЙ БОЙ ===");
Console.WriteLine();
Console.WriteLine("=== БОЙ НАЧАЛСЯ ===");


// Цикл боя
// Сражение идет, пока живы и Игрок вражина
while (currentHP > 0 && currentMercHP > 0)
{

    PlayerDefend = false;

    // Интерфейс тут
    // Здоровье игрока
    int scaleLengthHP = 10;
    int filledCellsHP = currentHP * scaleLengthHP / maxHP;
    int emptyCellsHP = scaleLengthHP - filledCellsHP;
    Console.Write("Здоровье: [");
    for (int i = 0; i < filledCellsHP; i++) Console.Write("#");
    for (int i = 0; i < emptyCellsHP; i++) Console.Write("-");
    Console.WriteLine($"] ({currentHP}/{maxHP})");

    //Энергия игрока
    int scaleLengthE = 10;
    int filledCellsE = currentEnrg * scaleLengthE / maxEnrg;
    int emptyCellsE = scaleLengthE - filledCellsE;
    Console.Write("Энергия:  [");
    for (int i = 0; i < filledCellsE; i++) Console.Write("#");
    for (int i = 0; i < emptyCellsE; i++) Console.Write("-");
    Console.WriteLine($"] ({currentEnrg}/{maxEnrg})");

    // Хил
    int scaleLengthHeal = 3;
    int filledCellsHC = currentHealCount * scaleLengthHeal / maxHealCount;
    int emptyCellsHC = scaleLengthHeal - filledCellsHC;
    Console.Write("ДЫХАНИЕ ЖИЗНИ: [");
    for (int i = 0; i < filledCellsHC; i++) Console.Write("#");
    for (int i = 0; i < emptyCellsHC; i++) Console.Write("-");
    Console.WriteLine($"] ({currentHealCount}/{maxHealCount})");

    // Энерджайзер
    int scaleLengthEnergizer = 3;
    int filledCellsEn = currentEnergizer * scaleLengthEnergizer / maxEnergizer;
    int emptyCellsEn = scaleLengthEnergizer - filledCellsEn;
    Console.Write("КОНЦЕНТРАЦИЯ ЭНЕРГИИ: [");
    for (int i = 0; i < filledCellsEn; i++) Console.Write("#");
    for (int i = 0; i < emptyCellsEn; i++) Console.Write("-");
    Console.WriteLine($"] ({currentEnergizer}/{maxEnergizer})");

    Console.WriteLine("---------------------------------------------");

    //Здоровье
    int MercFilledCellsHP = currentMercHP * scaleLengthE / maxMercHP;
    int MercEmptyCellsHP = scaleLengthE - MercFilledCellsHP;
    Console.Write("Наёмник из банды: [");
    for (int i = 0; i < MercFilledCellsHP; i++) Console.Write("#");
    for (int i = 0; i < MercEmptyCellsHP; i++) Console.Write("-");
    Console.WriteLine($"] ({Math.Max(0, currentMercHP)}/{maxMercHP})");

    //Энергия врага
    int MercFilledCellsE2 = currentMercE * scaleLengthE / maxMercE;
    int MercEmptyCellsE2 = scaleLengthE - MercFilledCellsE2;
    Console.Write("Энергия Наёмника: [");
    for (int i = 0; i < MercFilledCellsE2; i++) Console.Write("#");
    for (int i = 0; i < MercEmptyCellsE2; i++) Console.Write("-");
    Console.WriteLine($"] ({currentMercE}/{maxMercE})");

    Console.WriteLine();

    //Выбор действий тут
    int userChoice = 0;
    do
    {
        Console.WriteLine("ВЫБЕРИТЕ ДЕЙСТВИЕ:");
        Console.WriteLine("1. АТАКА");
        Console.WriteLine("2. СПЕЦ. АТАКА (требует 50 энергии)");
        Console.WriteLine("3. ЗАЩИТА");
        Console.WriteLine("4. ДЫХАНИЕ ЖИЗНИ");
        Console.WriteLine("5. КОНЦЕНТРАЦИЯ ДУХА");

        string? input = Console.ReadLine();
        if (int.TryParse(input, out userChoice))
        {
            if (userChoice >= 1 && userChoice <= 5)
            {
                if (userChoice == 2 && currentEnrg < 50)
                {
                    Console.WriteLine("Недостаточно энергии!\n");
                    userChoice = 0;
                }
                else if (userChoice == 4 && currentHealCount <= 0)
                {
                    Console.WriteLine("Закончились расходники!\n");
                    userChoice = 0;
                }
                else if (userChoice == 5 && currentEnergizer <= 0)
                {
                    Console.WriteLine("Закончились расходники!\n");
                    userChoice = 0;
                }
            }
            else
            {
                Console.WriteLine("Не вариант!\n");
            }
        }
        else
        {
            Console.WriteLine("Не вариант!\n");
        }
    } while (userChoice == 0);


    //Действие
    Console.WriteLine();
    if (userChoice == 1)
    {
        int playerDamage = rnd.Next(12, 22);
        currentMercHP -= playerDamage;
        Console.WriteLine($"Игрок нанес {playerDamage} урона.");
    }
    else if (userChoice == 2)
    {
        currentEnrg -= 50;
        int Ultimate = rnd.Next(35, 50);
        currentMercHP -= Ultimate;
        Console.WriteLine($"Ронин использует спец. атаку и наносит {Ultimate} урона!");
    }
    else if (userChoice == 3)
    {
        PlayerDefend = true;
        Console.WriteLine("Ронин встал в оборонительную стойку. Урон будет снижен!");
    }
    else if (userChoice == 4)
    {
        currentHealCount--;
        currentHP = Math.Min(maxHP, currentHP + 30);
        Console.WriteLine("Вы использовали Дыхание жизни и восстановили здоровье.");
    }
    else if (userChoice == 5)
    {
        currentEnergizer--;
        currentEnrg = Math.Min(maxEnrg, currentEnrg + 40);
        Console.WriteLine("Вы использовали Концентрацию духа и восстановили энергию.");
    }





    if (currentMercHP <= 0)
    {
        Console.WriteLine("\nНаёмник из банды повержен!");

        break;
    }

    //Ответка
    int enemyDamage = rnd.Next(8, 16);

    if (PlayerDefend)
    {
        enemyDamage /= 2;
        Console.WriteLine("Благодаря защите вы заблокировали часть урона!");
    }

    currentHP -= enemyDamage;
    Console.WriteLine($"Наёмник нанес вам {enemyDamage} урона.");


    currentEnrg = Math.Min(maxEnrg, currentEnrg + 10);



}

//финал первого боя
if (currentHP <= 0)
{
    Console.WriteLine("Поражение! Ронин погиб в бою.");
}
else
{
    Console.WriteLine("Победа!");
}

Console.WriteLine("Перед следующим боем Ронин отдахнул и набрался сил");
currentHealCount--;
currentHP = Math.Min(maxHP, currentHP + 30);

Console.WriteLine("---------------------------------------------");
Console.WriteLine("===2-ЫЙ БОЙ ===");
Console.WriteLine();
Console.WriteLine("=== БОЙ НАЧАЛСЯ ===");

while (currentHP > 0 && currentNjHp > 0)
{

    PlayerDefend = false;

    int scaleLengthHP2 = 10;
    int filledCellsHP2 = currentHP * scaleLengthHP2 / maxHP;
    int emptyCellsHP2 = scaleLengthHP2 - filledCellsHP2;
    Console.Write("Здоровье: [");
    for (int i = 0; i < filledCellsHP2; i++) Console.Write("#");
    for (int i = 0; i < emptyCellsHP2; i++) Console.Write("-");
    Console.WriteLine($"] ({currentHP}/{maxHP})");

    int scaleLengthE2 = 10;
    int filledCellsE2 = currentEnrg * scaleLengthE2 / maxEnrg;
    int emptyCellsE2 = scaleLengthE2 - filledCellsE2;
    Console.Write("Энергия:  [");
    for (int i = 0; i < filledCellsE2; i++) Console.Write("#");
    for (int i = 0; i < emptyCellsE2; i++) Console.Write("-");
    Console.WriteLine($"] ({currentEnrg}/{maxEnrg})");

    int scaleLengthHeal2 = 3;
    int filledCellsHC2 = currentHealCount * scaleLengthHeal2 / maxHealCount;
    int emptyCellsHC2 = scaleLengthHeal2 - filledCellsHC2;
    Console.Write("ДЫХАНИЕ ЖИЗНИ: [");
    for (int i = 0; i < filledCellsHC2; i++) Console.Write("#");
    for (int i = 0; i < emptyCellsHC2; i++) Console.Write("-");
    Console.WriteLine($"] ({currentHealCount}/{maxHealCount})");

    int scaleLengthEnergizer2 = 3;
    int filledCellsEn2 = currentEnergizer * scaleLengthEnergizer2 / maxEnergizer;
    int emptyCellsEn2 = scaleLengthEnergizer2 - filledCellsEn2;
    Console.Write("КОНЦЕНТРАЦИЯ ЭНЕРГИИ: [");
    for (int i = 0; i < filledCellsEn2; i++) Console.Write("#");
    for (int i = 0; i < emptyCellsEn2; i++) Console.Write("-");
    Console.WriteLine($"] ({currentEnergizer}/{maxEnergizer})");

    Console.WriteLine("---------------------------------------------");

    int NjFilledCellsHP = currentNjHp * scaleLengthE2 / maxNjHP;
    int NjEmptyCellsHP = scaleLengthE2 - NjFilledCellsHP;
    Console.Write("Ниндзя клана: [");
    for (int i = 0; i < NjFilledCellsHP; i++) Console.Write("#");
    for (int i = 0; i < NjEmptyCellsHP; i++) Console.Write("-");
    Console.WriteLine($"] ({Math.Max(0, currentNjHp)}/{maxNjHP})");

    //Энергия врага
    int NjFilledCellsE = currentNjE * scaleLengthE2 / maxNjE;
    int NjEmptyCellsE = scaleLengthE2 - NjFilledCellsE;
    Console.Write("Энергия Ниндзя: [");
    for (int i = 0; i < NjFilledCellsE; i++) Console.Write("#");
    for (int i = 0; i < NjEmptyCellsE; i++) Console.Write("-");
    Console.WriteLine($"] ({currentNjE}/{maxNjE})");

    Console.WriteLine();

    //Выбор действий тут
    int userChoice2 = 0;
    do
    {
        Console.WriteLine("ВЫБЕРИТЕ ДЕЙСТВИЕ:");
        Console.WriteLine("1. АТАКА");
        Console.WriteLine("2. СПЕЦ. АТАКА (требует 50 энергии)");
        Console.WriteLine("3. ЗАЩИТА");
        Console.WriteLine("4. ДЫХАНИЕ ЖИЗНИ");
        Console.WriteLine("5. КОНЦЕНТРАЦИЯ ДУХА");

        string? input = Console.ReadLine();
        if (int.TryParse(input, out userChoice2))
        {
            if (userChoice2 >= 1 && userChoice2 <= 5)
            {
                if (userChoice2 == 2 && currentEnrg < 50)
                {
                    Console.WriteLine("Недостаточно энергии!\n");
                    userChoice2 = 0;
                }
                else if (userChoice2 == 4 && currentHealCount <= 0)
                {
                    Console.WriteLine("Закончились расходники!\n");
                    userChoice2 = 0;
                }
                else if (userChoice2 == 5 && currentEnergizer <= 0)
                {
                    Console.WriteLine("Закончились расходники!\n");
                    userChoice2 = 0;
                }
            }
            else
            {
                Console.WriteLine("Не вариант!\n");
            }
        }
        else
        {
            Console.WriteLine("Не вариант!\n");
        }
    } while (userChoice2 == 0);

    //Действие
    Console.WriteLine();
    if (userChoice2 == 1)
    {
        int playerDamage = rnd.Next(12, 22);
        currentNjHp -= playerDamage;
        Console.WriteLine($"Игрок нанес {playerDamage} урона.");
    }
    else if (userChoice2 == 2)
    {
        currentEnrg -= 50;
        int Ultimate = rnd.Next(35, 50);
        currentNjHp -= Ultimate;
        Console.WriteLine($"Ронин использует спец. атаку и наносит {Ultimate} урона!");
    }
    else if (userChoice2 == 3)
    {
        PlayerDefend = true;
        Console.WriteLine("Ронин встал в оборонительную стойку. Урон будет снижен!");
    }
    else if (userChoice2 == 4)
    {
        currentHealCount--;
        currentHP = Math.Min(maxHP, currentHP + 30);
        Console.WriteLine("Вы использовали Дыхание жизни и восстановили здоровье.");
    }
    else if (userChoice2 == 5)
    {
        currentEnergizer--;
        currentEnrg = Math.Min(maxEnrg, currentEnrg + 40);
        Console.WriteLine("Вы использовали Концентрацию духа и восстановили энергию.");
    }
    if (currentNjHp <= 0)
    {
        Console.WriteLine("\nНиндзя клана повержен!");

        break;
    }

    //Ответка
    int enemyDamage = rnd.Next(8, 16);

    if (PlayerDefend)
    {
        enemyDamage /= 2;
        Console.WriteLine("Благодаря защите вы заблокировали часть урона!");
    }

    currentHP -= enemyDamage;
    Console.WriteLine($"Ниндзя нанес вам {enemyDamage} урона.");


    currentEnrg = Math.Min(maxEnrg, currentEnrg + 10);



}
if (currentHP <= 0)
{
    Console.WriteLine("Поражение! Ронин погиб в бою.");
}
else
{
    Console.WriteLine("Победа!");
}
Console.WriteLine("Перед следующим боем Ронин отдахнул и набрался сил");
currentHealCount--;
currentHP = Math.Min(maxHP, currentHP + 30);

Console.WriteLine("---------------------------------------------");
Console.WriteLine("===ФИНАЛЬНЫЙ БОЙ ===");
Console.WriteLine();
Console.WriteLine("=== БОЙ НАЧАЛСЯ ===");

while (currentHP > 0 && currentMsHP > 0)
{

    PlayerDefend = false;

    int scaleLengthHP2 = 10;
    int filledCellsHP2 = currentHP * scaleLengthHP2 / maxHP;
    int emptyCellsHP2 = scaleLengthHP2 - filledCellsHP2;
    Console.Write("Здоровье: [");
    for (int i = 0; i < filledCellsHP2; i++) Console.Write("#");
    for (int i = 0; i < emptyCellsHP2; i++) Console.Write("-");
    Console.WriteLine($"] ({currentHP}/{maxHP})");

    int scaleLengthE2 = 10;
    int filledCellsE2 = currentEnrg * scaleLengthE2 / maxEnrg;
    int emptyCellsE2 = scaleLengthE2 - filledCellsE2;
    Console.Write("Энергия:  [");
    for (int i = 0; i < filledCellsE2; i++) Console.Write("#");
    for (int i = 0; i < emptyCellsE2; i++) Console.Write("-");
    Console.WriteLine($"] ({currentEnrg}/{maxEnrg})");

    int scaleLengthHeal2 = 3;
    int filledCellsHC2 = currentHealCount * scaleLengthHeal2 / maxHealCount;
    int emptyCellsHC2 = scaleLengthHeal2 - filledCellsHC2;
    Console.Write("ДЫХАНИЕ ЖИЗНИ: [");
    for (int i = 0; i < filledCellsHC2; i++) Console.Write("#");
    for (int i = 0; i < emptyCellsHC2; i++) Console.Write("-");
    Console.WriteLine($"] ({currentHealCount}/{maxHealCount})");

    int scaleLengthEnergizer2 = 3;
    int filledCellsEn2 = currentEnergizer * scaleLengthEnergizer2 / maxEnergizer;
    int emptyCellsEn2 = scaleLengthEnergizer2 - filledCellsEn2;
    Console.Write("КОНЦЕНТРАЦИЯ ЭНЕРГИИ: [");
    for (int i = 0; i < filledCellsEn2; i++) Console.Write("#");
    for (int i = 0; i < emptyCellsEn2; i++) Console.Write("-");
    Console.WriteLine($"] ({currentEnergizer}/{maxEnergizer})");

    Console.WriteLine("---------------------------------------------");

    int MsFilledCellsHP = currentMsHP * scaleLengthE2 / MaxMsHP;
    int MsEmptyCellsHP = scaleLengthE2 - MsFilledCellsHP;
    Console.Write("Мастер меча: [");
    for (int i = 0; i < MsFilledCellsHP; i++) Console.Write("#");
    for (int i = 0; i < MsEmptyCellsHP; i++) Console.Write("-");
    Console.WriteLine($"] ({Math.Max(0, currentMsHP)}/{MaxMsHP})");

    //Энергия врага
    int MsFilledCellsE = currentMsE * scaleLengthE2 / maxMsE;
    int MsEmptyCellsE = scaleLengthE2 - MsFilledCellsE;
    Console.Write("Энергия Ниндзя: [");
    for (int i = 0; i < MsFilledCellsE; i++) Console.Write("#");
    for (int i = 0; i < MsEmptyCellsE; i++) Console.Write("-");
    Console.WriteLine($"] ({currentMsE}/{maxMsE})");

    Console.WriteLine();

    //Выбор действий тут
    int userChoice2 = 0;
    do
    {
        Console.WriteLine("ВЫБЕРИТЕ ДЕЙСТВИЕ:");
        Console.WriteLine("1. АТАКА");
        Console.WriteLine("2. СПЕЦ. АТАКА (требует 50 энергии)");
        Console.WriteLine("3. ЗАЩИТА");
        Console.WriteLine("4. ДЫХАНИЕ ЖИЗНИ");
        Console.WriteLine("5. КОНЦЕНТРАЦИЯ ДУХА");

        string? input = Console.ReadLine();
        if (int.TryParse(input, out userChoice2))
        {
            if (userChoice2 >= 1 && userChoice2 <= 5)
            {
                if (userChoice2 == 2 && currentEnrg < 50)
                {
                    Console.WriteLine("Недостаточно энергии!\n");
                    userChoice2 = 0;
                }
                else if (userChoice2 == 4 && currentHealCount <= 0)
                {
                    Console.WriteLine("Закончились расходники!\n");
                    userChoice2 = 0;
                }
                else if (userChoice2 == 5 && currentEnergizer <= 0)
                {
                    Console.WriteLine("Закончились расходники!\n");
                    userChoice2 = 0;
                }
            }
            else
            {
                Console.WriteLine("Не вариант!\n");
            }
        }
        else
        {
            Console.WriteLine("Не вариант!\n");
        }
    } while (userChoice2 == 0);

    //Действие
    Console.WriteLine();
    if (userChoice2 == 1)
    {
        int playerDamage = rnd.Next(12, 22);
        currentMsHP -= playerDamage;
        Console.WriteLine($"Игрок нанес {playerDamage} урона.");
    }
    else if (userChoice2 == 2)
    {
        currentEnrg -= 50;
        int Ultimate = rnd.Next(35, 50);
        currentMsHP -= Ultimate;
        Console.WriteLine($"Ронин использует спец. атаку и наносит {Ultimate} урона!");
    }
    else if (userChoice2 == 3)
    {
        PlayerDefend = true;
        Console.WriteLine("Ронин встал в оборонительную стойку. Урон будет снижен!");
    }
    else if (userChoice2 == 4)
    {
        currentHealCount--;
        currentHP = Math.Min(maxHP, currentHP + 30);
        Console.WriteLine("Вы использовали Дыхание жизни и восстановили здоровье.");
    }
    else if (userChoice2 == 5)
    {
        currentEnergizer--;
        currentEnrg = Math.Min(maxEnrg, currentEnrg + 40);
        Console.WriteLine("Вы использовали Концентрацию духа и восстановили энергию.");
    }
    if (currentMsHP <= 0)
    {
        Console.WriteLine("\nМастер меча повержен!");

        break;
    }

    //Ответка
    int enemyDamage = rnd.Next(8, 16);

    if (PlayerDefend)
    {
        enemyDamage /= 2;
        Console.WriteLine("Благодаря защите вы заблокировали часть урона!");
    }

    currentHP -= enemyDamage;
    Console.WriteLine($"Мечник нанес вам {enemyDamage} урона.");


    currentEnrg = Math.Min(maxEnrg, currentEnrg + 10);



}
if (currentHP <= 0)
{
    Console.WriteLine("Поражение! Ронин погиб в бою.");
}
else
{
    Console.WriteLine("Победа! Игра пройдена!");
}
```
---
```
<picture>
  <img src="https://github.com/v1skarr/practic-5/blob/main/ConsoleRPG2/1.png.png">
</picture>
<picture>
  <img src="https://github.com/v1skarr/practic-5/blob/main/ConsoleRPG2/2.png.png">
</picture>
<picture>
  <img src="https://github.com/v1skarr/practic-5/blob/main/ConsoleRPG2/3.png.png">
</picture>
<picture>
  <img src="https://github.com/v1skarr/practic-5/blob/main/ConsoleRPG2/4.png.png">
</picture>
<picture>
  <img src="https://github.com/v1skarr/practic-5/blob/main/ConsoleRPG2/5.png.png">
</picture>
<picture>
  <img src="https://github.com/v1skarr/practic-5/blob/main/ConsoleRPG2/6.png.png">
</picture>
<picture>
  <img src="https://github.com/v1skarr/practic-5/blob/main/ConsoleRPG2/7.png.png">
</picture>
<picture>
  <img src="https://github.com/v1skarr/practic-5/blob/main/ConsoleRPG2/8.png.png">
</picture>
<picture>
  <img src="https://github.com/v1skarr/practic-5/blob/main/ConsoleRPG2/9.png.png">
</picture>
<picture>
  <img src="https://github.com/v1skarr/practic-5/blob/main/ConsoleRPG2/10.png.png">
</picture>