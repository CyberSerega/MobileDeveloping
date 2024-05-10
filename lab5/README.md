<h1 align="center" paddin> МИНИСТЕРСТВО НАУКИ И ВЫСШЕГО ОБРАЗОВАНИЯ РОССИЙСКОЙ ФЕДЕРАЦИИ ФЕДЕРАЛЬНОЕ ГОСУДАРСТВЕННОЕ БЮДЖЕТНОЕ ОБРАЗОВАТЕЛЬНОЕ УЧРЕЖДЕНИЕ ВЫСШЕГО ОБРАЗОВАНИЯ «САХАЛИНСКИЙ ГОСУДАРСТВЕННЫЙ УНИВЕРСИТЕТ»</h1>

<p align="center"><strong>Лабораторная работа №5 "Вторая activity" </strong></p>

<p align="right">Выполнил: Рогаль С. А.</p>
<p align="right">Проверил: Соболев Е. И.</p>

<p align="center">г. Южно-Сахалинск <br> 2024 год</p>

<h2 align="center">Введение</h2>
<p align="justify">Приложение не всегда состоит из одного экрана. Например, мы создали очень полезную программу и пользователю хочется узнать, кто же её автор. Он нажимает на кнопку «О программе» и попадает на новый экран, где находится полезная информация о версии программы, авторе, адресе сайта, сколько у автора котов и т.д. Можно воспринимать экран активности как веб-страницу с ссылкой на другую страницу.
<h2 align="center">Цели и задачи</h2>
<ol>
  <li><strong>Упражнение. Лазейка для читера </strong><br>
<p>Мошенники никогда не выигрывают... Если, конечно, им не удастся обойти вашу защиту от мошенничества. А скорее всего, они так и сделают — именно потому, что они мошенники. У GeoQuiz есть кое-какая лазейка. Пользователи могут вращать CheatActivity после чита, чтобы удалить следы обмана. После возврата к MainActivity их жульничество будет забыто. Исправьте эту ошибку, сохраняя состояние пользовательского интерфейса CheatActivity во время вращения и после уничтожения процесса. </p>
</li>
  <li><strong> Упражнение. Отслеживание читов по вопросу </strong><br>
<p>В настоящее время, когда пользователь читерит на одном вопросе, он считается читером по всем вопросам. Обновите GeoQuiz, чтобы отслеживать, сколько раз пользователь нарушал закон. Когда пользователь использует чит для ответа на заданный вопрос, осуждайте его всякий раз, когда он пытается ответить на этот вопрос. Когда пользователь отвечает на вопрос, с которым он не жульничал, покажите правильный или неправильный ответ. </p>
</ol>

<h2>Решение задач</h2>
<p>Добавили массив, который хранит информацию о читерных ответах на вопросы</p>

```kotlin
private var cheatedQuestions = Array<Boolean>(questionBank.size) { false }
```

<p>Добавили кнопку cheatButton, которая будет вызывать CheatActivity и передавать туда ответ на вопрос.</p>

```kotlin
cheatButton.setOnClickListener {
            val intent = Intent(this, CheatActivity::class.java)
            intent.putExtra("answer_text", questionBank[currentIndex].answer.toString())
            cheatedQuestions[currentIndex] = true
            startActivity(intent)
        }
```

<p>В CheatActivity добавили данный код, позволяющий получить данные из MainActivity и вывести их</p>

```kotlin
val arguments = intent.extras
        val answer = arguments?.getString("answer_text")
        answerTextView.setText(answer)
        backButton.setOnClickListener{
            finish()
        }
```

<p>Также в метода checkAnswer добавили проверку на чит</p>

```kotlin
if(cheatedQuestions[currentIndex]==true){
                Toast.makeText(this, R.string.cheat_toast, Toast.LENGTH_SHORT).show()
                if (questionBank[currentIndex].answer==answer) correctAnswCount+=1
                else incorrectAnswCount+=1
                return
}
```

<p>Для сохранения данных реализовали два метода жизненного цикла Activity: onSaveInstanceState, onRestoreInstanceState</p>

```kotlin
override fun onSaveInstanceState(outState: Bundle) {
        super.onSaveInstanceState(outState)
        outState.putInt("count", currentIndex)
        outState.putInt("correctAnswCount", correctAnswCount)
        outState.putInt("incorrectAnswCount", incorrectAnswCount)
        outState.putBooleanArray("answeredQuestions", answeredQuestions.toBooleanArray())
        outState.putBooleanArray("cheatedQuestions", cheatedQuestions.toBooleanArray())

    }

    override fun onRestoreInstanceState(savedInstanceState: Bundle) {
        super.onRestoreInstanceState(savedInstanceState)
        currentIndex = savedInstanceState.getInt("count")
        correctAnswCount = savedInstanceState.getInt("correctAnswCount")
        incorrectAnswCount = savedInstanceState.getInt("incorrectAnswCount")
        answeredQuestions = savedInstanceState.getBooleanArray("answeredQuestions")!!.toTypedArray()
        cheatedQuestions = savedInstanceState.getBooleanArray("cheatedQuestions")!!.toTypedArray()
    }
```

<h3>Задачи Codewars</h3>
<ul>
<li>Simple multiplication

  ```kotlin
fun simpleMultiplication(n: Int): Int {
    if (n % 2==0)  return n*8;
    else return n*9;
}
```

</li>
<li>Lost number in number sequence

  ```python
def find_deleted_number(arr, mixed_arr):
    if len(arr)==0:
        return 0
    return len(arr)*((arr[0]+arr[len(arr)-1])/2)-sum(mixed_arr)
```

</li>
<li>Remove String Spaces

  ```kotlin
fun noSpace(x: String): String {
  return x.replace(" ", "")
}
```

</li>
<li>String repeat

  ```kotlin
fun repeatStr(r: Int, str: String) : String{
    var temp = "";
    var i=0;
    while (i++<r){
        temp+=str;
    }
    return temp;
}
```

</li>
<li>Function 1 - hello world

  ```kotlin
fun greet():String{
    return "hello world!"
}
```

</li>
<li>Square(n) Sum

  ```kotlin
package solution

fun squareSum(n: Array<Int>): Int {
    var sum=0;
    for (num in n){
        sum+=num*num;
    }
    return sum;
}
```

</li>

<li>Century From Year

  ```kotlin
fun century(number: Int): Int {
    if (number%100==0) return number/100;
    return 1+number/100;
}
```

</li>
<li>Is n divisible by x and y?

  ```kotlin
fun isDivisible(n: Int, x: Int, y: Int): Boolean {
    return (n%x==0) and (n%y==0)
}
```

</li>
<li>Even or Odd

  ```kotlin
fun evenOrOdd(number: Int): String = if (number%2==0) "Even" else "Odd"
```

</li>
</ul>
<h2 align="center">Вывод</h2>
<p align="justify">Таким образом, я продолжаю изучать Android Studio и развивать свой первый проект - GeoQuiz. Добавил вторую Activity для подсказок, убрал лазейку с поворотом для читера через сохранение данных Activity. Кроме того, добавил отслеживание читов.</p>




