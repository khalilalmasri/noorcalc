<template>
<b><div class="printbody">
    <div class="qr">
        <table>
            <tr>
                <td>
                    <p>
                        :فاتورة صرف
                    </p>
                    <!-- <p class="arabic-font" style="display: inline;" v-if="buymod">
                    فاتورة بيع 
                :</p>
                    <p class="arabic-font" style="display: inline;" v-else>
                        فاتورة شراء 
                        :</p> -->
                    <p style= "display: inline;">{{nom}}</p>
                </td>
                <td><img src="../image/logo.png" ></td>
            </tr>
        </table>
    </div>
    <p style="font-size: large;" >شركة النور للصرافة والحوالات</p>
    <div class="time">
        <p id="current_data"> {{ currentDate()}}  <span></span>   {{ currentDateh()}}:{{ currentDatem()<10?zero="0":zero="" }}{{currentDatem()}} <span></span></p>
        <p class="arabic-font">             :
            الوقت
            </p>
    </div>
        <table class="pr">
            <tr >
                <td class="arabic-font">المبلغ</td>
                <td class="mar"></td>
                <td >سعر الصرف</td>
                <td class="mar"></td>

                <td class="arabic-font">العملة</td>
            </tr>
            <tr>
                <td>{{ amount%2===0?amount:amount.toFixed(2) }}</td>
                <td class="mar"></td>
                <td >1</td>
                <td class="mar"></td>
                <td>{{currency_price_active.currency_selling_code}}</td>
            </tr>
            <tr>
                <td>{{ +result%2===0?+result:+result.toFixed(2) }}</td>
                <td class="mar"></td>
                <td  v-if="buymod">{{buymanu}}</td>
                <td  v-else>{{salemanu}}</td>
                <td class="mar"></td>
                <td>{{currency_price_active.currency_buy_code}}</td>
            </tr>
            </table>
    <div class="qr">
        <table>
            <tr> <td style="margin: 0px; padding: 0px;"><img src="../image/Qr.jpg" ></td>
                <td><p >عفرين  -  دوار نيروز </p>
                    <p class="arabic-font" >صرافة: {{ exn }}  
            </p><p class="arabic-font">
حوالات:
{{ trn }}
</p></td>
                
            </tr>
        </table>
    </div>
</div></b>
</template>
<script>

export default {
    name: "PrintPage",

    data(){
        return{
            exn:'84 222 666 09 ',
            trn:' 04 35 664 0538 ',
            zero:'',
            
        }
} ,
props: {
    currency_price_active: {
        type: Object,
        required: true
    },
    buymod:{
        type:Boolean
    },
    amount:{
        type: Number,
    },
    result:{
        type: Number,
    },
    nom:{
        type: Number,
    },
    buymanu:{
        type:Number
    },
    salemanu:{
        type:Number,
    }
    },
methods: {
currentDate(){
var today = new Date();
var dd = String(today.getDate()).padStart(2, '0');
var mm = String(today.getMonth() + 1).padStart(2, '0'); //January is 0!
var yyyy = today.getFullYear();

return  dd + '/' + mm + '/' + yyyy + ' '
// + '     ' + today.getHours()+ ":" +today.getMinutes()  ;
},
currentDateh(){
var today = new Date();
// var dd = String(today.getDate()).padStart(2, '0');
// var mm = String(today.getMonth() + 1).padStart(2, '0'); //January is 0!
// var yyyy = today.getFullYear();

return today.getHours();
//  + ":" + today.getMinutes()  ;
//   dd + '/' + mm + '/' + yyyy + ' '
},
currentDatem(){
var today = new Date();
return today.getMinutes()  ;
}
},
}
</script>
<style>
@import '../assets/css/style.css';
*{
    font-size: 300;
    color: black;
}
/* .printbody{
    border-color: black;
    border-width: 2px;
    border-style: solid;   
} */
img{
    width: 75px;
    height: 75px;
}
p{
    display: inline;
    margin-right: 5px;
    margin-left: 5px;
    font-size: small;


}
table {
    width: 100%;
    line-height: 15px;
    
}
tr {
    padding-bottom: 5px;
}
td {
    border-color: black ;
    border-bottom-width: 1px;
    border-top-width: 0px;
    border-right-width: 0px;
    border-left-width: 0px;
    border-style: solid;
    padding-bottom: 5px;
}
.mar{
    width: 5px;
    border: none;
    
} 
.qr{
    padding: 0px;
    margin: 0px;
}
/* .pr{
font-family:'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif
} */
.qr table td {
border:none ;
}
.qr p {
    display: block;
    margin: 2px;
}
</style>