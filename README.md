# КВ_2 Вывод дерева иерархии объектов
Для обработки определенного множества вершин древовидного графа, используется рекурсивный алгоритм обхода. Будем использовать версию данного алгоритма, которая работает от заданной вершины графа. В таком случае, алгоритм обойдет вершины ветки древовидного графа от заданной вершины. Если заданная вершина корневая, то алгоритм обойдет все вершины графа. Приведем шаблон кода реализации метода, который реализует данный алгоритм относительно текущего объекта:
```cpp
void cl_base::tree_traversal()
{
    // фрагмент кода обработки очередного объекта
    . . . . .
    for (auto p_subordinate_object : subordinate_objects)   // цикл по подчиненным объектам
    {
        p_subordinate_object->tree_traversal();             // рекурсивный вызов
    }
}
```

Естественно, в зависимости от назначения обхода, у метода могут быть параметры. Используя этот шаблон можно реализовать метод вывода дерева иерархии объектов, обозначив вложенность посредством сдвигов наименований объектов.

Пример вывода на консоль дерева иерархии объектов.
```
root
    ob_1
        ob_2
    ob_3
        ob_4
            ob_5
        ob_6
            ob_7
```

Для анализа текущей иерархической структуры системы в целом или определенной ветки, необходимо иметь возможность его отображения (распечатки, вывода на экран) в форме приемлемой для простой интерпретации.

Для анализа состояния системы и ее элементов, необходимо иметь возможность вывести эту информацию (распечатать, вывести на экран) в форме приемлемой для простой интерпретации.

## Постановка задачи
Первоначальная сборка системы (дерева иерархии объектов, модели системы) осуществляется исходя из входных данных. Данные вводятся построчно. Первая строка содержит имя корневого объекта (объект приложение). Номер класса корневого объекта 1. Далее, каждая строка входных данных определяет очередной объект, задает его характеристики и расположение на дереве иерархии. Структура данных в строке:
> «Наименование головного объекта» «Наименование очередного объекта» «Номер класса принадлежности очередного объекта»

Ввод иерархического дерева завершается, если наименование головного объекта равно «endtree» (в данной строке ввода больше ничего не указывается).

Поиск головного объекта выполняется от последнего созданного объекта. Первоначально последним созданным объектом считается корневой объект. Если для головного объекта обнаруживается дубляж имени в непосредственно подчиненных объектах, то объект не создается. Если обнаруживается дубляж имени на дереве иерархии объектов, то объект не создается. Если номер класса объекта задан некорректно, то объект не создается.

## Вывод иерархического дерева объектов на консоль.

Внутренняя архитектура (вид иерархического дерева объектов) в большинстве реализованных моделях систем динамически меняется в процессе отработки алгоритма. Вывод текущего дерева объектов является важной задачей, существенно помогая разработчику, особенно на этапе тестирования и отладки программы.

В данной задаче подразумевается, что наименования объектов уникальны. Система содержит объекты пяти классов, не считая корневого. Номера классов: 2, 3, 4, 5, 6.

Расширить функциональность базового класса:
+ метод поиска объекта на ветке дереве иерархии от текущего по имени (метод возвращает указатель на найденный объект или nullptr). Передается один параметр строкового типа, содержит наименование искомого объекта. Если на искомой ветке дерева иерархии наименование объекта не уникально или отсутствует, то возвращает nullptr;
+ метод поиска объекта на дереве иерархии по имени (метод возвращает указатель на найденный объект или nullptr). Передается один параметр строкового типа, содержит наименование искомого объекта. Если на дерева иерархии наименование объекта не уникально или отсутствует, то возвращает nullptr;
+ метод вывода иерархии объектов (дерева или ветки) от текущего объекта;
+ метод вывода иерархии объектов (дерева или ветки) и отметок их готовности от текущего объекта;
+ метод установки готовности объекта, в качестве параметра передается переменная целого типа, содержит номер состояния.

Готовность для каждого объекта устанавливается индивидуально. Готовность задается посредством любого отличного от нуля целого числового значения, которое присваивается свойству состояния объекта. Объект переводится в состояние готовности, если все объекты вверх по иерархии до корневого включены, иначе установка готовности игнорируется. При отключении головного, отключаются все объекты от него по иерархии вниз по ветке. Свойству состояния объекта присваивается значение нуль.

Разработать программу:
1. Построить дерево объектов системы (в методе корневого объекта построения исходного дерева объектов).
2. В методе корневого объекта запуска моделируемой системы реализовать:
  2.1. Вывод на консоль иерархического дерева объектов в следующем виде:
```
root
    ob_1
        ob_2
    ob_3
        ob_4
            ob_5
        ob_6
            ob_7
```
  где: root - наименование корневого объекта (приложения).

  2.2 Переключение готовности объектов согласно входным данным (командам).
  2.3 Вывод на консоль иерархического дерева объектов и отметок их готовности в следующем виде:
```
root  is ready
    ob_1  is ready
        ob_2  is ready
    ob_3  is ready
        ob_4 is not ready
            ob_5 is not ready
        ob_6 is ready
            ob_7 is not ready
```

_При решении задачи необходимо руководствоваться методическим пособием и приложением к методическому пособию_

## Входные данные
Множество объектов, их характеристики и расположение на дереве иерархии. Последовательность ввода организовано так, что головной объект для очередного вводимого объекта уже присутствует на дереве иерархии объектов.

Первая строка:
> «Наименование корневого объекта»

Со второй строки:
> «Наименование головного объекта» «Наименование очередного объекта» «Номер класса принадлежности очередного объекта»\
. . . . .\
endtree

Со следующей строки вводятся команды включения или отключения объектов
> «Наименование объекта» «Номер состояния объекта»

Пример ввода:
```
app_root
app_root object_01 3
app_root object_02 2
object_02 object_04 3
object_02 object_05 5
object_01 object_07 2
endtree
app_root 1
object_07 3
object_01 1
object_02 -2
object_04 1
```

## Выходные данные
Вывести иерархию объектов в следующем виде:
```
Object tree
«Наименование корневого объекта»
    «Наименование объекта 1»
        «Наименование объекта 2»
    «Наименование объекта 3»
. . . . .
The tree of objects and their readiness
«Наименование корневого объекта» «Отметка готовности»
    «Наименование объекта 1» «Отметка готовности»
        «Наименование объекта 2» «Отметка готовности»
    «Наименование объекта 3» «Отметка готовности»
. . . . .
«Отметка готовности» - равно «is ready» или «is not ready»
```
Отступ каждого уровня иерархии 4 позиции.

Пример вывода:
```
Object tree
app_root
    object_01
        object_07
    object_02
        object_04
        object_05
The tree of objects and their readiness
app_root is ready
    object_01 is ready
        object_07 is not ready
    object_02 is ready
        object_04 is ready
        object_05 is not ready
```
---
### Автор - https://vk.com/aptekkkar 
   + Прямой путь по ID: https://vk.com/id169607065
