
## Комп'ютерні системи імітаційного моделювання
## СПм-22-11, **Яковлєв Андрій Віталійович**
### Лабораторна робота №**1**. Опис імітаційних моделей та проведення обчислювальних експериментів

max-sheep
 sheep a-sheep
 wolves wolf
 energy
 countdown
 sheep-wolves-grass
  
### Варіант 10, [Wolf Sheep Predation](https://www.netlogoweb.org/launch#http://www.netlogoweb.org/assets/modelslib/Sample%20Models/Biology/Wolf%20Sheep%20Predation.nlogo)


### Вербальний опис моделі:
Ця модель досліджує стабільність екосистем хижак-жертва. Така система називається нестабільною, якщо вона має тенденцію призводити до вимирання одного або кількох видів. Навпаки, система є стабільною, якщо вона підтримує себе протягом тривалого часу, незважаючи на коливання чисельності популяції. 

### Керуючі параметри:
- **model-version** Вибір моделі - вовки та вівці, або вовки, вівці та трава
- **initial-number-wolves** визначає початкове значення вовків в моделі
- **initial-number-sheep** визначає початкове значення поголов'я овець в моделі
- **sheep-gain-from-food** визначає скільки енергії отримують вівці від кожної з'їденої травинки
- **wolf-gain-from-food** визначає кількість енергії,  яку отримають вовки за кожну з'їдену вівцю
- **grass-regrowth-time** визнаває свільки часу потрібно, щоб трава відросла з того часу, як її з'їла вівця
- **wolf-reproduce**визначає ймовірність відтворення вовків на кожному кроці моделювання
- **sheep-reproduce** визначає ймовірність відтворення вівці на кожному кроці моделювання
- **show-speed** відповідає за показ кількості енергіі овець та вовків
### Внутрішні параметри:
- **max-sheep** максимальна кількість овець в моделі до того, як вони заполонять усе поле
-  **speed** визначає кількість енергії вівці або вовка
- **countdown** змінна яка використовується в моделі де також фігурує трава, відповідає за відлік часу поки трава не відросте після того, як її з'їла вівця

### Показники роботи системи:
- максимальна кількість овець на поточному такті симуляції не може перевищувати значення max-sheep.
- вовки балансують популяцію овець від розростання на все поле моделювання
- овець повинно бути достатньо і для виживання виду, так і для виживання вовків

### Примітки:
При налаштуваннях керуючих параметрів за замовчуванням, вовки не встигають очищати поле від овець, тому десь на 330 крок вони заповнюють усе поле і моделювання завершується з повідомленням "The sheep have inherited the earth"

### Недоліки моделі:
З точки зору реального світу, вівці мали б бігти від вовка при його спробі напасти на вівцю, що, безумовно, змінило б деякі вихідні дані моделювання, як кількість овець, було б доцільно додати вірогідніть того, чи буде полювання вовка успішним, чи неавдалим. 

<br>

## Обчислювальні експерименти 
### 1. Дослідження залежності популяції вовків від насиченості від однієї вівці
Досліджується залежність зростання\зменшення популяції вовків в залежності від значення насиченності, яку може отримати один вовк від однієї вівці. Змінюватись будуть значення параметра **wolf-gain-from-food**
Інші керуючі параметри мають значення за замовчуванням:
- **initial-number-wolveі** 50
- **initial-number-sheep** 100
- - **initial-number-wolves** 50
- **sheep-gain-from-food** 4
- **grass-regrowth-time** 30
- **wolf-reproduce** 5%
- **sheep-reproduce** 4%

<table>
<thead>
<tr><th>Насиченість від вівці</th><th>Середня кількість вовків</th></tr>
</thead>
<tbody>
<tr><td>15</td><td>34</td></tr>
<tr><td>20</td><td>75</td></tr>
<tr><td>25</td><td>93</td></tr>
<tr><td>30</td><td>89</td></tr>
<tr><td>35</td><td>92</td></tr>
<tr><td>40</td><td>92</td></tr>
<tr><td>45</td><td>68</td></tr>
<tr><td>50</td><td>24</td></tr>
</tbody>
</table>

Таблиця наочно показує що для стабільної роботи системи насиченість вовка від однієї вівці повинна бути    від 20 до 40. При менших значеннях популяція вовків вимирає від голоду, при більших занадто сильно розмножується, вбиває всіх (або майже всіх) овець і помирає від голоду 

### 2. Перевірка гіпотези про те, що час, за який відновлюється трава впливає на зріст популяції овець
Досліджується залежність зростання\зменшення популяції овець в залежності від значення часу, який потрібен для відновлення травинки після того, як її з'їла вівця. Змінюватись будуть значення параметра **grass-regrowth-time**
Інші керуючі параметри мають значення за замовчуванням:
- **initial-number-wolves** 50
- **initial-number-sheep** 100
- - **initial-number-wolves** 50
- **sheep-gain-from-food** 4
- **wolf-reproduce** 5%
- **sheep-reproduce** 4%
- **wolf-gain-from-food** 20
<table>
<thead>
<tr><th>Час росту трави</th><th>Популяція овець</th></tr>
</thead>
<tbody>
<tr><td>10</td><td>604</td></tr>
<tr><td>20</td><td>191</td></tr>
<tr><td>30</td><td>157</td></tr>
<tr><td>40</td><td>153</td></tr>
<tr><td>50</td><td>150</td></tr>
<tr><td>60</td><td>129</td></tr>
</tbody>
</table>
В результаті даного дослідження, можна зробити висновок, що збільшення часу росту трави не допомагає вівцям у збільшенні популяціі, а тільки заважає.

### 3. Дослідження залежності популяції вовків від збільшення вірогідності появлення нової вівці

Досліджується залежність зростання\зменшення популяції вовків в залежності від значення вірогідності появлення нової вівці. Змінюватись будуть значення параметра **sheep-reproduce**

Інші керуючі параметри мають значення за замовчуванням:
- **initial-number-wolves** 50
- **initial-number-sheep** 100
- - **initial-number-wolves** 50
- **sheep-gain-from-food** 4
- **wolf-reproduce** 5%
- **wolf-gain-from-food** 20
- **grass-regrowth-time** 30 
<table>
<thead>
<tr><th>Час росту трави</th><th>Популяція овець</th></tr>
</thead>
<tbody>
<tr><td>2</td><td>43</td></tr>
<tr><td>4</td><td>69</td></tr>
<tr><td>8</td><td>123</td></tr>
<tr><td>16</td><td>203</td></tr>
<tr><td>20</td><td>224</td></tr>
</tbody>
</table>
У ході дослідження було виявлено, що процент вірогідності появлення нової вівці дійсно впливає на популяцію вовків, чим більше вірогідність появлення вівці, тим більше популяція вовків буде.

