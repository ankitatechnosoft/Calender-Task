<template>
    <div class="wrapper">
         <div class="dropdown">
             <YearSelector v-on:changeTitle="updateCalender" />
             <MonthSelector v-on:changeMonth="updateMonth"/>
         </div>
        <div class="calender">
            <div class="months">
                <div class="prev">
                    <span @click="subtractMonth">&#10094;</span>
                </div>
                <div>
                    <h3>{{month + '-' + year}}</h3>
                </div>
                <div class="next">
                <span @click="addMonth">&#10095;</span>
                </div>
            </div>
            <div class="weekends">
                <div v-for="day in days" :key="day">{{ day }}</div>
            </div>
            
            <div class="days">
                <div v-for="blank in firstDayOfMonth" :key="blank">&nbsp;</div>
                <div v-for="date in daysInMonth"  :key="date" class="{'current-day':date==initialDate &amp;&amp; month==initialMonth && year==initialYear}">{{date}}
                </div>                      
            </div>
        </div>
    </div>
</template>
<script> 
import moment from 'moment';
import YearSelector from './YearSelector.vue';
import MonthSelector from './MonthSelector.vue';
export default {
    name:'Calender',
     components: {
      YearSelector,
      MonthSelector
  },
    computed:{
        year: function(){
           var t=this;
            return t.dateContext.format('Y');
        },
        month: function(){
            var t=this;
            return t.dateContext.format('MMMM');
        },
        daysInMonth: function(){
            var t=this;
           return t.dateContext.daysInMonth();
        },
        currentDate: function(){
            var t=this;
            return t.dateContext.get('date');
        },
        firstDayOfMonth: function(){
            var t=this;
             var firstDay=moment(t.dateContext).subtract((t.currentDate-1),'days');
            return firstDay.weekday();
        },
        initialDate: function(){
            var t=this;
            return t.today.get('date');
        },
        initialMonth: function(){
            var t=this;
            return t.today.format('MMMM');
        },
        initialYear: function(){
            var t=this;
            return t.today.format('Y');
        },
        currentDay: function(){
            var t=this;
            return t.dateContext.format('D');
        },
           
    },
    methods: {
            addMonth: function(){
            var t=this;
             t.dateContext=moment(t.dateContext).add(1,'month');
           },
        subtractMonth: function(){
            var t=this;
            t.dateContext=moment(t.dateContext).subtract(1,'month');
        },
        
       // to change year 
    updateCalender(value){
         var t=this;
       var getSelectedMonth=sessionStorage.getItem('month1')
       console.log("getSelectedMonth")
       if(getSelectedMonth){
           t.dateContext=moment( value + '-' + getSelectedMonth,"YYYY-MM")
       }
       else{
           t.dateContext=moment().set({'year':value})
       } 
         
       },

       //to change month
       updateMonth(selectedMonth){
           var t=this;
           var selectedYear = sessionStorage.getItem('year1')
          if(selectedYear){
              t.dateContext=moment( selectedYear +'-' + selectedMonth,"YYYY-MM")
          }
          else{
              t.dateContext=moment(selectedMonth,'MM')
          }
       }
       
    },
     
    data(){   
        return{
            today:moment(),
            dateContext:moment(),
            days:['Sun','Mon','Tue','Wed','Thurs','Fri','Sat'],
        }    }
    }
</script>
<style scoped>
body{
    margin:0px;
    font-family: "Lato",sans-serif;
}

 .calender {
     width: 600px;
     height: auto;
     background-color:white;
     margin: auto;
     box-shadow: 0px 0px 15px 3px rgba(0,0,0,0.2);

 }
 .weekends{
     background-color: tomato;
     color: white;
     display: flex;
     padding: 10px 0;
 }
 .days div{
     width: 14.28%;
     margin-bottom: 20px;
    text-align: center;
    transition: all 0.4s;
  
 }

 .weekends div{
     width: 14.28%;
     text-align: center;
 }
 .days{
     display: flex;
     flex-wrap: wrap;
     text-align: center;
     font-weight: 300;
     padding: 10px 0;
 }
 .days div:hover{
     background-color:#dfe6e9;
     cursor: pointer;
 }
 .months{
     width:100%;
     background-color:blueviolet;
     color:white;
     display: flex;
     justify-content: space-between;
     cursor: pointer;
     text-align: center;
     padding: 40px 30px;
 }
 *{
     margin: 0;
     box-sizing: border-box;
 }

.dropdown{
    display: flex;
    margin-left: 45%;
}

 @media  (min-width: 768px) and (max-width: 979px){
     .calender {
     width:auto;
     }
 }
</style>
