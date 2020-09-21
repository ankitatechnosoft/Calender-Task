<template>
   <div>
        <select id="month" class="select1" @change="changeMonth($event)">
            <option  v-for="item in months" :key="item.id" :value="item.id">{{item.month}}</option>
        </select>
    </div> 
</template>
<script>
export default {
    name:'MonthSelector',
    methods:{
            changeMonth: function(){
            var selectedMonth=event.target.value
            sessionStorage.setItem('month1',selectedMonth)
            this.$emit('changeMonth',selectedMonth)   
     }, 
    },
    data(){
        return{
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