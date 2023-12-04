
## Комп'ютерні системи імітаційного моделювання

## СПм-22-3,  Яковлєв Андрій Віталійович
### Лабораторна робота №**2**. Редагування імітаційних моделей у середовищі NetLogo
  

###  [Варіант 10,](https://github.com/Avareco/Ksim/blob/main/README.md#%D0%B2%D0%B0%D1%80%D1%96%D0%B0%D0%BD%D1%82-10-wolf-sheep-predation) [Wolf Sheep Predation](https://www.netlogoweb.org/launch#http://www.netlogoweb.org/assets/modelslib/Sample%20Models/Biology/Wolf%20Sheep%20Predation.nlogo)


  

### Внесені зміни у вихідну логіку моделі, за варіантом:
#### Для овець: 
Якцо вівця бачить вовка в радіусі 5, то починає тікати від нього
Процедура 
<pre>  move</pre>
змінена на 
 <pre>
to sheep-move
 		let nearest-wolf one-of wolves in-radius 5 ; find the nearest wolf

  	ifelse nearest-wolf != nobody [
    	face nearest-wolf ; face towards the nearest sheep
    	rt 180 ;
    	fd 1 ; move towards the sheep
  	]
  	[
    	flock
  	]
end
</pre>
#### Для вовків: 
Якщо вовк бачить вовка в радіусі 5 він від нього тікає
 <pre>
to wolf-run-from-wolf
  let nearest-wolf one-of other wolves in-radius 5 ; find the nearest wolf within vision range

  ifelse nearest-wolf != nobody [
    face nearest-wolf ;
    rt 180 ;  face away from the nearest wolf
	  fd 1 ; move away from the nearest wolf
  ]
  [
  wolf-move
  ] 
</pre>
При знаходженні на одній ділянці поля двох вовків залишається лише один з них
 <pre>
to eat-wolf;
  let wolf-in-same-chunk one-of other wolves in-radius 1 ;

  if wolf-in-same-chunk != nobody [
 	 ask wolf-in-same-chunk [ die ]
 	 set energy energy + wolf-gain-from-food / 2
   ]    
end
</pre>
Вовк гонеться за вівцею
 <pre>
to wolf-move;
  let nearest-sheep one-of sheep in-radius 10 ; find the nearest sheep within vision range

  ifelse nearest-sheep != nobody [
    face nearest-sheep ; face towards the nearest sheep
    fd 1 ; move towards the sheep
  ]
  [
    move;
  ]   
end
</pre>
### Внесені зміни у вихідну логіку моделі, на власний розсуд:
Якщо вівці не тікають від вовка вони збиваються в отару, якщо поряд немаэ овець то рухаються радомно 
<pre>
to flock  ; sheep procedure
  let neighbor other sheep in-radius 1

  ifelse any? neighbor [
    let average-heading mean [heading] of neighbor
    turn-towards average-heading 
  ]
  [
    move
  ]
end

to turn-towards [ new-heading ]  
  let current-heading heading ; Get the current heading of the sheep
  let turn-angle subtract-headings new-heading current-heading ; Calculate the angle to turn towards the new heading
   
  rt turn-angle  
  fd 1 ;
end
</pre>

Скріншот моделі в процесі симуляції

Фінальний код моделі та її інтерфейс доступні за  [посиланням](https://github.com/knureigs/GitHubDocs_Simulation/blob/main/lb/Simulation_Lab2/example-model.nlogo).  _// якщо вносили зміни до інтерфейсу середовища моделювання - то експорт потрібен у форматі nlogo, як тут. Інакше, якщо змінювався лише код логіки моделі, достатньо викласти лише його, як  [тут](https://github.com/knureigs/GitHubDocs_Simulation/blob/main/lb/Simulation_Lab2/example-model-code.html),якщо експортовано з десктопної версії NetLogo, або окремим текстовим файлом, шляхом копіпасту з веб-версії_.  

## Обчислювальні експерименти
### [1. Дослідження залежності популяції вовків від насиченості від однієї вівці](https://github.com/Avareco/Ksim/blob/main/README.md#1-%D0%B4%D0%BE%D1%81%D0%BB%D1%96%D0%B4%D0%B6%D0%B5%D0%BD%D0%BD%D1%8F-%D0%B7%D0%B0%D0%BB%D0%B5%D0%B6%D0%BD%D0%BE%D1%81%D1%82%D1%96-%D0%BF%D0%BE%D0%BF%D1%83%D0%BB%D1%8F%D1%86%D1%96%D1%97-%D0%B2%D0%BE%D0%B2%D0%BA%D1%96%D0%B2-%D0%B2%D1%96%D0%B4-%D0%BD%D0%B0%D1%81%D0%B8%D1%87%D0%B5%D0%BD%D0%BE%D1%81%D1%82%D1%96-%D0%B2%D1%96%D0%B4-%D0%BE%D0%B4%D0%BD%D1%96%D1%94%D1%97-%D0%B2%D1%96%D0%B2%D1%86%D1%96)

Досліджується залежність зростання\зменшення популяції вовків в залежності від значення насиченності, яку може отримати один вовк від однієї вівці. Змінюватись будуть значення параметра  **wolf-gain-from-food**  Інші керуючі параметри мають значення за замовчуванням:

-   **initial-number-wolveі**  50
-   **initial-number-sheep**  100
-   -   **initial-number-wolves**  50
-   **sheep-gain-from-food**  4
-   **grass-regrowth-time**  30
-   **wolf-reproduce**  5%
-   **sheep-reproduce**  4%


## Обчислювальні експерименти 
### 1. Дослідження залежності популяції вовків від насиченості від однієї вівці
Досліджується залежність зростання\зменшення популяції вовків в залежності від значення насиченності, яку може отримати один вовк від однієї вівці. Змінюватись будуть значення параметра **wolf-gain-from-food**
Інші керуючі параметри мають значення за замовчуванням:
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
<tr><td>20</td><td>47</td></tr>
<tr><td>25</td><td>67</td></tr>
<tr><td>30</td><td>123</td></tr>
<tr><td>35</td><td>128</td></tr>
<tr><td>40</td><td>112</td></tr>
<tr><td>45</td><td>90</td></tr>
<tr><td>50</td><td>33</td></tr>
</tbody>
</table>

Таблиця наочно показує що для стабільної роботи системи насиченість вовка від однієї вівці повинна бути    від 30 до 45. При менших значеннях популяція вовків вимирає від голоду, при більших занадто сильно розмножується, вбиває всіх (або майже всіх) овець і помирає від голоду 



