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
    <!--We have to inject object-->
    <button @click="changeName($event), decrement(5, $event)">Change Name and Decrement 5</button>

    <!--Forms-->
    <h1>Forms</h1>
    <form @submit.prevent="submitForm">
      <div>
        <label for="name">Name</label>
        <input type="text" id="name" v-model.trim.lazy="form.name">
      </div>
      <div>
        <label for="profile">Profile Summary</label>
        <textarea id="profile" v-model.trim="form.profile_summary"></textarea>
      </div>
      <div>
        <label for="country">Country</label>
        <select id="country" v-model="form.country">
          <option selected disabled value="">Select A country</option>
          <option value="kenya">Kenya</option>
          <option value="uganda">Uganda</option>
          <option value="tanzania">Tanzania</option>
          <option value="burundi">Burundi</option>
        </select>
      </div>
      <div>
        <label for="job-location">Job Location</label>
        <select id="job-location" multiple v-model="form.job_location">
          <option value="kenya">Kenya</option>
          <option value="uganda">Uganda</option>
          <option value="tanzania">Tanzania</option>
          <option value="burundi">Burundi</option>
        </select>
      </div>

      <div>
        <input type="checkbox" id="remote-work" v-model="form.remote_work" true-value="yes" false-value="no">
        <label for="remote-work">Remote Work?</label>
      </div>

      <div>
        <label>Skill Set</label>
          <input type="checkbox" id="html" name="skillset" value="html" v-model="form.skillset">
          <label for="html">HTML</label>
          <input type="checkbox" id="css" name="skillset" value="css" v-model="form.skillset">
          <label for="css">CSS</label>
      </div>

      <div>
        <input type="radio" name="experience" id="0-2" value="0-2" v-model="form.experience">
        <label for="0-2">0-2</label>
        <input type="radio" name="experience" id="2-4" value="2-4" v-model="form.experience">
        <label for="2-4">2-4</label>
        <input type="radio" name="experience" id="4-8" value="4-8" v-model="form.experience">
        <label for="4-6">4-6</label>
        <input type="radio" name="experience" id="8+" value="8+" v-model="form.experience">
        <label for="8+">8+</label>
      </div>

      <div>
        <label for="age">Age</label>
        <input @keyup.enter="submitForm" type="number" id="age" v-model.number.lazy="form.age">
      </div>
      <p>{{ JSON.stringify(form, null, 2) }}</p>
      <button type="submit">Submit</button>
    </form>

    <!--Bonus Directives-->
    <h1>Bonus Directives</h1>
    <h2>v-once</h2>
    <p v-once >{{ name }}</p>
    <button @click="changeName">Change Name</button>
    <h2>v-pre</h2>
    <p v-pre >{{ name }}</p>

    <!--Computed Properties-->
    <h1>Computed Properties</h1>
    <p>{{ full_names }}</p>
    <p>Computed Total: {{ total }}</p>
    <button @click="items.push({id: 4, title: 'Pen', price: 225})">Add Item</button>

    <!--Watchers-->
    <h1>Watchers</h1>
    <p>Current Volume: {{ volume }}</p>
    <button @click="volume -= 2">Reduce Volume</button>
    <button @click="volume += 2">Add Volume</button>
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

      form: {
        name: '',
        profile_summary: '',
        country: '',
        job_location: [],
        remote_work: 'no',
        skillset: [],
        experience: '',
        age: null,
      },

      first_name2: 'Kraig',

      last_name2: 'Ochieng',

      items: [
        {
          id: 1,
          title: 'TV',
          price: 100,
        },
        {
          id: 2,
          title: 'Laptop',
          price: 250,
        },
        {
          id: 3,
          title: 'Broom',
          price: 300,
        },
      ],

      volume: 0,

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

    submitForm() {
      console.log(this.form)
    },
  },

  computed: {
    full_names() {
      return `${this.first_name2} ${this.last_name2}`
    },

    total() {
      let total = 0

      for(let i = 0; i < this.items.length; i++) {
        total += this.items[i].price
      }

      return total
    }
  },

  watch: {
    volume(newValue, oldValue) {
      if(newValue === 16 && oldValue < newValue ) {
        alert('Volume too high')
      }
    }
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
