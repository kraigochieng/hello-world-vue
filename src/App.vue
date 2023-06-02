<template>
  <div>
    <!--Text -->
    <h1>Dynamic Text Stuff</h1>
    <div v-text="greet"></div>
    <div v-text="name"></div>
    <h2 :class="status">Underlined</h2>
    <p v-html="bold_channel"></p>
    <p>{{ greet }},  {{ name }}</p>

    <!--Dynamic Classes-->
    <h1>Dynamic Classes</h1>
    <p class="new" :class=" isPromoted && 'promoted' ">Promoted Movie</p>
    <p :class=" isSoldOut ? 'sold-out' : 'new' ">Sold Out</p>
    <p :class="['sold-out', 'promoted']">Sold Out Promoted Mover</p>
    <p :class="[isSoldOut ? 'sold-out' : 'new', 'promoted']">Sold Out Promoted Mover</p>
    <p :class="{
      promoted: isPromoted,
      new: !(isSoldOut),
      'sold-out': isSoldOut
    }">Sold Out Promoted Mover</p>
    <p :class=" isSoldOut ? 'new' : 'promoted' ">{{ name }}</p>

    <!--Conditional Rendering-->
    <h1>Conditional Rendering</h1>
    <p v-if="num === 0">Num is 0</p>
    <p v-else-if="num < 0">Num is less than 0</p>
    <p v-else-if="num > 0">Num is greater than 0</p>

    <!--List Rendering-->
    <h1>List Rendering</h1>
      <h2>Array of primitives</h2>
      <p v-for="(name, index) in names" :key="index">
        {{ index + 1 }}. {{ name }}
      </p>
      
      <h2>Array Of Objects</h2>
      <section v-for="(student, index) in students" :key="index">
        <h6>Student</h6>
        <p>
          {{ index }}. {{ student.first_name }} {{ student.last_name }}
        </p>
        <h6>Subjects</h6>
        <p v-for="(subject, index) in student.subjects" :key="index">{{ subject }}</p>
      </section>
      <h2>Object</h2>
      <p v-for="(value, key, index) in tutorial" :key="value">{{ index }}. {{ key }}: {{ value }}</p>

    <!--Conditional List Rendering-->
    <h1>Conditional List Rendering</h1>
    <template v-for="(name, index) in names" :key="index">
      <p v-if="name.length > 5">{{ name }}</p>
    </template>

    <!-- Methods -->
    <h1>Methods</h1>
    <p>{{ add(1,34,2) }}</p>
    <p>{{ multiply(7) }}</p>

    <!--Events-->
    <h1>Events</h1>
    <p>{{ name }}</p>
    <button @click="changeName">Change Name</button>
    <p>{{ count }}</p>
    <button @click="increment()">Increment</button>
    <button @click="decrement(1, $event)">Decrement</button>
    <button @click="increment(2)">Increment 2</button>
    <button @click="decrement(2, $event)">Decrement 2</button>
    <!--We have to inject-->
    <button @click="changeName($event), decrement(5, $event)">Change Name and Decrement 5</button>
</div>
</template>

<script>

export default {
  name: 'App',
  data() {

    return {

      name: "Kraig",
      greet: "Hello",
      channel: "sourwa",
      bold_channel: "<b>sourwa</b>",
      status: "underline",
      isPromoted: true,
      isSoldOut: false,
      num: 0,
      
      names: ['Kraig', 'Ochieng', 'Omondi'],
      
      students: [
        {
          'first_name': 'Kraig',
          'last_name': 'Ochieng',
          'subjects': ['Maths', 'English', 'Kiswahili'],
        },
        {
          'first_name': 'Kristina',
          'last_name': 'Akoth',
          'subjects': ['Computer', 'Arts'],
        },
      ],

      tutorial: {
        teacher: 'Codevolution',
        title: 'Vue 3',
      },

      baseMultiplier: 5,

      count: 0,

    }
  },
    
  methods: {
    
    add(a, b, c) {
      return a + b + c
    },

    multiply(num) {
      return num * this.baseMultiplier
    },

    changeName() {
      if(this.name === 'Batman') {
        this.name = 'Kraig'
      } else {
        this.name = 'Batman'
      }
    },

    increment(num = 1) {
      this.count = this.count + num
    },

    decrement(num = 1, event) {
      this.count = this.count - num
      console.log('Event: ', event)
    },

  }
}

</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    /* text-align: center; */
    color: #2c3e50;
    margin-top: 60px;
  }

  .underline {
    text-decoration: underline;
  }

  .promoted {
    font-style: italic;
  }

  .new {
    color: green;
  }

  .sold-out {
    color: red;
  }
</style>
