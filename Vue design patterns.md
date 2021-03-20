Vue design patterns

## Props
***
Очень важно при написании кода разделять бизнес логику и UI
Проектировать все так чтобы не особо зависело от выбранного фреймворка.

```
export default {
    props: {
        variant: {
            type: String,
            required: true,
            validator: (variant) => {
                if (!['success', 'warning', 'error'].includes(variant)) 
                throw Error(
                `variant is required and must` +
                `be either 'success', 'warning' or 'error'.` +
                `You passed: ${variant}`
                )
            }

            return true

            }
        }

    }

}
```

***
для проверки рендеринга в тестах есть удобная функция - render()
она также привязывает все доступные запросы к функции screen()

пример - 
```javascript
	render(Navbar)
	screen.getByText('Login')
```
при использовании отрендеренного компонента в нескольких тестах удобно вынести его в отдельную функцию
```javascript
	function renderNavbar(props) {
		render(Navbar, {
			props
		})
	}
```

***
Когда мы пишем код мы концентрируемся на том ***как*** он работает. Когда мы пишем тесты, нам все равно как это работает, вместо этого мы фокусируемся на том ***что это делает*** и правильно ли.

***

Если кнопке задать аттрибут role="increment" - то в тесте можно найти ее - getByRole("increment")

***

1. Называть вызываемый метод и событие одинаковыми именами. $emit('submit') - вызываемый метод тоже называем submit

2. или именуем методы которые вызывают $this.emit() или ctx.emit() используя префикс handleXXX - handleSubmit в данном случае.

   
## Emits
Объявление событий в компоненте облегчает понимание что делает этот компонент и как его использовать.

Пример объявления события с валидацией:

```javascript
export function submitValidator(count) {
	if(typeof count !== 'string' && !isNaN(count)) {
		throw Error(`
			Count should be a number
			Got: ${count}
		`)
	}
	return true
}

export default {
	emits: {
		submit: submitValidator
	}
}
```
Написание теста для такого события не составит труда - expect(actual).toThrow()
Написать два теста в которых проверить actual с валидным и невалидным значением.


## Testable Forms

[form validation](https://github.com/lmiller1990/design-patterns-for-vuejs-source-code/blob/master/examples/form-validation/form.js)

screen.getByLabelText() - еще одна функция полезная в тестировании форм.



## HTTP and API

При тестировании Vuex лучше использовать настоящий store, а не его jest.mock версию. Потому что при последующем изменении стора, например удалении некоторых методов тесты будут проходить, а код будет поломанный.

Хорошая библиотека для имитации запросов и ответов на сервер [mswjs](https://mswjs.io/)

---

## Vue 3 notes

Хуки нужно использовать в виде функций внутри setup()

```
onMounted(() => {
	fn()
})
```



---

ref() - создает реактивное значение, для доступа к значению нужно использовать .value

```
const count = ref(0)
count.value += 1
```

---

reactive() - для больших объектов, которые содержат несколько значений

```
const numbers = reactive({
	a: 0,
	b: 0
})

numbers[num] += 1
```

---

computed()

```
computed(() => {
	return fn()
})
```

---

watch() - срабатывает при изменении переданных значений, если передать immediate: true - срабатывает первый раз сразу же.

---

options api: beforeRouteEnter(to, from, next)

защищает роуты

---

















