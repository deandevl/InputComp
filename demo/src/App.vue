<template>
  <div class="demo_container">
    <button v-on:click="set_job">Set Job to 'Janitor'</button>
    <button v-on:click="show_values">Show Current Values (at the console)</button>
    <input-comp
        heading="Enter your job"
        header_position="below"
        placeholder="Enter job here"
        input_size="40"
        :input_value="current_job"
        :css_variables="css_variables"
        v-on:input_comp_value_changed="value => {this.current_job = value}">
    </input-comp>

    <input-comp
        heading="Enter your name"
        placeholder="Enter name here"
        input_size="70"
        header_position="below"
        :input_value="current_name"
        :single_border="single_border"
        :css_variables="css_variables"
        v-on:input_comp_value_changed="value => {this.current_name = value}">
    </input-comp>

    <input-comp
        heading="Enter your address"
        placeholder="Enter address here"
        input_size="90"
        header_position="above"
        :input_value="current_address"
        :css_variables="css_variables_wide"
        v-on:input_comp_value_changed="value => {this.current_address = value}">
    </input-comp>

    <input-comp
        heading="Enter your age:"
        placeholder="Enter age here"
        input_type="number"
        input_size="40"
        :input_value="current_age"
        :css_variables="css_variables_wide"
        v-on:input_comp_value_changed="value => {this.current_age = value}">
    </input-comp>

    <input-comp
        heading="Enter your birth date:"
        input_type="date"
        :input_value="current_birth_date"
        :css_variables="css_variables_extra_wide"
        :single_border="single_border"
        v-on:input_comp_value_changed="value => {this.current_birth_date = value}">
    </input-comp>

    <input-comp
        heading="Do you smoke?"
        input_type="checkbox"
        :input_checked="current_smoker"
        :css_variables="css_variables_wide"
        v-on:input_comp_value_changed="value => {this.current_smoker = value}">
    </input-comp>

    <input-comp
        heading="Time you eat dinner?"
        input_type="time"
        :input_value="current_dinner_time"
        :css_variables="css_variables_wide"
        v-on:input_comp_value_changed="value => {this.current_dinner_time = value}">
    </input-comp>

    <input-comp
        heading="Month/Year of Collage Graduation:"
        input_type="month"
        :input_value="current_graduation"
        :css_variables="css_variables_extra_wide"
        v-on:input_comp_value_changed="value => {this.current_graduation = value}">
    </input-comp>

    <input-comp
        heading="Select your favorite color:"
        input_type="color"
        :input_value="current_color"
        :css_variables="css_variables_wide"
        v-on:input_comp_value_changed="value => {this.current_color = value}">
    </input-comp>

    <input-comp
        heading="Your email address:"
        input_type="email"
        input_size="40"
        :input_value="current_email"
        :css_variables="css_variables_extra_wide"
        v-on:input_comp_value_changed="value => {this.current_email = value}">
    </input-comp>
  </div>
</template>

<script>
  import InputComp from 'inputcomp';

  export default {
    name: 'App',
    data: function() {
      return {
        single_border: true,

        current_job: 'Pipe Fitter',
        current_name: null,
        current_address: null,
        current_age: 56,
        current_birth_date: null,
        current_smoker: true,
        current_dinner_time: '17:30:00',
        current_graduation: '1972-08',
        current_color: '#6770d8',
        current_email: null,

        css_variables: {
          input_comp_heading_color: 'white',
          input_comp_input_color: 'white',
          input_comp_input_border_color: 'white',
          input_comp_input_placeholder_color: 'white',
          input_comp_input_focus_background: 'black'
        },
        css_variables_wide: {
          input_comp_heading_color: 'white',
          input_comp_input_color: 'white',
          input_comp_input_border_color: 'white',
          input_comp_input_placeholder_color: 'white',
          input_comp_input_focus_background: 'black',
          input_comp_width: '20rem'
        },
        css_variables_extra_wide: {
          input_comp_heading_color: 'white',
          input_comp_input_color: 'white',
          input_comp_input_border_color: 'white',
          input_comp_input_placeholder_color: 'white',
          input_comp_input_focus_background: 'black',
          input_comp_width: '30rem'
        }
      };
    },
    components: {
      InputComp
    },
    methods: {
      show_values: function(){
        console.log(`--------Current Values---------\n
      ---Job: ${this.current_job}\n
      ---Name: ${this.current_name}\n
      ---Address: ${this.current_address}\n
      ---Age: ${this.current_age}\n
      ---Birth Date: ${this.current_birth_date}\n
      ---Smoker?: ${this.current_smoker}\n
      ---Eat Dinner Time: ${this.current_dinner_time}\n
      ---Graduation Date: ${this.current_graduation}\n
      ---Favorite Color: ${this.current_color}\n
      ---Email address: ${this.current_email}\n
      `);
      },
      // set the value of component InputComp for job to 'Janitor'
      set_job: function(){
        this.current_job = 'Janitor';
      }
    }
  }
</script>

<style>
  .demo_container {
    height: 800px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    color: white;
    background-color: black;
    padding: 20px;
  }
  button {
    width: 260px;
    height: 22px;
  }
</style>