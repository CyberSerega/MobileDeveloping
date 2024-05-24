<h1 align="center" paddin> МИНИСТЕРСТВО НАУКИ И ВЫСШЕГО ОБРАЗОВАНИЯ РОССИЙСКОЙ ФЕДЕРАЦИИ ФЕДЕРАЛЬНОЕ ГОСУДАРСТВЕННОЕ БЮДЖЕТНОЕ ОБРАЗОВАТЕЛЬНОЕ УЧРЕЖДЕНИЕ ВЫСШЕГО ОБРАЗОВАНИЯ «САХАЛИНСКИЙ ГОСУДАРСТВЕННЫЙ УНИВЕРСИТЕТ»</h1>

<p align="center"><strong>Лабораторная работа №7 "Макет" </strong></p>

<p align="right">Выполнил: Рогаль С. А.</p>
<p align="right">Проверил: Соболев Е. И.</p>

<p align="center">г. Южно-Сахалинск <br> 2024 год</p>

<h2 align="center">Введение</h2>
<p align="justify">Макет Android – это объект, который определяет визуальную структуру пользовательского интерфейса. То, как будет выглядеть утилита на дисплее задействованного устройства. Компоненты пользовательского интерфейса будут определяться в пределах выбранного макета относительно других элементов. К таковым составляющим относятся:
<ul>
  <li>тестовые поля;</li>
  <li>кнопки;</li>
  <li>маркеры;</li>
  <li>указатели;</li>
  <li>иные составляющие интерфейса.</li>
</ul>
Пользовательский интерфейс в Android может быть создан через XML-файлы, а также посредством Java-кода.<br>
Первый вариант более удобен – в нем представление контента будет храниться обособлено от итоговой кодификации управления поведением. За счет этого отладка и корректировка элементов на дисплее Android контента станет проще и безопаснее. XML-документы макетов размещаются в папке res/layout.</p>
<h2 align="center">Цели и задачи</h2>
<p><strong>Упражнение. Сделать функциональный макет</strong></p>
<p>Необходимо реализовать макет по изображению использую материалы из архива lab7.zip, соблюдая отступы согласно рисунку 1. </p>


<h2>Решение задач</h2>
<p>Добавили apiVersionTextView на макет, в класс MainActivity добавили аналогичную переменную. Кроме того, при запуске приложения (OnCreate) задаем текст для apiVersionTextView в виде уровня API устройства</p>

```kotlin
private lateinit var apiVersionTextView: TextView
apiVersionTextView.setText("API Version " + Build.VERSION.SDK)
```

<p>Для ограничения подсказок создали переменную-счетчик cheatsLeft, значение которой будет отображаться на макете в cheatsLeftTextView. При нажатии на кнопку вызова подсказки cheatButton их количество уменьшается. При отсутствии подсказок кнопка блокируется.</p>

```kotlin
private lateinit var cheatsLeftTextView: TextView
private var cheatsLeft = 3
cheatButton.setOnClickListener {
...
cheatsLeft-=1
if(cheatsLeft==0){
                cheatButton.isEnabled = false
            }
}
```

<h3>Задачи Codewars</h3>
<ul>
<li>Fix string case

  ```kotlin
object FixStringCase {
    
    fun solve(s: String): String {
        var countUpper = 0
        var countLower = 0
        for(symb in s){
            if(symb.isUpperCase()) countUpper+=1
            else countLower+=1
        }
        var res = ""
        if(countUpper>countLower){
            for(symb in s){
                if(symb.isLowerCase()) res+=symb.uppercase()
                else res+=symb
            }
        }        
        else{
            for(symb in s){
                if(symb.isUpperCase()) res+=symb.lowercase()
                else res+=symb
            }
        }
        return res
    }   
}
```

</li>
<li>Geometric Progression Sequence

  ```kotlin
fun geometricSequenceElements(a: Int, r: Int, n: Int): String{
    val myArray = Array(n, {1})
    myArray[0] = a
    for (i in 1..n-1){
        myArray[i]=myArray[i-1]*r
    }
    return myArray.joinToString(separator = ", ")  
}
```

</li>
<li>Count the Digit

  ```kotlin
package countdig

fun nbDig(n:Int, d:Int):Int {
    var res = 0
    for(k in 0..n){
        res+= (k*k).toString().count{ it.digitToInt()==d}
    }
    return res
}
```

</li>
<li>Sum of odd numbers

  ```kotlin
fun rowSumOddNumbers(n: Int): Int {
    var start = 1+(n-1)*(2+(n-1)*2)/2
    var sum = start
    for (i in 1..n-1){
        sum+=start+2*i
    }
    return sum
}
```

</li>
<li>Alphabet war

  ```kotlin
fun alphabetWar(fight: String): String {
   val leftSide: Map<Char, Int> = mapOf('w' to 4, 'p' to 3,'b' to 2,'s' to 1)
   val rightSide: Map<Char, Int> = mapOf('m' to 4, 'q' to 3,'d' to 2,'z' to 1)
   var leftSum = 0
   var rightSum = 0
   for (symb in fight.toList() ){
        if(leftSide.containsKey(symb)){
            leftSum+=leftSide[symb]!!.toInt()
        }
        else if(rightSide.containsKey(symb)){
            rightSum+=rightSide[symb]!!.toInt()
        }
   }
   if(leftSum<rightSum){
       return "Right side wins!"
   }
   else if(leftSum>rightSum){
       return "Left side wins!"
   }
   else return "Let's fight again!"
}
```

</li>
<li>The 'spiraling' box

  ```kotlin
import kotlin.math.*

fun createBox(width: Int, length: Int) = Array(length) {r -> 
    IntArray(width) { x -> 
        var row = min(r + 1, length - r)
        var col = min(x + 1, width - x)
        min(row, col) 
    }
}
```

</ul>
<h2 align="center">Вывод</h2>
<p align="justify">Таким образом, я продолжаю изучать Android Studio и развивать свой первый проект - GeoQuiz. Добавил вывод версии API устройства, ограничил пользователя тремя подсказками, результат на рисунке.</p>
<img src="res.PNG" width="428" height="801" title="GeoQuiz">






