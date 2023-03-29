# Титульник

# Задания на практику

Цель: Изучить работу алгоритмов поиска и сортировки

Задачи:
- Изучить типы алгоритмов
- Исследовать алгоритм сортировки пузырьком
- Исследовать алгоритм сортировки деревом
- Исследовать алгоритм пирамидальной сортировки
- Исследовать алгоритм Кнута-Морриса-Паратта
- Исследовать алгоритм Боуера-Мура
- Исследовать алгоритм бинарного поиска  

# Оглавление

# Введение

# Теоретическая часть

# Алгоритмы сортировки

## Болотная сортировка (Bogosort) ИИ

Болотная сортировка - это алгоритм сортировки, который случайным образом переставляет элементы массива до тех пор, пока отсортированный массив не получится.

### Логика работы

1. Проверяем, отсортирован ли массив. Если да, то завершаем алгоритм.
2. Иначе перемешиваем элементы массива случайным образом.
3. Проверяем, отсортирован ли массив после перемешивания. Если да, то завершаем алгоритм, иначе повторяем шаги 2-3.


### Код алгоритма
```
function Bogosort(arr){
    var isSorted = function(arr){
        for(var i = 1; i < arr.length; i++){
            if (arr[i-1] > arr[i]) {
                return false;
            }
        }
        return true;
    };

    function shuffle(arr){
        var count = arr.length, temp, index;

        while(count > 0){
            index = Math.floor(Math.random() * count);
            count--;

            temp = arr[count];
            arr[count] = arr[index];
            arr[index] = temp;
        }

        return arr;
    }

   function sort(arr){
        var sorted = false;
        while(!sorted){
            arr = shuffle(arr);
            sorted = isSorted(arr);
        }
        return arr;
    }

    return sort(arr);
}

```



### Плюсы и минусы

Плюсы:
- Простота реализации
- Может быть использован для проверки других алгоритмов сортировки, так как он всегда останавливается, когда массив отсортирован.

Минусы:
- Неэффективен и может работать очень долго для больших массивов.
- Шансы получить отсортированный массив случайным образом крайне малы, поэтому алгоритм не гарантирует быструю сортировку.
- Непредсказуемость времени выполнения.

### Источники
- [Wikipedia](https://en.wikipedia.org/wiki/Bogosort)
- https://w3resource.com/javascript-exercises/searching-and-sorting-algorithm/searching-and-sorting-algorithm-exercise-14.php

Сортировка пузырьком — элементарный алгоритм
сортировки, который сравнивает
и меняет соседние элементы
массива до тех пор, пока все
элементы не будут отсортированы.

### Логика работы

1. Стартуем от первого элемента массива и сравниваем его с его соседом справа.
2. Если первый элемент больше второго, меняем элементы местами.
3. Двигаемся на следующую пару элементов и продолжаем сравнивать и менять местами элементы, если это необходимо.
4. Продолжаем выполнять шаги 1-3 до тех пор, пока все элементы не будут отсортированы в порядке возрастания.

### Плюсы и минусы

Плюсы:
- Простота реализации
- Разумное время работы для небольших массивов

Минусы:
- Очень медленный для больших массивов данных
- Элементы на концах массива могут перемещаться медленно, даже если они уже отсортированы.

### Источники
- [Wikipedia](https://en.wikipedia.org/wiki/Bubble_sort)
- [GeeksforGeeks](https://www.geeksforgeeks.org/bubble-sort/)

<!## Сортировка деревом (Tree Sort) ИИ

Дерево - это структура данных, которая состоит из корня и ноль или более поддеревьев, каждое из которых также является деревом. Сортировка деревом использует бинарное дерево для сортировки элементов.

### Логика работы

1. Создаем пустое бинарное дерево.
2. Вставляем каждый элемент списка в бинарное дерево.
3. Производим обход дерева (ин-ордер или симметричный обход) и записываем элементы в исходный список в отсортированном порядке.

### Плюсы и минусы

Плюсы
- Сортировка деревом имеет линейную сложность O(nlogn).
- Эффективна для сортировки больших массивов данных.
- Не требует дополнительного пространства, кроме дополнительного пространства, необходимого для создания дерева.

Минусы

- Может быть неэффективна для небольших массивов данных.
- Для сбалансированного бинарного дерева эффективность алгоритма будет лучше, однако создание сбалансированного дерева может быть сложным и занимать больше времени.
- Относительно более сложный алгоритм, чем, например, Bubble Sort или Selection Sort.

### Источники

- Cormen, T.H., Leiserson, C.E., Rivest, R.L., & Stein, C. (2009). Introduction to Algorithms (3rd ed.). MIT Press.
- GeeksforGeeks. (2021). Tree Sort. Retrieved June 19, 2021, from https://www.geeksforgeeks.org/tree-sort/

## Пирамидальная сортировка ИИ

Пирамидальная сортировка - это алгоритм сортировки данных, который использует структуру данных в виде пирамиды, чтобы эффективно находить наибольшее (или наименьшее) значение массива/списка и переставлять его в начало (или конец) списка. 

### Логика работы
1. Построение двоичной кучи из исходного массива данных. Таким образом, мы получаем структуру данных, где для каждого узла выполняется условие $a[i]<=a[2*i] \&\& a[i]<=a[2*i+1]$ (для сортировки по возрастанию, либо наоборот: для сортировки по убыванию)
2. Максимальный элемент в корне кучи. Меняем местами корневой элемент с последним справа в подмассиве.
3. Сокращение диапазона массива на 1, исключая отсортированные элементы, и перестройка кучи (свап корневой вершины с наибольшим из листьев поддерева). Поэтому возникает необходимость восстановления структуры пирамиды (Heapify).
4. Повторяем шаги 2-3, пока диапазон не станет 1.



### Код алгоритма
```

// recursive

function pyramid(n, row = 0, level = '#') {
    if (n === row) {
        return;
    }

    if (level.length === 2 * n - 1) {
        console.log(level);
        return pyramid(n, row + 1);
    }

    level = level.length < 2 * row ? `#${level}#` : ` ${level} `;
    pyramid(n, row, level);
}



// iterative

function pyramid(n) {
    const columnCount = 2 * n - 1;
    const midColumn = Math.floor(columnCount / 2);

    for (let row = 0; row < n; row++) {
        let level = '';

        for (let column = 0; column < columnCount; column++) {
            if (Math.abs(column - midColumn) <= row) {
                level += '#';
            } else {
                level += ' ';
            }
        }

        console.log(level);
    }
}

```




### Плюсы и минусы

Плюсы:
- Эффективен на больших массивах, так как время выполнения составляет $O(n log n)$.
- Имеет инструкцию по построению двоичной кучи, что приводит к дополнительному применению на практике.

Минусы:
- Из-за высокой константы времени выполнения, алгоритм может работать медленнее простых алгоритмов сортировки (например, сортировка вставками) для небольших массивов.
- Нет возможности параллельной обработки данных, так как каждый шаг зависит от предыдущего.

### Источники
- Cormen, T. H., Leiserson, C. E., Rivest, R. L., & Stein, C. (2009). Introduction to algorithms. MIT press.
- https://www.geeksforgeeks.org/heap-sort/
- https://dev.to/tommy3/learning-algorithms-with-js-python-and-java-10-pyramid-4mga



## Добавить еще какую нибудь сортировку

# Алгоритмы поиска

## Алгоритм Кнута-Морриса-Паратта (KMП) ИИ

КМП - это алгоритм поиска подстроки в строке, который был разработан Кнутом, Моррисом и Праттом в 1977 году. Этот алгоритм используется для поиска всех вхождений подстроки в строку и работает за время O(n + m), где n - длина строки, а m - длина подстроки.

### Логика работы

1. Строим массив префиксных значений (prefix function) для заданной подстроки.
2. Сравниваем символы в строке и подстроке, начиная с начала.
3. Если символы совпадают, то индексы обоих смещаются на следующий символ в строке и подстроке соответственно.
4. Если символы не совпадают, то мы используем prefix function, чтобы определить максимальное совпадающее префиксное значение подстроки, которое находится внутри текущего несовпадающего префикса подстроки.
5. Мы сдвигаем подстроку на это значение и продолжаем поиски с шага 2.


### Код алгоритма
```
/**
 * `indexOf` is an implementation of the Knuth-Morrison-Pratt
 * Algorithm for finding the index of a given subsequence
 * (identified as `word` here) within a sequence (identified as
 * `string` here). Thanks to JavaScript's dynamic nature it
 * works equally well with strings and arrays.
 */

module.exports = function indexOf(word, string) {
  'use strict';

  var m = 0;
  var i = 0;
  var table = [];

  var pos = 2;
  var cnd = 0;

  table[0] = -1;
  table[1] = 0;

  // build the table for KMP. This takes `O(word.length)` steps.
  while (pos < word.length) {
    if (word[pos - 1] == word[cnd]) {
      cnd = cnd + 1;
      table[pos] = cnd;
      pos = pos + 1;
    } else if (cnd > 0) {
      cnd = table[cnd];
    } else {
      table[pos] = 0;
      pos = pos + 1;
    }
  }
  
  // scan the string. This takes `O(string.length)` steps.
  while (m + i < string.length) {
    if (word[i] == string[m + i]) {
      if (i == word.length - 1) {
        return m;
      }
      i = i + 1;
    } else {
      if (table[i] > -1) {
        m = m + i - table[i];
        i = table[i];
      } else {
        i = 0;
        m = m + 1;
      }
    }
  }
  // Returns -1 if the subsequence was not found in the sequence.
  return -1;
};

```



### Плюсы и минусы

Плюсы:
1. Он является одним из самых быстрых алгоритмов поиска подстроки в строке.
2. Не использует дополнительную память для поиска, кроме массива префиксных значений.
3. Хорошо работает со всеми типами символов (цифрами, буквами, специальными символами).

Минусы:
1. Требует предобработки подстроки для создания массива префиксных значений.
2. Этот алгоритм может быть немного сложным для понимания и реализации.

### Источники

1. Источник: Кнут, Дональд Э. (1977), "Fast Pattern Matching in Strings", SIAM Journal on Computing, 6 (2): 323–350
2. Источник: Кормен, Томас Х. (2009), Introduction to Algorithms (3rd ed.), MIT Press and McGraw-Hill, стр. 923–925.

## Алгоритм Боуера-Мура (БМ) ИИ

BM-алгоритм, который был разработан в 1977 году Р. Боуером и Д. Муром, является алгоритмом поиска подстроки в строке. Он основан на использовании набора матриц, которые позволяют эффективно искать совпадения между подстрокой и строкой. 

### Логика работы

1. Создание таблицы смещений символов: в таблице для каждого символа определяется его смещение от последнего вхождения этого символа в подстроку (если встречается впервые, то считается, что он отсутствует полностью).

2. Сравнение строк: строки сравниваются справа налево, начиная с последнего символа. Определяется шаг смещения в зависимости от совпадений символов подстроки и строки. 

3. Поиск: если найдено совпадение, то производится начало строки (подстроки). 





### Код алгоритма
```
function boyerMooreAlgorithm(NO_OF_CHARS = 256, ) {
 
   // A utility function to get maximum of two integers
   function max (a,b)
   {
       return (a > b)? a: b;
   }
    
   // The preprocessing function for Boyer Moore's
   // bad character heuristic
   function badCharHeuristic(str,size,badchar)
   {
       // Initialize all occurrences as -1
         for (let i = 0; i < NO_OF_CHARS; i++)
              badchar[i] = -1;
     
         // Fill the actual value of last occurrence
         // of a character (indices of table are ascii and values are index of occurrence)
         for (i = 0; i < size; i++)
              badchar[ str[i].charCodeAt(0)] = i;
   }
    
   /* A pattern searching function that uses Bad
        Character Heuristic of Boyer Moore Algorithm */
   function search(txt,pat)
   {
       let m = pat.length;
         let n = txt.length;
     
         let badchar = new Array(NO_OF_CHARS);
     
         /* Fill the bad character array by calling
            the preprocessing function badCharHeuristic()
            for given pattern */
         badCharHeuristic(pat, m, badchar);
     
         let s = 0;  // s is shift of the pattern with
                     // respect to text
          // there are n-m+1 potential alignments
         while(s <= (n - m))
         {
             let j = m-1;
     
             /* Keep reducing index j of pattern while
                characters of pattern and text are
                matching at this shift s */
             while(j >= 0 && pat[j] == txt[s+j])
                 j--;
     
             /* If the pattern is present at current
                shift, then index j will become -1 after
                the above loop */
             if (j < 0)
             {
                 document.write("Patterns occur at shift = " + s);
     
                 /* Shift the pattern so that the next
                    character in text aligns with the last
                    occurrence of it in pattern.
                    The condition s+m < n is necessary for
                    the case when pattern occurs at the end
                    of text */
                 //txt[s+m] is character after the pattern in text
                 s += (s+m < n)? m-badchar[txt[s+m].charCodeAt(0)] : 1;
     
             }
     
             else
                 /* Shift the pattern so that the bad character
                    in text aligns with the last occurrence of
                    it in pattern. The max function is used to
                    make sure that we get a positive shift.
                    We may get a negative shift if the last
                    occurrence  of bad character in pattern
                    is on the right side of the current
                    character. */
                 s += max(1, j - badchar[txt[s+j].charCodeAt(0)]);
         }
   }
} // function boyerMooreAlgorithm



```






### Плюсы и минусы

Плюсы:
1. BM-алгоритм является одним из самых эффективных алгоритмов поиска подстроки в строке.

2. Алгоритм не перебирает все возможные варианты, а сразу проверяет только несколько вариантов, что позволяет сократить время выполнения.

3. В отличие от некоторых других алгоритмов, BM-алгоритм работает оптимально на данных случайного доступа.

Минусы:
1. BM-алгоритм не может быть использован в случаях, когда искомая подстрока исчерпывает всю входную строку. 

2. Алгоритм может работать неэффективно, если строка содержит много повторяющихся символов.

3. В случае, если подстрока преимущественно состоит из одного символа, то BM-алгоритм может работать неэффективно.

### Источники

1. Дональд Кнут, «Искусство программирования. Том 3: Сортировка и поиск», Вильямс, 2011.

2. Роберт Седжвик. Алгоритмы на Java. М.: «Издательский дом Вильямс», 2006. 

3. Р. Боуер, Д. Мур. «A New Algorithm for String Search». Communications of the ACM, 20(10): p. 762–772, October 1977.
4. https://www.geeksforgeeks.org/boyer-moore-algorithm-for-pattern-searching/

## Алгоритм поиска в глубину (DFS)

Алгоритм поиска в глубину используется для
обхода графа или дерева. Алгоритм начинает
обход из заданной вершины и продолжает обход в
глубину пока есть не посещенные вершины,
затем возвращается назад к предыдущей вершине и
продолжает так до тех пор, пока все вершины не будут посещены.

### Логика работы 
1. Создаем переменную, которая будет хранить информацию о посещенных вершинах. В начале все вершины помечаются как непосещенные.
2. Выбираем начальную вершину и помечаем ее как посещенную.
3. Для каждой смежной вершины, которая еще не была посещена, запускаем рекурсивную функцию поиска в глубину.
4. После обхода всех смежных вершин возвращаемся к предыдущей вершине и продолжаем поиск.

### Код алгоритма
```JavaScript
const dfs = (graph, start) => {
  let visited = []; // save a visited nodes 
  let needVisit = [];  // save a need-to-visit nodes

  needVisit.push(start);  // start search with start node

  // looping for need-to-visit list
  while(needVisit.length !== 0) {
    let node = needVisit.shift(); // take a nodes which in first position in array
    if(!visited.includes(node)){ // if this node is not visited,
      visited.push(node); // add to visited list (now visit)

      const tmp = (!graph[node] ? [] : graph[node]) 
      needVisit = [...tmp , ...needVisit] 
// dfs is depth first, So, nodes connected to this node has more high priority than original nodes in need-to-visit list
    }
  }
  return visited.join(' ');
}
```

### Особенности
- Может быть использован для решения задач на поиск пути, маршрута, связности и т.д.
- Если в графе есть закольцованный(зацикленный) путь это может вызывает зацыкливание самого алгоритма.

### Источники
- https://dev.to/phantolajang/dfsbfs-with-js-3652
- https://ru.wikipedia.org/wiki/Поиск_в_глубину



## Сравнение алгоритмов сортировки

## Сравнение работы алгоритмов поиска

# Заключение
После завершения учебной практики и выполнения работ, я выполнил следующие задачи:
- Изучил понятие «вычислительная сложность», познакомился с
  несколькими примерами наглядно выражающие понятие
  вычислительная сложность, познакомились с понятием
  «О большое» и его классами сложностей.
  
- Изучил алгоритмы сортировки пузырьком, деревом и пирамидальной сортировки
- Изучил алгоритмы поиска Кнута-Морриса-Паратта, Боуера-Мура и алгоритм бинарного поиска 



# Список источников

# Приложения
1. https://habr.com/ru/post/111449/
2. https://proglib.io/p/6-search-algorithms-java
3. https://medium.com/nuances-of-programming/алгоритмы-поиска-которые-должен-знать-каждый-специалист-по-обработке-и-анализу-данных-8ffb944850cc

## Ссылка на реп отчета

## Отчет на антиплагиат


<style>
    body > * {
        /* color: red */
        color: black;
        font: 14px 'Times New Roman'
    }

    /* h1 {
        border-bottom: red
    } */

    hr {
        border: red solid;
        /* display: none; */
    }

</style>