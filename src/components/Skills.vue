<template>
  <div class="hello">
    <vue-typer  text='My name is michael kimani, im a vue and laravel developer'
        :repeat='Infinity'
        :shuffle='false'
        initial-action='typing'
        :erase-delay='550'
        erase-style='select-all'
        :erase-on-complete='false'
        caret-animation='smooth'
></vue-typer>
   <h1>My skills</h1> 
   <!-- {{name}}-->
   <!--interpolation of text and html atrritubes-->

   <!--{{btnState ? 'The button is disabled' : 'The button is active'}}-->

   <!--<button  v-on:click="changeName" v-bind:disabled="btnState">Change Name</button><br>-->
   <div class="holder">
     <form @submit.prevent="addSkill">  
       <input type="text"  placeholder="Enter your new skill here.." v-model="skill" v-validate="'min:5'" name="skill" ><br/>
       <transition name="animate-in" enter-active-class="animated flipInX" leave-active-class="animated flipOutX">
         <p  class="alert alert-danger" v-if="errors.has('skill')">{{ errors.first('skill') }}</p>

       </transition>
       
       {{skill}}
     </form>
     
     <ul>
       <transition-group name="list" enter-active-class="animated bounceInUp" leave-active-class="animated bounceOutDown">
         <li v-for="(data,index) in skills" :key="index">{{data.skill}}
           <i class="fa fa-minus-circle" v-on:click="remove"></i>
       </li>

       </transition-group>
       
     </ul>
     <!--
     <p v-if="skills.length >1"> You have more than 1 skill</p>
     <p v-else>You do not have any skill</p>
     <div v-bind:class="alertObject"></div>
     -->

   </div>
  
  </div>
</template>

<script>
export default {
  name: 'Skills',
  data () {
    return {
     // name:'Michael Kimani',
      //btnState:true
      skill:'',
      skills:[
        {"skill":"Vue Developer"},
        {"skill":"laravel Developer"}
      ],
     
    }
  },
  methods:{
    addSkill()
    {
       this.$validator.validate().then(valid => {
                if (valid) {
                    this.skills.push({skill:this.skill})
                     this.skill='';
                }
                else
                {
                  console.log('invalid');
                }
            });
      
     
    },
    remove(id)
    {
      this.skills.splice(id,1);
    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import "https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.0/animate.min.css";
@import "https://use.fontawesome.com/releases/v5.7.2/css/all.css";
.holder {
    background: #fff;
  }

  ul {
    margin: 0;
    padding: 0;
    list-style-type: none;
  }
  
  ul li {
    padding: 20px;
    font-size: 1.3em;
    background-color: #E0EDF4;
    border-left: 5px solid #3EB3F6;
    margin-bottom: 2px;
    color: #3E5252;
  }

  p {
    text-align:center;
    padding: 30px 0;
    color: gray;
  }

  .container {
    box-shadow: 0px 0px 40px lightgray;
  }
  input {
    border: 0;
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  box-sizing: border-box;
  border: none;
  background-color: #3CBC8D;
  font-size: 1.3em;

}
i{
  float:right;
  cursor: pointer;
}



</style>
