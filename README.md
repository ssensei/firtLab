# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #2 выполнил:
- Малыгин Виктор Александрович
- НМТ-213929
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

## Цель работы
Познакомиться с программными средствами для организции передачи данных между инструментами google, Python и Unity

## Задание 1
### Реализовать совместную работу и передачу данных в связке Python - Google-Sheets – Unity. При выполнении задания используйте видео-материалы и исходные данные, предоставленные преподавателя курса.
- В облачном сервисе google console подключить API для работы с google sheets и google drive.
- Реализовать запись данных из скрипта на python в google-таблицу. Данные описывают изменение темпа инфляции на протяжении 11 отсчётных периодов, с учётом стоимости игрового объекта в каждый период.
- Создать новый проект на Unity, который будет получать данные из google-таблицы, в которую были записаны данные в предыдущем пункте.
- Написать функционал на Unity, в котором будет воспризводиться аудио-файл в зависимости от значения данных из таблицы.

####Скриншот с демонстрацией сохранения данных в GoogleSheets:
![изображение](https://user-images.githubusercontent.com/61794638/194843430-d870f7ee-e939-4398-8253-6f69d49082a8.png)
####Скриншот с демонтрацией кода для создания данных в GoogleSheets
![изображение](https://user-images.githubusercontent.com/61794638/194844004-5d7d58ae-c522-4c65-abae-cde8d17d2c49.png)
####Скриншоты с демонтрацией кода для вызова звука в Unity
![изображение](https://user-images.githubusercontent.com/61794638/195159382-65a1965f-ec9d-478b-bc88-de110e7053d8.png)
![изображение](https://user-images.githubusercontent.com/61794638/195159425-2b5369d7-5b02-458c-bfa5-72404dacee0a.png)
![изображение](https://user-images.githubusercontent.com/61794638/195159470-7fd5bc27-52f9-4fc4-82ff-ab381f22b441.png)
![изображение](https://user-images.githubusercontent.com/61794638/195159488-52901f63-7072-4f73-901f-07878a11c171.png)
####Скриншот с демонтрацией работы в Unity
![изображение](https://user-images.githubusercontent.com/61794638/195159790-4c51e7fe-6b4b-4660-98e6-b200a7208456.png)



## Задание 2
### 
Ход работы:
- Произвести подготовку данных для работы с алгоритмом линейной регрессии. 10 видов данных были установлены случайным образом, и данные находились в линейной зависимости. Данные преобразуются в формат массива, чтобы их можно было вычислить напрямую при использовании умножения и сложения.
Скриншоты выполнения:
import numpy as np
import gspread
import numpy as np

gc = gspread.service_account(filename='unitydata-365217-b1abff74e3ad.json')
sh = gc.open("Sheet1")

x = [3,21,22,34,54,34,55,67,89,99]
x = np.array(x)
y = [2,22,24,65,79,82,55,130,150,199]
y = np.array(y)

def model(a,b,x):
    return a*x+b
def loss_function(a,b,x,y):
    num = len(x)
    prediction=model(a,b,x)
    return (0.5/num)*(np.square(prediction-y)).sum()
def optimaze(a,b,x,y):
    num = len(x)
    prediction=model(a,b,x)
    da = (1.0/num)*((prediction-y)*x).sum()
    db = (1.0/num)*((prediction-y)).sum()
    a = a- Lr*da
    b = b- Lr*db
    return a,b
def iterate(a,b,x,y,times):
    for i in range(times):
        a,b = optimaze(a,b,x,y)
    return a,b

a = np.random.rand(1)
print(a)
b = np.random.rand(1)
print(b)
Lr = 0.000001

i=1

a,b=iterate(a,b,x,y,1)
prediction = model(a,b,x)
loss = loss_function(a,b,x,y)
sh.sheet1.update(('A' + str(i)), str(a))
sh.sheet1.update(('B' + str(i)), str(b))
sh.sheet1.update(('C' + str(i)), str(loss))
i = i+1

a,b=iterate(a,b,x,y,2)
prediction = model(a,b,x)
loss = loss_function(a,b,x,y)
sh.sheet1.update(('A' + str(i)), str(a))
sh.sheet1.update(('B' + str(i)), str(b))
sh.sheet1.update(('C' + str(i)), str(loss))
i = i+1

a,b=iterate(a,b,x,y,3)
prediction = model(a,b,x)
loss = loss_function(a,b,x,y)
sh.sheet1.update(('A' + str(i)), str(a))
sh.sheet1.update(('B' + str(i)), str(b))
sh.sheet1.update(('C' + str(i)), str(loss))
i = i+1

a,b=iterate(a,b,x,y,4)
prediction = model(a,b,x)
loss = loss_function(a,b,x,y)
sh.sheet1.update(('A' + str(i)), str(a))
sh.sheet1.update(('B' + str(i)), str(b))
sh.sheet1.update(('C' + str(i)), str(loss))
i = i+1

a,b=iterate(a,b,x,y,5)
prediction = model(a,b,x)
loss = loss_function(a,b,x,y)
sh.sheet1.update(('A' + str(i)), str(a))
sh.sheet1.update(('B' + str(i)), str(b))
sh.sheet1.update(('C' + str(i)), str(loss))
i = i+1

a,b=iterate(a,b,x,y,1000)
prediction = model(a,b,x)
loss = loss_function(a,b,x,y)
sh.sheet1.update(('A' + str(i)), str(a))
sh.sheet1.update(('B' + str(i)), str(b))
sh.sheet1.update(('C' + str(i)), str(loss))
i = i+1


## Задание 3
### Должна ли величина loss стремиться к нулю при изменении исходных данных? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ.
Ответ: с каждой новой итерацией величина loss стремится к 0, это мы можем видеть на скриншоте ![изображение](https://user-images.githubusercontent.com/61794638/192373191-da677fff-1e64-4b0d-b141-c7cc00c954b3.png) , каждая итерация способствует изменению исходных значений, следовательно величина loss должна стремиться к нулю при изменении исходных данных 

### Какова роль параметра Lr? Ответьте на вопрос, приведите пример выполнения кода, который подтверждает ваш ответ. В качестве эксперимента можете изменить значение параметра.
Ответ: параметр Lr нужен для определения шага при вычислении новых значений а и b при оптимизации. (Визуально увеличивает расстрояния между линиями итераций)

## Выводы
В ходе данной работы я узнал что такой линейная регрессия, написал(переписал) код реализации линейной регрессии, ознакомился с работой в Unity, Jupyter и google.colab. 

