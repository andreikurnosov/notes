# Firebase DB



## Reading

```

const database = firebase.database() // подключение к фб

const messagesRef = database.ref('messages') // подключение к точке messages

// подписка на события, к значению message
database.ref('message').on('value', snapshot => {
	snapshot.val()
})

database.ref('msg').on('child_added') // подписка на добавление новых данных

//  забираем еще и id из firebase
messagesRef.on('child_added', snapshot => this.messages.push({...snapshot.val(), id: snapshot.key}))

```



## Writing

```javascript
database.ref('msg').push().set({new object values})  

database.ref('msg').push({text: 'hello', nickname: 'Hi there!'})

database.ref('who/am/I').set('alex') // создаст по пути who/am/ значение I: 'alex'

database.ref('who').child('am').child('i').set('hootlex') // тоже самое - who/am и значние i: 'hootlex', два раза - обновит имеющееся значение

```



## Deleting

```

messagesRef.child('ID').remove() 

// подписка на событие удаления
messagesRef.on('child_removed', snapshot => {
	const deletedMessage = this.messages.find(message => message.id === snapshot.key)
	const index = this.messages.indexOf(deletedMessage)
	this.messages.splice(index, 1)
})

```



## Updating

```
messageRef.child(id).update({ text: updatedText })

messageRef.on('child_changed', snapshot => ())

// для обновления нескольких значений одновременно
const payload = {}
payload['users/id/nickname'] = 'elaine'
payload['messages/id/nickname'] = 'elaine'
database.ref().update(payload)
```





---

# Firebase Auth



## Create user

```

firebase.auth().createUserWithEmailAndPassword('email', 'password') // регистрация

firebase.auth().onAuthStateChanged(user => {}) // событие слушает когда пользователь зарегится

firebase.auth().signOut() // выйти

firebase.auth().signInWithEmailAndPassword('email', 'password') // вход

```



## Errors

```

firebase.auth().createUserWithEmailAndPassword('email', 'password')
	.then(user => { this.authUser = user })
	.catch(err => alert(err.message))
	
```



## 3rd party providers

```

const provider = firebase.auth.GoogleAuthProvider()
firebase.auth().signInWithPopup(provider)
	.catch(err => alert(err.message))
	.then(data => console.log(data.user, data.credential.accessToken))	

```



## Updating user

```
// при изменение состояния вход/выход
firebase.auth().onAuthStateChanged(user => {
	this.authUser = user
	if(user) {
		this.displayName = user.displayName
		this.photoURL = user.photoURL
	}
})

firebase.updateProfile({
	displayName: this.displayName,
	photoURL: this.photoURL
})


```



```
updateEmail() {
this.authUser.updateEmail(this.email)
}

updatePassword () {
	this.authUser.updatePassword(this.newPassword)
		.then(() => { this.newPassword = null })
}
```



```
linkToGoogle - еще одна фича firebase
```























