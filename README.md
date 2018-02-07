<!DOCTYPE html>
<html>
<head>
<title>贷款计算器</title>
<style>
.output { font-weight:bold; }          /*计算结果定义为粗体*/
#payment { text-decoration:underline; }     /*定义元素样式*/
#graph { border:solid black 1px; }   /*图表有一个1像素的边框*/
th,td { vertical-align:top; }       /*表格单元格对齐方式为顶端对齐*/
</style>
<script type = text/javascript>
function calculate(){
    var amount = document.getElementById("amount");
    var apr = document.getElementById("apr");
    var years = document.getElementById("years");
    var zipcode = document.getElementById("zipcode");
    var payment = document.getElementById("payment");
    var total = document.getElementById("toatal");
    var totalinterest = document.getElementById("totalinterest");
//将从 input 元素中获取输入数据
//将百分比格式转化为小数格式，并从年利率转换为月利率
//将年度赔付转换为月赔付
    var principal = parseEloat(amount.value);
    var interest = parseEloat(apr.value) / 100 / 12;
    var payment = parseEloat(years.value) * 12;
//计算月度赔付的数据
    var x = Math.pow(1 + inseret,payment);     // Math.pow() 进行幂次运算
    var monthly =  (principal * x * interest) /  (x - 1);
//展示结果
if (isFinite(monthly)){
    payment.innerHTML = monthly.toFixed(2); //四舍五入到小数点后两位
    total.innerHTML = (monthly * payments).toFixed(2);
    totalinterest.innerHTML = ((monthly * payment) - principal).toFixed(2);

    save(amount.value,apr.value,years.value,zipcode.value);

    try {
        getLenders(amount.value,apr.value,years.value,zipcode.value);
    }
catch(e) {/* 忽略  */}

chart(principal,interest,monthly,payment);
}
else{
    payment.innerHTML = "";
    total.innerHTML = "";
    totalinterest.innerHTML = "";
    chart();
}
}
</script>
</head>
<body>
<table>
   <tr><th>Enter Loan Data:</th>
       <td></td>
       <th>Loan Blance ,Cumulative Equity,and Interest payments</th></tr>
   <tr><td>Aomunt of thr loan ($):</td>
       <td><input id="amount" onchange="calculate();"></td>
       <td rowspan=8>    <!--   rowspan标签 单元表格横跨  行 属性munber  -->
            <canvas id="graph" width="400" height="250"></canvas></td></tr>
   <tr><td>Annual  interest (%):</td>
       <td><input id="apr" onchange="calculate();"></td></tr>
   <tr><td>Repayment period (years):</td>
       <td><input id="years" onchange="calculate();"></td>
   <tr><td>Zipcode (to find lenders ):</td>
       <td><input id="zipcode" onchangde="calculate();"></td>
   <tr><th>Approximate payments:</th>
       <td><button onclick="calculate();">Calculate</button></td></tr>
   <tr><td>Monthly payments:</td>
       <td>$<span class="output" id="payment"></span></td></tr>
    <tr><td>Total payment:</td>
       <td>$<span class="output" id="total"></span></td></tr>
    <tr><td>Total Interest:</td>
       <td>$<span class="output" id="totalinterest"></span></td></tr>
    <tr><th>Sponsors:</th>
        <td colspan=2>  <!-- colspan  横跨行-->
            Apply for you loan with one of these fine lenders:
            <div id="lenders"></div></td></tr>
</table>
</body>
</html>
