# firstBog
github 博客练习
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8" />
    <title>prototype原型与继承</title>
    <style>
        *{
            margin: 0;
            padding: 0;
        }
        ul{
            list-style: none;
        }
        .content{
            width: 300px;
            margin: 0 auto;
            margin-top: 100px;
            overflow: hidden;
            position: relative;
        }
        .box{
            width: 1500px;
            height: 200px;
            position: relative;
            left: -300px;
        }
        .box-item{
            float: left;
            width: 300px;
            height: 200px;
        }
        .box-item-1{
            background: red;
        }
        .box-item-2{
            background: purple;
        }
        .box-item-3{
            background: blue;
        }
        .box-item-4{
            background: red;
        }
        .box-item-5{
            background: purple;
        }
        .arrow{
            display: none;
        }
        .arrow span{
            display: inline-block;
            position: absolute;
            font-size: 24px;
            padding: 10px;
            top: 50%;
            cursor: pointer;
            color: #fff;
            -webkit-transform: translateY(-50%);
               -moz-transform: translateY(-50%);
                -ms-transform: translateY(-50%);
                 -o-transform: translateY(-50%);
                    transform: translateY(-50%);
        }
        .arrow span:first-child{
            left: 0px;
        }
        .arrow span:last-child{
            right: 0px;
        }
        .num{
            width: 60px;
            margin: 0 auto;
            margin-top: 20px;
        }
        .num li{
            float: left;
            width: 10px;
            height: 10px;
            border-radius: 50%;
            background: #999;
            margin-right: 10px;
            cursor: pointer;
        }
        .num .num-active{
            background: #a40b5d;
        }
        .content:hover .arrow{
            display: block;
        }
    </style>
</head>

<body>
    <div class="content">
        <div class="box" id="box" style="left:-300px;">
            <div class="box-item box-item-1">3</div>
            <div class="box-item box-item-2">1</div>
            <div class="box-item box-item-3">2</div>
            <div class="box-item box-item-4">3</div>
            <div class="box-item box-item-5">1</div>
            
            
       </div>
       <div class="arrow">
           <span id="left-arrow"><</span>
           <span id="right-arrow">></span>
       </div>
       
       <ul class="num">
           <li index="0" class="num-active"></li>
           <li index="1"></li>
           <li index="2"></li>
       </ul>
    </div>
    

</body>

<script type="text/javascript">
    var index = 0;//当前播放的角标
    var timer = null;
    
    var box  =  document.getElementById("box");
    var prev = document.getElementById("left-arrow");
    var next = document.getElementById("right-arrow");
    var div_width = document.querySelector(".box-item").clientWidth;//获取当前图片的宽度
    var dots = document.getElementsByTagName("li");
       
   
    
    //默认设置向右播放
    function play(offset){
        var newLeft = parseInt(box.style.left) + offset;

        box.style.left = newLeft + 'px';
        if(newLeft<-1200){
            box.style.left = -600 + 'px';
        }
        if(newLeft>0){
            console.log(newLeft)
            box.style.left = -600 + 'px';
        }
    }
   
    prev.onclick = function(){
        nextClick();
        
    }
    next.onclick = function(){
       nextClick();
    }
    function nextClick(){
        index++;
        if(index>2){
            index = 0;
        }
        showCurrentDot()
        play(-div_width)
    }
    function prevClick(){
        index--;
        if(index<0){
            index = 2;
        }
        
        showCurrentDot()
        play(div_width)
    }

    function showCurrentDot () {
        for(var i = 0, len = dots.length; i < len; i++){
            dots[i].className = "";
        }
        dots[index].className = "num-active";
    }

    function autoPlay () {
        timer = setInterval(function () {
            nextClick()
        },3000);
    }
    autoPlay()


    box.onmouseenter = function () {
        clearInterval(timer);
    }
    box.onmouseleave = function () {
        // autoPlay();    
    }


    for(var i = 0, len = dots.length; i < len; i++){
        dots[i].onclick = function(){
            if(this.className == 'num-active') {
                return;
            }
            var myIndex = parseInt(this.getAttribute('index'));
            
            
            var offset = -div_width * (myIndex - index);
            
            play(offset)
            index = myIndex;//更新index值
            showCurrentDot();
        }
    }








    //获取url中的参数
    function getRequest(str) {
        var url = "www.93999.com.cn/wxwebapp#/user?uid=2587&pid=10025&name=";
        var postdata = new Object();
        if (url.indexOf("?") == -1) return;
        var arr = url.substr(url.indexOf("?") + 1).split("&");
        
        // for (var i = 0; i < arr.length; i++) {
        //     postdata[arr[i].split("=")[0]] = arr[i].split("=")[1];
        // }
        console.log(arr)
        arr.forEach(function(item, index) {

            postdata[arr[index].split("=")[0]] = arr[index].split("=")[1];
        })
        console.log(postdata)
        return postdata[str];

    }
    var a = getRequest("name");
    console.log(a)




    function uper(str) {

        var len = str.split("-");
        var arr = [];
        console.log(str.split("-"))
        for (var i = 0; i < len.length; i++) {

            arr.push(len[i][0].toUpperCase() + len[i].substr(1));

        }
        
        return arr.join("")
    }
    uper("get-element-by-id")

    // 字符串反转
    function reverstr(str) {
        return str.split("").reverse().join("");
    }
    reverstr("Hello World");
    console.log(reverstr("Hello World"))

    var arr1 = [25, 14, 5, 89, 4, 5, 29, 25, 5, 6, 25];
    // 数组去重并重新排序
    function sortarr(arr) {
        if (arr.length < 1) return;
        var new_arr = [];
        var temp;
        arr.forEach(function(i, item) {
            if (new_arr.indexOf(i) == -1) {
                new_arr.push(i)
            }
        });
        console.log(new_arr)

        // sort方法排序

        console.log(new_arr.sort(function(a, b) {
            return a - b;
        }))

        //冒泡排序
        for (var k = 0; k < new_arr.length; k++) {
            for (var j = k + 1; j < new_arr.length; j++) {

                if (new_arr[k] > new_arr[j]) {
                    temp = new_arr[k];
                    new_arr[k] = new_arr[j];
                    new_arr[j] = temp;

                }
            }
        }
        console.log(new_arr);
        return new_arr
    }
    sortarr(arr1)


   
</script>

</html>
