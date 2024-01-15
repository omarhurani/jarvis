
# Vue router examples

In this example, vue router was used to define routes for Vue to use.
```javascript
import Vue from 'vue'
import Router from 'vue-router'
import AuthLayout from '@/layout/AuthLayout'
Vue.use(Router)

export default new Router({
  linkExactActiveClass: 'active',
  routes: [
    {
      path: '/',
      redirect: 'login',
      component: AuthLayout,
      children: [
        {
          path: '/login',
          name: 'login',
          component: () => import('./views/Login.vue')
        },
        {
          path: '/register',
          name: 'register',
          component: () => import('./views/Register.vue')
        },
        {
          path: '/reset',
          name: 'reset',
          component: () => import('./views/ForgotPassEmail.vue')
        },// etc...
      ]
    },
    {
    //......
    }   // ......
})
```

In the example, the router consists of an array of routes. The array in the example has one route element that defines authentication-related routes. The route contains of a path, which is the actual web route trailing the website URL in the browser. It also contains a redirect, which is the default route trailing the defined path (for a total route of '/login' in this case) that the router redirects to in case of requesting invalid sub-routes. The main component of the route is the component, which is the Vue component that is associated with that route. Whenever that route is accessed, the router instantiates the bound Vue component and places it in the correct location. The route also can have children, which all are also routes. Children routes are usually used when the component to be replaced is not the whole page but rather a part of it. When the route of a child is accessed, the main component of the parent is loaded, and the child is placed inside the parent component replacing a special tag defined by the vue router:

```html
<router-view></router-view>
```

There are multiple ways to use the router inside the components, either by using another special tag defined by the vue router, or by using the global router object and forcing a redirect to a different route. Examples are shown in the following code:
```html
<template>
    <div>
        <!-- Using router-link tag -->
        <router-link to="/register">
            <!-- Anything can be placed inside
            the tag just like <a></a> -->
            Register
        </router-link>
        
        <!-- Using router object -->
        <a href="#" @click:prevent="goToLogin()">Login</a>
        <!-- The addition of ':prevent' prevents the original 
        event of the anchor from happening -->
    </div>
</template>

<script>
import router from 'vue-router';
export default {
    name: 'example',
    methods:{
        goToLogin(){
            this.$router.push('/login');
            // Push the route to the router. Current route
            // is saved in browser history and new route is accessed.
        }
    }

}
</script>
```