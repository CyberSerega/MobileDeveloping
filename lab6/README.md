<h1 align="center" paddin> МИНИСТЕРСТВО НАУКИ И ВЫСШЕГО ОБРАЗОВАНИЯ РОССИЙСКОЙ ФЕДЕРАЦИИ ФЕДЕРАЛЬНОЕ ГОСУДАРСТВЕННОЕ БЮДЖЕТНОЕ ОБРАЗОВАТЕЛЬНОЕ УЧРЕЖДЕНИЕ ВЫСШЕГО ОБРАЗОВАНИЯ «САХАЛИНСКИЙ ГОСУДАРСТВЕННЫЙ УНИВЕРСИТЕТ»</h1>

<p align="center"><strong>Лабораторная работа №6 "Версии Android SDK и совместимость" </strong></p>

<p align="right">Выполнил: Рогаль С. А.</p>
<p align="right">Проверил: Соболев Е. И.</p>

<p align="center">г. Южно-Сахалинск <br> 2024 год</p>

<h2 align="center">Введение</h2>
<p align="justify">SDK расшифровывается как Software Development Kit (комплект для разработки программного обеспечения), он представляет из себя набор различных инструментов, библиотек, документации, примеров, помогающих разработчикам создавать, отлаживать и запускать приложения для Android. API предоставляется вместе с SDK.</p>
<p align="justify">API расшифровывается как Application Programming Interface (программный интерфейс приложения). Это просто интерфейс, уровень абстракции, который обеспечивает связь между двумя разными «частями» программного обеспечения. Он работает как договор между поставщиком (например, библиотекой) и потребителем (например, приложением).Это набор формальных определений, таких как классы, методы, функции, модули, константы, которые могут использоваться другими разработчиками для написания своего кода. При этом API не включает в себя реализацию. Уровень API — это целочисленное значение, однозначно идентифицирующее версию API фреймворка, предлагаемую платформой Android.</p>
<h2 align="center">Цели и задачи</h2>
<ol>
  <li><strong>Упражнение. Вывод версии Android на устройстве</strong><br>
<p>Добавьте в макет GeoQuiz виджет TextView для вывода уровня API устройства, на котором работает программа.</p>
</li>
  <li><strong>Упражнение. Ограничение подсказок</strong><br>
<p>Ограничьте пользователя тремя подсказками. Храните информацию о том, сколько раз пользователь подсматривал ответ, и выводите количество оставшихся подсказок под кнопкой. Если ни одной подсказки не осталось, то кнопка получения подсказки блокируется.</p>
</ol>

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
<p align="justify">Таким образом, я продолжаю изучать Android Studio и развивать свой первый проект - GeoQuiz. Добавил вывод версии API устройства, ограничил пользователя тремя подсказками</p>





