# VUE  notes

Функция для обновления localStorage - 

```
const updateOnLocalStorage = (propertyName, property) => 
	window.localStorage.setItem(propertyName, JSON.stringify(property))
```

Вытаскием из localStorage - 

```
const localStorageHistory = JSON.parse(
	window.localStorage.getItem('history'))
```



----

задаем типы

```
type Period = 'today' | 'this week' | 'this month'
const periods: Period[] = ['today', 'this week', 'this month']
```



ref - это generic поэтому нужно

```
const selectedPeriod = ref<Period>('today')
```

 

в функции тип аргумента задается через двоеточие

```
const setPeriod = (period: Period) => {}
```

 

создаем интерфейс для поста - 

```
export interface Post {
	id: number
	title: string
	markdown: string
	html: string
	authorId: string
	created: number
}
```

мокаем наш пост для тестирования - 

```
export const basePost: Post = {
	id: 1,
	title: "Post",
	markdown: "Content",
	html: "<p>Content</p>",
	authorId: 1,
	created: moment() // отдельная библиотека для работы с датами
}

export const todayPost: Post  = {
	...basePost, 
	title: 'Today' // изменяем значение basePost.title
}
```



Если реактивное значение изменяется внутри computed() - эта функция перезапускается



---

чтобы jest находил все файлы, а не только которые находятся внутри tests

```
  testMatch: ['**/__tests__/**/*.[jt]s?(x)', '**/?(*.)+(spec).[jt]s?(x)']
```

---









