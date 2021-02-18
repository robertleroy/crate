## Contents
[Install Firebase](#add-firebase)  
[firebase.js](#firebasejs)  
[UserCreate.vue](#usercreatevue)  
[UserList.vue](#userlistvue)  
[Edit.vue](#editvue)  
[router.js](#routerjs)  
  
## Add Firebase
``` bash
npm i firebase
```
[top](#contents) 
___

## firebase.js
``` js
import firebase from 'firebase'

// import firebase from 'firebase/app';
// import 'firebase/firestore';

import { ref, onUnmounted } from 'vue'

const config = {
  apiKey: "AIzaSyCsTTsbZPmKdh4E9sW3f94yTjiXisRvOfI",
  authDomain: "clio-f2014.firebaseapp.com",
  projectId: "clio-f2014",
  storageBucket: "clio-f2014.appspot.com",
  messagingSenderId: "571753554371",
  appId: "1:571753554371:web:7ee42af5deded015835d76",
  measurementId: "G-SMBX8WDKY2"
}

const firebaseApp = firebase.initializeApp(config)

const db = firebaseApp.firestore()
const usersCollection = db.collection('users')

export const createUser = user => {
  return usersCollection.add(user)
}

export const getUser = async id => {
  const user = await usersCollection.doc(id).get()
  return user.exists ? user.data() : null
}

export const updateUser = (id, user) => {
  return usersCollection.doc(id).update(user)
}

export const deleteUser = id => {
  return usersCollection.doc(id).deletee()
}

export const useLoadUsers = () => {
  const users = ref([])
  usersCollection.onSnapshot(snapshot => {
    users.value = snapshot.docs.map(doc => ({
      id: doc.id, ...doc.data()
    }))
  })
  onUnmounted(close)
  return users
}
```
[top](#contents) 
___


## UserCreate.vue
``` html
<script>
  import { createUser } from '@/firebase'
  import { reactive } from 'vue'
  
  export default {
    name: 'UserCreate',
    setup() {

      const form = reactive({
        name: '', 
        email: ''
      })

      const onSubmit = async () => {
        await createUser({...form})
        form.name = ''
        form.email = ''
      }

      return {
        form, onSubmit
      };
    }
  };
</script>

<template>
  <section class='card'>
    <form @submit.prevent="onSubmit">
      <div class="spacer">
        <label>Name</label>
        <input type="text" v-model="form.name" required>
      </div>
      
      <div class="spacer">
        <label>Email</label>
        <input type="email" v-model="form.email" required>
      </div>

      <div class="spacer">
        <button type="submit">Create User</button>
      </div>
    </form>    
  </section>
</template>

<style scoped lang='scss'>
  @import '../scss/imports';
  label {
    margin-right: 1rem;
    &::after {
      content: ':'
    }
  }
  input {
    // border-bottom: $muted-5;
    border-bottom-width: 1px;
  }

  .spacer {
    padding: 1rem 0;
  }
</style>
```
[top](#contents) 
___


## UserList.vue
``` html
<script>
  import { useLoadUsers, deleteUser } from '@/firebase'

  export default {
    name: 'UserList',
    setup() {
      const users = useLoadUsers()
      return { users, deleteUser }
    },
  };
</script>

<template>
  <section class='card'>
    <div class='list'>
      <div class='listItem'
        v-for='user of users'
        :key='user.id'>
    
        <div class='name'>{{ user.name }}</div>
        <div class='email'>{{ user.email }}</div>
        <router-link :to="`/edit/${user.id}`">
          <button>edit</button>
        </router-link>
        
        <button @click="deleteUser(user.id)">delete</button>
    
      </div>
    </div>
    
  </section>
</template>

```
[top](#contents) 
___



## Edit.vue
``` html
<script>
  import {reactive, computed, onMounted } from 'vue'
  import { useRouter, useRoute } from 'vue-router'
  import { getUser, updateUser } from '@/firebase'

  export default {
    name: 'Edit',
    setup() {
      const router = useRouter()
      const route = useRoute()
      const userId = computed(() => route.params.id)

      const form = reactive({
        name: '', email: ''
      })

      onMounted(async () => {     
        const user = await getUser(userId.value)
        // console.log('userId', userId.value)
        
        form.name = user.name
        form.email = user.email
      })

      const update = async () => {
        await updateUser(userId.value, { ...form })
        router.push('/')
        form.name = ''
        form.email = ''
      }

      return {
        form, update
      };
    }
  };
</script>

<template>
  <section class='edit'>
    <form @submit.prevent="update">
      <div class="spacer">
        <label>Name</label>
        <input type="text" v-model="form.name" required>
      </div>
      
      <div class="spacer">
        <label>Email</label>
        <input type="email" v-model="form.email" required>
      </div>

      <div class="spacer">
        <button type="submit">Update User</button>
      </div>
    </form>    
    
  </section>
</template>

<style scoped lang='scss'>
  @import '../scss/imports';
  label {
    margin-right: 1rem;
    &::after {
      content: ':'
    }
  }
  input {
    // border-bottom: $muted-5;
    border-bottom-width: 1px;
  }

  .spacer {
    padding: 1rem 0;
  }
</style>
```
[top](#contents) 
___



## router.js
``` js
import { createRouter, createWebHistory } from 'vue-router'
import Home from '../views/Home.vue'
import Edit from '../views/Edit.vue'


const routes = [
  {
    path: '/',
    name: 'Home',
    component: Home
  },
  {
    path: '/edit/:id',
    name: 'Edit',
    component: Edit
  },
  {
    path: '/about',
    name: 'About',
    // route level code-splitting
    // this generates a separate chunk (about.[hash].js) for this route
    // which is lazy-loaded when the route is visited.
    component: () => import(/* webpackChunkName: "about" */ '../views/About.vue')
  }
]

const router = createRouter({
  history: createWebHistory(process.env.BASE_URL),
  routes
})

export default router
```

[top](#contents) 
___
