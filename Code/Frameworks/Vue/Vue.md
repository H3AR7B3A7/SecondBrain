# Vue
[Official Vue Pages](https://vuejs.org/)

Vue.js is an open-source model–view–viewmodel front end [[JavaScript]] framework for building user interfaces and single-page applications. It was created by Evan You, and is maintained by him and the rest of the active core team members.

### Installation
- **Install NPM & Node.js**: Download installer [here](https://nodejs.org/en/download/).
- **Install Typescript**: npm install -g typescript
- **Install Vue CLI**: npm install -g @vue/cli

### VSC Extensions:

- Vetur
- Vue Snippets
- TSLint

## Support & Plugins

### Support

- Typescript

>vue add typescript

- Vue 3 (currently in separate release)

>vue add vue-next

Component definitions have changed and we will need to change the default App.vue and HelloWord.vue files accordingly:

In HelloWorld.vue:

```
<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'HelloWorld',
  props: {
    msg: {
      type: String,
      required: false,
    },
  },
});
</script>
```

In App.vue:

```
<script lang="ts">
import { defineComponent } from 'vue';
import HelloWorld from '@/components/HelloWorld.vue'

export default defineComponent({
  name: 'App',
  components: {
    HelloWorld
  },
});
</script>
```

- Property Decorator

>npm install vue-property-decorator

### Plugins

- Vuetify

>vue add vuetify

- Notifications

>npm install vue-notification

In main.js:
```
import Notifications from 'vue-notification'
 
Vue.use(Notifications)
```

## Project Commands
### Setup Existing Project
Navigate to the project folder and use following command:
>npm install

### Creating Project
Navigate to the desired folder and use following command:
>vue create <name>

### Compiles and hot-reloads for development
>npm run serve

### Compiles and minifies for production
>npm run build

### Lints and fixes files
>npm run lint

# Displaying Data
## Interpolation
{{ }}

## Event Handling
@event

## Binding to Properties
:property

## Two-Way Binding Inputs
v-model

## Add or remove DOM Elements
v-if

## Hide or Show DOM Elements
v-show

## Lists
v-for

# Defining and Manipulating Data
## Define
date()

## Custom Logic
methods

## Lifecycle Hooks
- beforeCreate
- created
- beforeMount
- mounted
- beforeUpdate
- updated
- beforeDestroy
- destroyed

## Property Depending on Values
computed

## Logic on Data Model Changes
watch

## Output Transformations
filter

# Component Communication



---
#JavaScript 