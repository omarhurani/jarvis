
# A Vue component example
In this example, the component to be created is a bootstrap-styled button that has a count displayed inside it. Whenever the button is pressed, that count is incremented by 1.

The first thing included in the Vue file is a template tag. This tag must surround **one** component which surrounds all sub-components. In this example, what is needed is a simple HTML button. For the Vue component to receive the contents of the tag, the slot tag must be defined. Whenever the Vue component is used, the text inside the component tag is placed inside the slot tag inside the component itself.

Now, I also want a count value inside the button which is automatically updated whenever it is changed. The traditional way to do this is to store the text value of the button somewhere, and keep track of the count, and whenever it changes, use the DOM to access the button and update its text. In Vue, it is much simpler. Each component has its own JavaScript data and functions which is defined inside a script tag after the template tag. That script tag contains an export statement which exports the component for use in other components and files. The data and functions of the component are defined inside this export statement. For the count, we define a count variable under the data of the component, and assign it to an initial value of 1. Now, Vue allows us to directly access this count variable in the template tag by using double dented parenthesis (`{{}}`). Any JavaScript expression that evaluates into some value can be placed inside those double dented parenthesis, and the up-to-date value of that expression is displayed in the template. Using it, the count value can be placed and its up-to-date value will be displayed in the template.

The click of the button also needs to be detected and handled. Vue also allows for each component to have its own JavaScript functions that can be called on demand. To listen for the click event, Vue provides a custom tag attribute, which has the format of `v-on:event-name="JavaScript code"`. The `v-on:` can also be replaced with a simple `@`. This will listen for the event of that name, and will execute the JavaScript code when that event is caught. This is similar to HTML's basic event listening, but this method allows for custom events to be listened to and handled. We want to handle the click event of the button, and execute a component function which increments the count stored inside it, which will automatically update.

The last part that we want to handle is the styling. We don't want the user to keep using classes, and instead use a styling attribute on the tag which applies the needed style automatically. For that, Vue allows us to define a list of custom **properties** that can be used with the component as attributes. Their value then can be used like normal data in the component. However, that passed data is still bound to the parent component, and it cannot be changed directly without giving permissions or using an indirect way. The attributes that we want to receive are the color and the size of the button, so those two attributes should be defined in the props. They can be given initial values too. Then, we want to use their values to determine the needed bootstrap classes to apply to our component. Vue provides a way to have 'computed data', which is data that completely depends on other data. It is more of a value that is computed by executing a sequence of codes on already existing data. Through the 'computed' property, a function can be defined that uses the data inside the component to compute other data. The value of that function is always up-to-date with the value of the data used within it, and the function doesn't get called whenever that computed value is needed, but rather used like any normal attribute. The received color and size attributes will be received like `'color='dark' size='lg'`, and the corresponding classes for such style are `\btn btn-dark btn-lg`.

Finally, that computed value needs to be bound to the element inside the template. Using the class attribute directly doesn't work because it receives strings. Vue provides binding for attributes too through the directive `v-bind:attribute="expression"`. The `v-bind:` can also be replaced with a simple `:`. This way, we bind the class of the normal HTML button to the computed class.

The corresponding Vue code is as follows:
```html
<template>
    <button :class="buttonClass" @click="click()">
        <slot></slot> {{ count }}
    </button>
</template>

<script>
export default {
    name: 'bootbutton',
    props:{ // attributes
        color: 'light',
        size: 'lg'
    },
    data(){
        return {
            count: 1
        }
    },
    methods:{
        click(){
            this.count++;
        }
    },
    computed: {
        buttonClass(){
            return 'btn btn-'+this.color+' btn-'+this.size;
        }
    },

}
</script>
```

The component can then be used inside other Vue components as follows:
```html
<bootbutton color="danger" size="sm">Don't click me!</bootbutton>
```