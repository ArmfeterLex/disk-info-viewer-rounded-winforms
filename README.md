# Disk Info Viewer Rounded WinForms

Программа для просмотра информации о дисках Windows с нестандартным интерфейсом.

<img width="471" height="513" alt="Снимок экрана 2026-03-01 144632" src="https://github.com/user-attachments/assets/f81e8842-d44e-4f97-bb0d-65b954e18c71" />

## Функциональность

### 💾 Информация о дисках
- Получение списка всех логических дисков (два способа: Directory.GetLogicalDrives и Environment.GetLogicalDrives)
- Детальная информация о диске C: (тип, файловая система, свободное место)
- Детальная информация о диске D: (тип, файловая система, свободное место)

### 🎨 Интерфейс
- Скругленные углы окна через GDI (CreateRoundRectRgn)
- Отсутствие стандартного заголовка окна (FormBorderStyle.None)
- Кастомные кнопки: закрыть (radioButton1), свернуть (radioButton2)
- Вывод информации в listBox1

## Интерфейс

- Кнопка "button1" — показать все диски (через Directory.GetLogicalDrives)
- Кнопка "button2" — показать все диски (через Environment.GetLogicalDrives)
- Кнопка "button3" — информация о диске C:
- Кнопка "button4" — информация о диске D:
- RadioButton1 — закрыть программу
- RadioButton2 — свернуть программу
- ListBox1 — вывод информации

## Куда можно встроить

- В системную утилиту для диагностики
- В программу очистки диска
- В файловый менеджер с кастомным интерфейсом
- Как пример работы с DriveInfo и скругленными окнами

## Требования

- Windows
- .NET Framework / .NET Core с WinForms

## Примечание

Для дисков D: и других сменных носителей проверяется свойство IsReady — информация выводится только если диск готов (вставлен). Скругление углов реализовано через CreateRoundRectRgn из Gdi32.dll.

## Примеры использования

```csharp
// Получить все логические диски
string[] drives = System.IO.Directory.GetLogicalDrives();

// Получить информацию о диске
System.IO.DriveInfo drv = new System.IO.DriveInfo(@"c:\");
if (drv.IsReady)
{
    string driveType = drv.DriveType.ToString();
    string driveFormat = drv.DriveFormat.ToString();
    long freeSpace = drv.AvailableFreeSpace;
}

// Создать окно со скругленными углами
this.FormBorderStyle = FormBorderStyle.None;
Region = Region.FromHrgn(CreateRoundRectRgn(0, 0, Width, Height, 20, 20));
