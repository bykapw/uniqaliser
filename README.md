Тестовая программа

Сравнение Файла1 с Файлом2, вывод строк, не входящих в Файл2.

Исходные данные:
- размер файлов порядка терабайта
- размер строки порядка килобайта
- строки в достаточной степени уникальны

Принцип работы: 
- сравнение хешей строк. Строки с одинаковым хешем считаем одинаковыми.

Алгоритм работы:
- Файл2 разбивается на несколько блоков, по N строк
- для каждого блока происходит расчет хешей и загрузка в память
- затем происходит прогон Файла1: строки, отсутствующие в обрабатываемом блоке, выводятся во временный файл
- загружается следующий блок, производится прогон ненайденных строк
- цикл повторяется, пока все строки Файла1 не будут прогнаны через все блоки Файла2, уникальные останутся в файле вывода.
- при благоприятных условиях (отсев найденных строк) скорость прогона с каждым циклом увеличивается

Обоснования:
- Прямое сравнение строк в виде вложенных циклов дает X = A * B операций чтения файла. 
При заданных размерах файлов это порядка 1024 ^ 6.
- Сравнение блоками позволяет существенно сократить количество операций чтения.
В идеальном случае X = A + B, в случае полной загрузки Файла2 в память, но тогда возрастают требования к памяти.
- Разбивка на блоки позволяет достигнуть компромисса, экономя память и снижая число операций.

Оценочное быстродействие:
- на имеющемся оборудовании время одной операции чтения составляет порядка 130 мкс,
- обработка пары полностью уникальных файлов размерами 10240 строк - порядка 0.67 сек.
- обработка пары полностью уникальных файлов размерами 102400 строк - порядка 14.4 сек.
- обработка пары полностью уникальных файлов размерами 1024 ^ 3 строк (около 1 Тб) при загрузке блоками по 200 млн. строк - оценочно 170 часов.
- дальнейшее увеличение числа строк в блоке ограничено объемом памяти, увеличение скорости обработки - временем дисковых операций.
- при благоприятных условиях и подходящем оборудовании время полной обработки будет существенно меньше.




