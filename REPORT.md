# Отчет по лабораторной работе №7

## Тема работы

Изучение систем управления пакетами на примере Hunter.

## Цель работы

Познакомиться с Hunter и заменить ручное подключение зависимости GoogleTest на
подключение через пакетный менеджер.

## Ход работы

### 1. Подготовка проекта

Сначала я использовала проект из лабораторной работы №6 и на его основе
создала отдельный репозиторий `lab07`.

Команды:

```bash
git clone https://github.com/kanadya07/lab06.git lab07
cd lab07
git remote remove origin
git remote add origin https://github.com/kanadya07/lab07.git
```

### 2. Подключение Hunter

Дальше была создана папка `cmake`, в которую был добавлен файл
`HunterGate.cmake`. После этого в основной `CMakeLists.txt` было добавлено
подключение Hunter.

```cmake
include("cmake/HunterGate.cmake")
HunterGate(
  URL "https://github.com/cpp-pm/hunter/archive/v0.23.251.tar.gz"
  SHA1 "5659b15dc0884d4b03dbd95710e6a1fa0fc3258d"
  LOCAL
)
```

### 3. Подключение GoogleTest через Hunter

В проекте было изменено подключение тестов. Вместо `FetchContent` теперь
используется Hunter.

```cmake
hunter_add_package(GTest)
find_package(GTest CONFIG REQUIRED)
```

После этого тестовое приложение `check` было связано с целями `GTest::main` и
`GTest::gmock`.

### 4. Выполнение домашнего задания

Для домашнего задания была добавлена локальная настройка Hunter-пакета:

```text
cmake/Hunter/config.cmake
```

В этом файле указана версия пакета `GTest`, которую должен использовать Hunter.

### 5. Добавление демонстрационного приложения

Также была добавлена папка `demo` с приложением `demo`. Программа читает текст
из стандартного ввода и записывает форматированный результат в файл, путь к
которому берется из переменной окружения `LOG_PATH`.

### 6. Проверка сборки

Для проверки проекта можно использовать команды:

```bash
cmake -S . -B _builds -DBUILD_TESTS=ON
cmake --build _builds
cmake --build _builds --target test
```

## Что находится в репозитории

1. `TASK.md`
2. `REPORT.md`
3. `cmake/HunterGate.cmake`
4. `cmake/Hunter/config.cmake`
5. `demo/main.cpp`
6. проект из предыдущих лабораторных работ

## Вывод

Во время выполнения этой лабораторной работы я познакомилась с Hunter и
увидела, как можно подключать внешние зависимости через пакетный менеджер.

## Ссылка на репозиторий

https://github.com/kanadya07/lab07
