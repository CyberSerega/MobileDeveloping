<h1 align="center" paddin> МИНИСТЕРСТВО НАУКИ И ВЫСШЕГО ОБРАЗОВАНИЯ РОССИЙСКОЙ ФЕДЕРАЦИИ ФЕДЕРАЛЬНОЕ ГОСУДАРСТВЕННОЕ БЮДЖЕТНОЕ ОБРАЗОВАТЕЛЬНОЕ УЧРЕЖДЕНИЕ ВЫСШЕГО ОБРАЗОВАНИЯ «САХАЛИНСКИЙ ГОСУДАРСТВЕННЫЙ УНИВЕРСИТЕТ»</h1>

<p align="center"><strong>Лабораторная работа №3 "Жизненный цикл activity" </strong></p>

<p align="right">Выполнил: Рогаль С. А.</p>
<p align="right">Проверил: Соболев Е. И.</p>

<p align="center">г. Южно-Сахалинск <br> 2024 год</p>

<h2 align="center">Введение</h2>
<p align="justify">MVC — это шаблон программирования, который позволяет разделить логику приложения на три части: Model (модель). Получает данные от контроллера, выполняет необходимые операции и передаёт их в вид. View (вид или представление). Получает данные от модели и выводит их для пользователя. Controller (контроллер). Обрабатывает действия пользователя, проверяет полученные данные и передаёт их модели. 
</p>

<h2 align="center">Цели и задачи</h2>
<ol>
  <li>Предотвращение ввода нескольких ответов.
После того как пользователь введет ответ на вопрос, заблокируйте кнопки этого вопроса, чтобы предотвратить возможность ввода нескольких ответов. 
</li>
   <li>Вывод оценки.
После того как пользователь введет ответ на все вопросы, отобразите уведомление с процентом правильных ответов. </li>
</ol>

<h2>Решение задач</h2>
<p>1. Добавляем обработчик нажатий на prevButton и nextButton. Данная функция будет выключать кнопки, если на вопрос уже был дан ответ, и включать их в противном случае</p>

  ```kotlin
fun checkAnsweredQuestion(){
            if (answeredQuestions[currentIndex]==true){
                trueButton.isEnabled = false
                falseButton.isEnabled = false
            }
            else{
                trueButton.isEnabled = true
                falseButton.isEnabled = true
            }
}

```

<p>2. Было написано 2 функции. Первая будет проверять количество верных и неверных ответов на вопросы и выводить статистику, когда будут даны ответы на все вопросы (при нажатии на trueButton или falseButton)</p>

  ```kotlin
fun checkWin(){
            if(correctAnswCount+incorrectAnswCount==questionBank.size){
                val res = 100*correctAnswCount/questionBank.size
                Toast.makeText(this, "Ваш результат "+res.toString()+"% правильных ответов", Toast.LENGTH_SHORT).show()
            }
        }
```

<p>Вторая функция будет проверять ответ на вопрос и увеличивать соответствующий счетчик. (при нажатии на trueButton или falseButton)</p>

  ```kotlin
fun checkAnswer(answer:Boolean){
            if (questionBank[currentIndex].answer==answer){
                Toast.makeText(this, R.string.correct_toast, Toast.LENGTH_SHORT).show()
                correctAnswCount+=1
            }
            else{
                Toast.makeText(this, R.string.incorrect_toast, Toast.LENGTH_SHORT).show()
                incorrectAnswCount+=1
            }
        }
```

<h2 align="center">Вывод</h2>
<p align="justify">Таким образом, я продолжаю развивать первый проект в Android Studio - GeoQuiz. Дополнил механизмы ответов на вопросы и их проверки. В итоге получилась уже минимальная рабочая версия приложения. Приложение изображено на рисунке:</p>
<img src="res.PNG" width="300" height="500" title="res">


