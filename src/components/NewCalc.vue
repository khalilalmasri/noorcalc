<template>
  <div class="calcBody">
    <div class="currencyName">
      <span>{{ currency_price_active.currency_buy_code }}</span>
      <span>{{ currency_price_active.currency_buy_name }}</span>
      <span>{{ currency_price_active.currency_selling_code }}</span>
      <span>{{ currency_price_active.currency_selling_name }}</span>
    </div>
    <div class="button">
      <button @:click="buyButton">بيع</button>
      <button @:click="saleButton">شراء</button>
    </div>
    <div class="fild">
      <!-- <span>{{+currency_price_active.currency_buy_price}}</span> -->
      <input
        type="number"
        :placeholder="currency_price_active.currency_selling_name"
        v-model="inputval"
        @focus="revfalse"
        @keyup="saleButton"
      />
      <!-- <span>{{+currency_price_active.currency_selling_price}}</span> -->
    </div>
    <div class="manual">
      <input
        type="number"
        :placeholder="+currency_price_active.currency_buy_price"
        v-model="buyman"
        @keyup="buyButton"
        class="input-manual"
      />
      <span class="space"></span>
      <input
        type="number"
        :placeholder="+currency_price_active.currency_selling_price"
        v-model="saleman"
        @keyup="saleButton"
        class="input-manual"
      />
    </div>
    <div class="equal">
      <span>{{ currency_price_active.currency_buy_name }}</span>
      <input
        type="number"
        :placeholder="currency_price_active.currency_buy_name"
        v-model="resultval"
        @keyup="revers"
      />
    </div>
    <div class="update">
      <span>{{ currency_price_active.last_update_time }}</span>
      <span>{{ currency_price_active.last_update_date }}</span>
    </div>
    <div class="print">
      <button @click="print">طباعة</button>
    </div>
  </div>
  <div :id="index_id" style="display: none">
    <PrintPage
      :amount="inputval"
      :result="resultval"
      :nom="nomn"
      :buymanu="buyman"
      :salemanu="saleman"
      :buymod="buymod"
      :currency_price_active="currency_price_active"
    />
  </div>
</template>
<script>
import PrintPage from "./print.vue";

export default {
  name: "NewCalculator",
  components: {
    PrintPage,
  },
  data() {
    return {
      inputval: 0,
      resultval: 0,
      buyman: +this.currency_price_active.currency_buy_price,
      saleman: +this.currency_price_active.currency_selling_price,
      isRevers: false,
      isPrint: this.id,
      newdatanom: {},
      datanom: [],
      nomn: 1,
      buymod: true,
    };
  },
  props: {
    currency_price_active: {
      type: Object,
      required: true,
    },
    index_id: {
      type: Number,
    },
  },
  methods: {
    buyButton() {
      if (this.isRevers != true) {
        if (this.buyman == 0) {
          var value =
            this.inputval * this.currency_price_active.currency_buy_price;
          this.resultval = value;
        } else {
          var value = this.inputval * +this.buyman;
          this.resultval = value;
        }
      } else {
        if (this.buyman == "") {
          this.inputval =
            +this.resultval / +this.currency_price_active.currency_buy_price;
        } else {
          this.inputval = +this.resultval / +this.buyman;
        }
      }
      this.buymod = true;
      this.add();
      this.nomn = this.datanom.length;
    },
    saleButton() {
      if (this.isRevers != true) {
        if (this.saleman == 0) {
          var value =
            this.inputval * this.currency_price_active.currency_selling_price;
          this.resultval = value;
        } else {
          var value = this.inputval * +this.saleman;
          this.resultval = value;
        }
      } else {
        if (this.saleman == "") {
          this.inputval =
            this.resultval / this.currency_price_active.currency_selling_price;
        } else {
          this.inputval = +this.resultval / +this.saleman;
        }
      }
      this.buymod = false;
      this.add();
    },
    inputf($val) {
      console.log($val.target.value);
      var value = $val.target.value;
      this.inputval = value;
    },
    resultf($val) {
      console.log($val.target.value);
      var value = $val.target.value;
      this.resultval = value;
    },
    buymanf($val) {
      console.log($val.target.value);
      var value = $val.target.value;
      this.buyman = value;
    },
    salemanf($val) {
      console.log($val.target.value);
      var value = $val.target.value;
      this.saleman = value;
    },
    revers() {
      return (this.isRevers = true), this.buyButton();
    },
    revfalse() {
      return (this.isRevers = false);
    },
    print() {
      this.nomn = this.datanom.length;
      this.add();
      this.newdatanom = { nomn: this.nomn };
      console.log(this.newdatanom);
      this.datanom.push(this.newdatanom);
      localStorage.setItem("no", JSON.stringify(this.datanom));
      localStorage.no = JSON.stringify(this.datanom);
      if (this.buyman == "" || this.saleman == "") {
        return (
          (this.buyman = +this.currency_price_active.currency_buy_price),
          (this.saleman = +this.currency_price_active.currency_selling_price)
        );
      } else {
      }
      {
        //         var yourDOCTYPE = "<!DOCTYPE html>";
        // var printPreview = window.open('' , 'print_preview');
        // var printDocument = printPreview.document;
        // printDocument.open();
        // var head =
        //     "<head>" +
        //     "<style> .to-print{height:279mm; width:80mm; } </style>" +
        //     "</head>";
        // printDocument.write(yourDOCTYPE +
        //         "<html>" +
        //         head +
        //         "<body>" +
        //         "<div class='to-print'>" +
        //         "<!-- your content to print can be put here or you can simply use document.getElementById('id-content-toprint')-->"+
        //         "</div>"+
        //         "</body>" +
        //         "</html>");
        // printPreview.print();
        // printPreview.close()
      }

      const section = document.getElementById(this.index_id);
      if (section) {
        // Open the print dialog for the section
        section.style.display = "block"; // Ensure the section is visible
        window.print();
        section.style.display = "none"; // Hide the section again
      } else {
        alert("Section to print not found.");
      }
    },
    add() {
      this.nomn = this.datanom.length;
      if (localStorage.no != null) {
        this.datanom = JSON.parse(localStorage.no);
        console.log(10000);
      } else this.datanom = [];
    },
  },
};
</script>
<style>
@import "../assets/css/style.css";
:root {
  --main-ButtonColor: linear-gradient(#61531b, gold, rgb(148, 180, 5));
  --hover-ButtonColor: linear-gradient(#6a7506, #967f0c, #61531b);
}
.calcBody {
  max-width: auto;
  background: linear-gradient(#222, #111);
  /* font-family: system-ui; */
  border-top-left-radius: 25px;
  border-top-right-radius: 25px;
  border-bottom-color: goldenrod;
  border-bottom-width: 2px;
  border-top-width: 0px;
  border-right-width: 0px;
  border-left-width: 0px;
  border-style: solid;
  margin-bottom: 10px;
  margin-top: 0;
}
.currencyName {
  text-align: center;
  margin-left: auto;
  margin-right: auto;
  width: 100%;
  border: 2px none;
  border-top-left-radius: 25px;
  border-top-right-radius: 25px;
  background: var(--main-ButtonColor);
}
.currencyName span {
  color: #111;
  font-size: 20px;
}
span {
  margin-left: 1rem;
  margin-right: 1rem;
  color: #fcfcfc;
  width: 20%;
  font-size: 25px;
}
button {
  margin-right: 1rem;
  margin-left: 1rem;
  margin-top: 6px;
  border-radius: 5px;
  width: 35%;
  background: var(--main-ButtonColor);
  color: #111;
  cursor: pointer;
  transition: 1s;
  border: none;
  outline: none;
}
button:hover {
  scale: 1.1;
  text-transform: unset;
  background: var(--hover-ButtonColor);
  letter-spacing: 1px;
  outline: none;
}
input {
  height: 30px;
  background: radial-gradient(#222, #111);
  padding: 3px;
  width: 30%;
  font-size: 15px;
  color: #fff;
  border-width: 1px;
  border-color: gold;
  border-radius: 3px;
  margin-bottom: 5px;
  margin-top: 5px;
}
input:focus {
  background: #111;
  scale: 1.01;
  font-size: 15px;
  font-style: inherit;
  outline: none;
  border-bottom-color: gold;
  border-top-width: 0;
  border-right-width: 0;
  border-bottom-width: 3px;
  border-left-width: 0;
}
.input-manual {
  width: 15%;
}
.space {
  width: 20%;
  display: inline-block;
  height: 20px;
}
.equal {
  margin-bottom: 8px;
}
.print button {
  background: linear-gradient(#f1b775, rgb(240, 226, 150), rgb(50, 58, 14));
  margin-bottom: 5px;
}
</style>
