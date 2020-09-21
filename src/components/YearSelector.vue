<template>
<div>
    <div class="months">
        <select id="year" class="select1" @change="changeMonth($event)" >
            <option v-for="item in years" :key="item" :value="item">{{item}}</option>
        </select>     
    </div>
</div>
</template> 
<script>
import moment from 'moment';
export default {
    name:'Dropdown',
    
    computed:{
        years(){
            const yearr =new Date().getFullYear()
            return Array.from({length:yearr-1900},(value,index)=>1901+index)
        },
            year: function(){
            var t=this;
           return t.dateContext.format('Y');
        },

    },
    methods:{
     changeMonth: function(event){
        var value=event.target.value
        console.log("value",value)
        event.target.id=value
         sessionStorage.setItem('year1',value)  
        this.$emit('changeTitle',value)  
     }, 

    },

    data(){
        return{
            dateContext:moment(),
            months:[
               {id:"01",month:"January"},
               {id:"02",month:"February"},
               {id:"03",month:"March"},
               {id:"04",month:"April"},
               {id:"05",month:"May"},
               {id:"06",month:"June"},
               {id:"07",month:"July"},
                {id:"08",month:"August"},
              {id:"09",month:"September"},
                {id:"10",month:"October"},
                {id:"11",month:"November"},
                {id:"12",month:"December"},
            ],
           
        }
    }
}
</script>
<style scoped>

  .select1{
    padding: 10px;
    justify-content: space-between;
    margin: auto;
    margin-bottom: 10px;
    margin-right: 20px;
  }
</style>