<template>
  <div class="inputComp">
    <div :class="compute_container_class()">
      <div class="inputComp_headerBox" v-show="heading" :style="header_style">{{heading}}</div>
      <input
          class="inputComp_input"
          :size="input_size"
          :type="input_type"
          :style="input_box_style"
          :placeholder="placeholder"
          :value="input_value"
          :checked="input_checked"
          v-on:change="value_changed($event)">
    </div>
  </div>
</template>

<script>
  export default {
    name: 'InputComp',
    props: {
      heading: {
        type: String,
        default: null
      },
      input_value: {
        default: null
      },
      input_checked: {
        type: Boolean,
        default: false
      },
      input_type: {
        type: String,
        default: 'text'
      },
      placeholder: {
        type: String,
        default: 'Enter a value'
      },
      input_size: {
        type: String,
        default: '40'
      },
      header_position: {
        type: String,
        default: 'left'
      },
      single_border: {
        type: Boolean,
        default: false
      },
      css_variables: {
        type: Object,
        default: () => {
          return null;
        }
      }
    },
    computed: {
      header_style: function(){
        if(this.header_position === 'left'){
          return 'margin-right: 5px;';
        }else if(this.header_position === 'below'){
          return 'margin-top: 2px;';
        }
      },
      input_box_style: function(){
        let box_style = null;
        if(this.single_border){
          box_style = 'border: none; border-bottom: 1px solid';
        }else{
          box_style = 'border: 1px solid;';
        }

        if(this.input_type === 'number'){
          box_style = `${box_style}width: ${this.input_size}px;`;
        }
        return box_style;
      }
    },
    methods: {
      value_changed: function(e){
        if(this.input_type === 'checkbox'){
          this.$emit('input_comp_value_changed', e.currentTarget.checked);
        }else if(this.input_type === 'number'){
          this.$emit('input_comp_value_changed',e.currentTarget.valueAsNumber);
        }else {
          this.$emit('input_comp_value_changed',e.currentTarget.value);
        }
      },
      compute_container_class: function() {
        if(this.header_position === 'left'){
          return 'inputComp_containerBox__left';
        }else if(this.header_position === 'above'){
          return 'inputComp_containerBox__top';
        }else if(this.header_position === 'below'){
          return 'inputComp_containerBox__below';
        }
      }
    },
    mounted(){
      if(this.css_variables !== null){
        for(let key of Object.keys(this.css_variables)){
          this.$el.style.setProperty(`--${key}`, this.css_variables[key]);
        }
      }
    }
  }
</script>

<style lang="less">
  :root {
    --input_comp_width: 10rem;
    --input_comp_font_family: Verdana,serif;
    --input_comp_heading_color: black;
    --input_comp_heading_font_size: 1rem;
    --input_comp_heading_font_weight: bold;
    --input_comp_input_font_size: 0.8rem;
    --input_comp_input_font_weight: normal;
    --input_comp_input_color: black;
    --input_comp_input_background: transparent;
    --input_comp_input_border_color: black;
    --input_comp_input_placeholder_color: black;
    --input_comp_input_focus_outline: yellow;
    --input_comp_input_focus_background: white;
  }
  .inputComp {
    width: var(--input_comp_width);
    font-family: var(--input_comp_font_family);
  }
  .inputComp_containerBox__above {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .inputComp_containerBox__below {
    display: flex;
    flex-direction: column-reverse;
  }
  .inputComp_containerBox__left {
    display: flex;
    flex-direction: row;
  }
  .inputComp_headerBox {
    align-self: center;
    text-align: center;
    color: var(--input_comp_heading_color);
    font-size: var(--input_comp_heading_font_size);
    font-weight: var(--input_comp_heading_font_weight);
  }
  .inputComp_input {
    color: var(--input_comp_input_color);
    background: var(--input_comp_input_background);
    border-color: var(--input_comp_input_border_color);
    font-size: var(--input_comp_input_font_size);
    font-weight: var(--input_comp_input_font_weight);
    padding: 0.4rem;
  }
  .inputComp_input:focus {
    outline-color: var(--input_comp_input_focus_outline);
    background-color: var(--input_comp_input_focus_background);
  }
  .inputComp_input:invalid {
    background-color: red;
  }
  .inputComp_input::-webkit-input-placeholder {
    color: var(--input_comp_input_placeholder_color);
  }
</style>