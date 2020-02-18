# seisan_2

<html lang="ja">
<head>

<meta charset="UTF-8">

<style type="text/css">
    
li {
    list-style: none;
}
li:before {
    content: "● ";
}

input {
    border: none;
    width: 80px;
    font-size: 14px;
    padding: 2px;
}

input:hover {
    background-color: #eee;
}

input:focus {
    background-color: #ccf;
}

input:not(:focus) {
    text-align: right;
}

table {
    border-collapse: collapse;  
}

td {
    border: 1px solid #999;
    padding: 0;
}

tr:first-child td, td:first-child {
    background-color: #ccc;
    padding: 1px 3px;
    font-weight: bold;
    text-align: center;
}

footer {
    font-size: 80%;
}
    
 .red {color:#ff0000;}
 .grey {color:#ffffff; background:#999999;}
 .blue {color:#0000ff;}
 .waku {border:2px dotted #99cc66;
　　　　　　line-height: 200%;
　　　　　　padding: 10px;}

body { background-color: #00fff5; }
    
    </style>
    
    <script src="zan_calc.js"></script>

    </head>
    
    <body>

<h1><span class="blue"><strong>簡易計算シート付き、精算ページ</strong></span></h1>

<section>

<ul>
<li> <input type="button" id="btn1" value="精算計算  " onclick="btn1Click();" /> 　←　支払い＆精算計算、開始ボタン</li>
</ul>
    
<!--
<div id="edit_area"></div>-->
    
<script>   
//ボタン１をクリックした時の処理
function btn1Click(){ 

    var selects = prompt('参加人数を入力！');

    var selectss = prompt('支払った人の人数を入力！');

    var koukin = prompt('公金補助額を入力！');
    
var nama = [];
    for (var i=0; i<selectss; i++){
      nama[i] = prompt("支払った人の名前を入力");
    }   

var menu = [];    
    for (var i=0; i<selectss; i++){
      menu[i] = prompt(nama[i] + "さんの支払金額を入力");
    } 

    
//各自の会計額を計算
    
var kasann = [];
      kasann[0] = menu[0];
    for (var i=0; i<selectss-1; i++){
kasann[i+1] = Math.round (Number(kasann[i]) + Number(menu[i+1]));
      }
    
var kasan = Math.round (Number(kasann[i]) - Number(koukin))
      
//各自の分担分を計算

var buntan = Math.round (Number(kasan)/Number(selects));

//各自の割り勘分を計算

var wari = [];
    for (var i=0; i<selects; i++){
    wari[i] = Math.round (Number(menu[i]) - Number(buntan));
      }

    
var kasann = kasann[selectss-1]

/*
var myfunc = function () {
      var str = "document.write("各自の支払金額は<br>")
    for (var i=0; i<menu.length; i++){
      document.write(nama[i] + "さん：" + menu[i] + "円 <br>")
    }

document.write("<br>経費の総額：" + kasann + "円<br>")
      
document.write("公金補助額：" + koukin + "円<br>")

document.write("精算金額の総額：" + kasan + "円<br>")
      
document.write("一人当たりの分担：" + buntan + "円<br>")

document.write("<br>支払った人への払い戻し金額は<br>")
    for (var i=0; i<menu.length; i++){
      document.write(nama[i] + "さん：" + wari[i] + "円 <br>")
    }";
      document.getElementById('edit_area').innerHTML = str ;
    }
*/

document.write("各自の支払金額は<br>")
    for (var i=0; i<menu.length; i++){
      document.write(nama[i] + "さん：" + menu[i] + "円 <br>")
    }

document.write("<br>経費の総額：" + kasann + "円<br>")
      
document.write("公金補助額：" + koukin + "円<br>")

document.write("精算金額の総額：" + kasan + "円<br>")
      
document.write("一人当たりの分担：" + buntan + "円<br>")

document.write("<br>支払った人への払い戻し金額は<br>")
    for (var i=0; i<menu.length; i++){
      document.write(nama[i] + "さん：" + wari[i] + "円 <br>")
    }
document.write ("<br>以上、お帰りも気を付けて、来年も元気に再開～(^^)/<br><br>");
    
var str = "戻る";
document.write(str.link("https://sajyan.github.io/seisan_2/"));

}
    
    </script>
    
<ul>
    <li>算出結果を以下の表に記録できます。（IE未対応）</li>
    <li>記録表には表計算機能( = + - * / )があります。</li>
    <li>記録表の内容は、お使いのPCのブラウザ内に保存されます。（ほかの人には見えません）</li>
</ul>

      
        <table>
        <script type="text/javascript">  



for (var i=0; i<32; i++) {
    var row = document.querySelector("table").insertRow(-1);
    for (var j=0; j<15; j++) {
        var letter = String.fromCharCode("A".charCodeAt(0)+j-1);
        row.insertCell(-1).innerHTML = i&&j ? "<input id='"+ letter+i +"'/>" : i||letter;
    }
}

var DATA={}, INPUTS=[].slice.call(document.querySelectorAll("input"));
INPUTS.forEach(function(elm) {
    elm.onfocus = function(e) {
        e.target.value = localStorage[e.target.id] || "";
    };
    elm.onblur = function(e) {
        localStorage[e.target.id] = e.target.value;
        computeAll();
    };
    var getter = function() {
        var value = localStorage[elm.id] || "";
        if (value.charAt(0) == "=") {
            with (DATA) return eval(value.substring(1));
        } else { return isNaN(parseFloat(value)) ? value : parseFloat(value); }
    };
    Object.defineProperty(DATA, elm.id, {get:getter});
    Object.defineProperty(DATA, elm.id.toLowerCase(), {get:getter});
});
(window.computeAll = function() {
    INPUTS.forEach(function(elm) { try { elm.value = DATA[elm.id]; } catch(e) {} });
})();
    
        </script>
        </table>
        </section>

    <footer><p>Inspired by <a href="https://www.softantenna.com/wp/webservice/exel-with-javascript/">http://thomasstreet.net/blog/spreadsheet.html</a>. Features:</p></footer>

    
        </body>
    
</html> 
