# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #3 выполнил:
- Малыгин Виктор Александрович
- НМТ-213929
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | # | 20 |
| Задание 3 | # | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

## Цель работы
Познакомиться с программными средствами для создания системы машинного обучения и ее интеграции в Unity.

## Задание 1
### В проекте Unity реализовать перцептрон, который умеет производить вычисления:
-OR | дать комментарии о корректности работы
-AND | дать комментарии о корректности работы
-NAND | дать комментарии о корректности работы
-XOR | дать комментарии о корректности работы
#### Код Perceptron.cs:
```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[System.Serializable]
public class TrainingSet
{
	public double[] input;
	public double output;
}

public class Perceptron : MonoBehaviour {

	public TrainingSet[] ts;
	double[] weights = {0,0};
	double bias = 0;
	double totalError = 0;

	double DotProductBias(double[] v1, double[] v2) 
	{
		if (v1 == null || v2 == null)
			return -1;
	 
		if (v1.Length != v2.Length)
			return -1;
	 
		double d = 0;
		for (int x = 0; x < v1.Length; x++)
		{
			d += v1[x] * v2[x];
		}

		d += bias;
	 
		return d;
	}

	double CalcOutput(int i)
	{
		double dp = DotProductBias(weights,ts[i].input);
		if(dp > 0) return(1);
		return (0);
	}

	void InitialiseWeights()
	{
		for(int i = 0; i < weights.Length; i++)
		{
			weights[i] = Random.Range(-1.0f,1.0f);
		}
		bias = Random.Range(-1.0f,1.0f);
	}

	void UpdateWeights(int j)
	{
		double error = ts[j].output - CalcOutput(j);
		totalError += Mathf.Abs((float)error);
		for(int i = 0; i < weights.Length; i++)
		{			
			weights[i] = weights[i] + error*ts[j].input[i]; 
		}
		bias += error;
	}

	double CalcOutput(double i1, double i2)
	{
		double[] inp = new double[] {i1, i2};
		double dp = DotProductBias(weights,inp);
		if(dp > 0) return(1);
		return (0);
	}

	void Train(int epochs)
	{
		InitialiseWeights();
		
		for(int e = 0; e < epochs; e++)
		{
			totalError = 0;
			for(int t = 0; t < ts.Length; t++)
			{
				UpdateWeights(t);
				Debug.Log("W1: " + (weights[0]) + " W2: " + (weights[1]) + " B: " + bias);
			}
			Debug.Log("TOTAL ERROR: " + totalError);
		}
	}

	void Start () {
		Train(8);
		Debug.Log("Test 0 0: " + CalcOutput(0,0));
		Debug.Log("Test 0 1: " + CalcOutput(0,1));
		Debug.Log("Test 1 0: " + CalcOutput(1,0));
		Debug.Log("Test 1 1: " + CalcOutput(1,1));		
	}
	
	void Update () {
		
	}
}

```

#### Скриншоты и видео с демонтрацией работы:
1) Скриншот работы OR
![изображение](https://user-images.githubusercontent.com/61794638/204572583-719d32f1-daa8-484b-936b-6dd85c75291c.png)
2) Скриншот работы AND
![изображение](https://user-images.githubusercontent.com/61794638/204572660-15bbdbfd-48d4-421d-ba6d-f86fa832e99d.png)
3) Скриншот работы NAND
![изображение](https://user-images.githubusercontent.com/61794638/204572700-a5b81736-c653-40c7-a59b-6311e0b230a9.png)
4) Скриншот работы XOR
![изображение](https://user-images.githubusercontent.com/61794638/204572780-33ef5056-4c46-4aa9-912a-0d905ab7aac4.png)

1) В данном случае прецептрон обучился правильно за 8 тренингов, это мы можем наблюдать по правильности выводимых результатах и мы видим, что TOTAL ERROR= 0
2) В данном случае прецептрон обучился правильно за 8 тренингов, это мы можем наблюдать по правильности выводимых результатах и мы видим, что TOTAL ERROR= 0
3) В данном случае прецептрон обучился правильно за 8 тренингов, это мы можем наблюдать по правильности выводимых результатах и мы видим, что TOTAL ERROR= 0
4) В данном случае прецептрон не смог обучиться даже за 10 тренингов, это все потому что оператор XOR имеет нелинейный вид, данную задачу невозможно однозначно решить таким методом, т.к часть данных все-равно будут не совпадать.


## Выводы
В ходе данной лабораторный мы научились обучать нейросеть используя библиотеки ml-agent и torch. ДЛя полного понимания работы была изучена документация по созданию тренера ml-agent. 
