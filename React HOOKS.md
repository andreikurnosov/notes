

# React HOOKS

Если начальное состояние является результатом дорогостоящих вычислений, вы можете вместо этого предоставить функцию, которая будет выполняться только при начальном рендеринге:

```
const [state, setState] = useState(() => {
  const initialState = someExpensiveComputation(props);
  return initialState;
});
```



---

Подписка/отписка на события вместе с useEffect

```
useEffect(() => {
  const subscription = props.source.subscribe();
  return () => {
    // Очистить подписку
    subscription.unsubscribe();
  };
});
```

Функция очистки запускается до удаления компонента из пользовательского интерфейса, чтобы предотвратить утечки памяти. Кроме того, если компонент рендерится несколько раз (как обычно происходит), предыдущий эффект очищается перед выполнением следующего эффекта.



---

 useReducer также позволяет оптимизировать производительность компонентов, которые запускают глубокие обновления, поскольку вы можете передавать dispatch вместо колбэков.

```
 const initialState = {count: 0};

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <>
      Count: {state.count}
      <button onClick={() => dispatch({type: 'decrement'})}>-</button>
      <button onClick={() => dispatch({type: 'increment'})}>+</button>
    </>
  );
}
```





---

## useEffect

удобно использовать при создании кастомных хуков.

функция которая выполняется при создании state >>>

```
const [count, setCount] = useState(() => 
	JSON.parse(localStorage.getItem("count"))
);
```

выполняется каждый раз при изменении значения count

```
useEffect(() => {
	localStorage.setItem("count", JSON.stringify(count));
}, [count])
```



---
## useRef

фокус на элементе >>>

```
const inutRef = useRef()

<input ref={inputRef} ... />

<button onClick={ () => inputRef.current.focus() }
```



Исключение ошибок с помощью рефов

```
const isCurrent = useRef(true)

useEffect(() => {
return () => {
		isCurrent.current = false
	}
}, []);

```





---
## useLayoutEffect

