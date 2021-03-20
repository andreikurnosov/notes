# TailwindCSS Notes

Tailwind notes

=== Plugins ===

***
Чтобы обрезать до определенного количества строк, добавляет свойство -  line-clamp-1,2,3,4,5,6

yarn add @tailwindcss/line-clamp
затем включить его в tailwind.cofig.js - 
plugins: [require('@tailwindcss/line-clamp')]

добавить свой размер - 
theme: {
	extend: {
		lineClamp: {
			10 : '10',
			12 : '12'

вариант на hover - 
variants: {
	extend: {
		lineClamp: ["hover"]

***
Добавляем синюю тень - 

module.exports = {
  theme: {
    extend: {
      boxShadow: {
        blue: '0 4px 14px 0 rgba(19, 51, 81, 0.39)',
      },
    },
  },
};


***
Чтобы добавить фокус стиль - 

focus:outline-none - отключаем фокус
focus:ring - включаем кольцо
focus:ring-pink-500 - цвет
focus:ring-1 - толщина кольца
focus:ring-inset - кольцо внутри кнопки и тп
focus:ring-offset - промежуток между кольцом и элементом
focus:ring-offset-grey-300 - чтобы закрасить этот промежуток
focus:ring-opacity-50  - прозрачность кольца

***
чтобы включить темную тему -
darkMode: 'class'

***
Grid

grid grid-cols-3 - сделает сетку, и разделить на три колонки, на родителе
auto-cols-min - минимальное количество пространство необходимое для контекста
auto-cols-max
auto-cols-fr

туда же добавляем gap-8 создается отступы со всех сторон, чтобы кастомизировать 
используем gap-x -10     gap-y-8

если нужно разное количество строк и столбцов - 
grid-cols-6 
grid-rows-4

положение элементов, или строка или столбец - 
grid-flow-col
grid-flow-row
grid-flow-row | | -col dense - чтобы плотнее лежали колонки или столбцы

На элементе:
col-span-2 - заполняет указанное количество столбцов
col-span-full - полностью заполняет колонку
col-start-4 - вначале 4 колонки
col-end-7 - в конце 7 колонки 
если совместить start и end - заполнит заданное пространство
row-span-2 - все то же самое и с колонками


***
Разделитель - 

divide-y-2 
divide-gray-200
divide-dotted
divide-x-reverse

***