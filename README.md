# jquery-basic-metods
Bu jquery kütüphanesinin temel metotlarını içeren Türkçe belge niteliğinde hazırlanmış notlardan oluşur. Metotlar, tanımları ve kullanım örneklerinden oluşur. Hazırlayan @burakkrt 

# JQuery Library

İstemci tarafında çalışan javascript kütüphanesidir. Daha hızlı javascript yazmamıza olanak tanır. Basit yazılır ve hızlı sonuç alınır. JQuery ‘de bir elementi doğru seçmek neredeyse yapılacak işlemin büyük bir kısmını tamamlamak demektir.

### Başlarken

```jsx
$(document).ready(function () {
     console.log("hello jquery")
})
```

```jsx
 $(function () {
     console.log("hello jquery 2")
 })
```

### Elementleri yakalamak (class, id ..vb)

```jsx
<p id="test">Lorem ipmus ...</p> 

$("#test")  //bu şekilde yakalayabiliriz.
JQuery("#test")  //alternatif olarak bu şekilde yakalanabilir.

$("div#test") //bu şekilde alt alta sorug eklenebilir
```

### css()

```jsx
<p id="text">Lorem ipsum dolor sit amet</p>

$("#text").css("color","red"); // stil atamak

$("#text").css({
		color: "red",   // birden fazla stil atamak (camel case yapısında key)
		fontWeight: "bold"
}) 

let color = $("#text").css("color"); // stil özelliğini almak. result red;
```

### addClass()

```jsx
<p id="text">Lorem ipsum dolor sit amet</p>

$("#text").addClass("active") //active  class 'ı ekle
$("#text").addClass(["active","btn"])  //birden fazla class ekle
```

### children()

```jsx
<ul id="list">
    <li class="list-item">Apple</li>
    <li class="list-item">Samsung</li>
    <li class="list-item">Xiaomi</li>
    <li class="list-item">Huawei</li>
    <li class="list-item">General Mobile</li>
</ul>

$(function () {
    let element = $("#list")
		
		element.children() //return all children array [li,li,li...]
		element.children(":first") //return Apple element
		element.children(":last") //return General Mobile
		element.children(":nth-child(3)") //return  Xiaomi
		element.children("last").parent() //return ul
})
```

### siblings()

```jsx
<ul id="list">
    <li class="list-item">Apple</li>
    <li class="list-item">Samsung</li>
    <li class="list-item" id="xia">Xiaomi</li>
    <li class="list-item">Huawei</li>
    <li class="list-item">General Mobile</li>
</ul>

$(function(){
		$("#xia").siblings() //return xiaomi haric eşdeğer tüm li etiketleri
		$("#xia").siblings(":first") // return Apple element
		$("#xia").siblings().css("background-color","red") // xiaomi haric hepsi kırmızı
})
```

### Öznitelik Seçici

```jsx
<h1 id="title">Merhaba Jquery</h1>
<h1>Merhaba Jquery</h1>

$(function () {
	$("h1[id]").css("color","red")  //tüm h1 lerden id attribute si olanları al.
	$("h1[id][class]").css("color","red") //hem id si hemde class 'ı olan tüm h1 ler
	$("h1[id=test]").css("color","red")  //id si test olan h1 ler
	$("h1[class^=c]").css("color","red")  //class 'ı c harfi ile başlayan h1 ler
	$("h1[class&=c]").css("color","red")  //class 'ı c ile biten h1 ler
	$("h1[class*=item][id=title]").css("color","red") //class 'ın içinde item kelimesi geçen ve id si title olan h1
	$("#list li[class=list-item]").css("color","red") //list id li elementin altındaki li elemenletinde class 'ı list-item olanlar
})
```

### *Not : .click() kaldırıldı*

```jsx
$("test").click(function() {...}) //kaldırıldı
$("test").on("click", function() {...})  //artık bu şekilde
```

### nth-child

```jsx
<ul>
    <li>Lorem ipsum</li>
    <li>This</li>
    <li>Lorem ipsum</li>
    <li>Lorem ipsum</li>
</ul>

$(function () {
  $("ul li:nth-child(2)")  //return this
})

$(function () {
  $("ul li:nth-child(event)")  /return 2,4. element çift
})
```

### text()

```jsx
<ul>
    <li>Lorem ipsum</li>
    <li>This</li>
    <li>Lorem ipsum</li>
    <li>Lorem ipsum</li>
</ul>

$(function () {
  $("ul").text()  // ul elementinin içerisindeki tüm textlere ulaşır
	$("ul").text("texttt")  // ul elementininiçerise texttt ekler (tüm li elemnetleri silinir)
})
```

### html()

```jsx
<ul>
    <li>Lorem ipsum</li>
    <li>This</li>
    <li>Lorem ipsum</li>
    <li>Lorem ipsum</li>
</ul>

$(function () {
  $("ul").html("<a href='https://google.com'>Go Google</a>")
})
```

### append()   (sonuna element ekle)

```jsx
<ul>
    <li>Lorem ipsum</li>
    <li>This</li>
    <li>Lorem ipsum</li>
    <li>Lorem ipsum</li>
</ul>

$(function () {
  $("ul").append("<a href='https://google.com'>Go Google</a>") //sonuna elementi ekle
})
```

### prepend()   (başına element ekle)

```jsx
<ul>
    <li>Lorem ipsum</li>
    <li>This</li>
    <li>Lorem ipsum</li>
    <li>Lorem ipsum</li>
</ul>

$(function () {
  $("ul").prepend("<a href='https://google.com'>Go Google</a>") //başına elementi ekle
})
```

### append()   fonksiyon ile çalıştırma

```jsx
<ul>
    <li>Lorem ipsum</li>
    <li>This</li>
    <li>Lorem ipsum</li>
    <li>Lorem ipsum</li>
</ul>

$(function () {
  $("ul").append(function (index, value) {
			return ` - ${index}`    //tüm li elementlerinin sonuna - 0 , - 1 ... diye index numaralarını ekler
	})
})

$(function () {
  $("ul").append(function (index, value) {
			return `${value}` //tüm li elementlerinin bir kere daha aynı içeriği ekler
	})
})

//yada prepend ile başına ekleyebiliriz.
```

### appendTo() veya prependTo()

```jsx
<ul>
    <li>Lorem ipsum</li>
    <li>This</li>
    <li>Lorem ipsum</li>
    <li>Lorem ipsum</li>
</ul>

$(function () {
  $("<span>test message</span>").appendTo($("ul")) //ul nin sonuna ekle
})

$(function () {
  $("<span>test message</span>").prependTo($("ul")) //ul nin başına ekle
})
```

### after() ve before()

```jsx
<ul>
    <li>Lorem ipsum</li>
    <li>This</li>
    <li>Lorem ipsum</li>
    <li>Lorem ipsum</li>
</ul>

$(function () {
  $("ul").after("<div>test content</div>")  //ul elementinden sonra ekle
	 $("ul").before("<div>test content</div>")  //ul elementinden önce ekle
})

```

### remove()

```jsx
<ul>
    <li>Lorem ipsum</li>
    <li>This</li>
    <li>Lorem ipsum</li>
    <li>Lorem ipsum</li>
</ul>

$(function () {
  $("ul li:nth-child[2]").remove()  //this adlı li elementini dom 'dan siler
})
```

### empty()

```jsx
<ul>
    <li>Lorem ipsum</li>
    <li>This</li>
    <li>Lorem ipsum</li>
    <li>Lorem ipsum</li>
</ul>

$(function () {
  $("ul").empty()  //ilgili elementin içeriğini siler return <ul></ul>
})
```

### clone()

```jsx
<ul>
    <li>Lorem ipsum</li>
    <li>This</li>
    <li>Lorem ipsum</li>
    <li>Lorem ipsum</li>
</ul>

$(function () {
  let kopya = $("ul li:nth-child[2]").clone(); //ilgili elementi alt elementleri ile birlikte kopyaladık.
	kopya.appendTo($("ul"))  //kopyalanan elementi ul elementinin en sonuna ekledik.
})
```

### wrap()

```jsx
<ul>
    <li>Lorem ipsum</li>
    <li>This</li>
    <li>Lorem ipsum</li>
    <li>Lorem ipsum</li>
</ul>

$(function () {
  $("ul li:nth-child[2]").wrap("<div></div>") //this elementini div etiketleri ile sar
})

//return
<ul>
    <li>Lorem ipsum</li>
		<div>
	    <li>This</li>
		</div>
    <li>Lorem ipsum</li>
    <li>Lorem ipsum</li>
</ul>
```

### wrapAll()

```jsx
<ul>
    <li id="no1">Text no1</li>
    <li id="no2">Text no2</li>
    <li id="no3">Text no3</li>
    <li id="no4">Text no4</li>
</ul>

$(function () {
  $("#no1 , #no2, #no4").wrap("<div></div>") //biren çok elementi div etiketleri ile sar
})

//result 
<ul>
		<div>
	    <li id="no1">Text no1</li>
	    <li id="no2">Text no2</li>
      <li id="no3">Text no4</li>
		</div>
			<li>Text no3</li>
</ul>
```

### wrapInner()   - içeriyi sarmala

```jsx
<ul>
    <li id="no1">Text no1</li>
    <li id="no2">Text no2</li>
    <li id="no3">Text no3</li>
    <li id="no4">Text no4</li>
</ul>

$(function () {
  $("#no3").wrap("<div></div>") //elementin içerisindekileri sar
})

//result 
<ul>
		<li id="no1">Text no1</li>
    <li id="no2">Text no2</li>
    <li id="no3">
			<div>Text no3</div>
		</li>
    <li id="no4">Text no4</li>
</ul>
```

### attr()

```jsx
 <img src="test.jpg" width="150px" class="img img-fuild" />

$(function () {
  $("img").attr("src")  //return test.jpg  //ilgili elementin src attribute sini getir
	$("img").attr("src","test2.jpg")  //src attributesini test2.jpg olarak değiştir.
	// aynı anda birden fazla attribute değiştir
	$("img").attr({src: "test2.jpg", width:"175px"}) 
})
```

### removeAttr()

```jsx
 <img src="test.jpg" width="150px" class="img img-fuild" />

$(function () {
  $("img").removeAttr("src") //src attribute 'nu siler.
})
```

### find()

```jsx
<ul>
    <li id="no1">Text no1</li>
    <li id="no2">Text no2</li>
    <li id="no3"><span>hello jquery</span>Text no3</li>
    <li id="no4">Text no4</li>
</ul>

$(function () {
		$("ul").find("span")  //return array [<span>hello jquery</span>]
})
```

### eq()

```jsx
<ul>
    <li id="no1">Text no1</li>
    <li id="no2">Text no2</li>
    <li id="no3">Text no3</li>
    <li id="no4">Text no4</li>
</ul>

$(function () {
		$("ul li").eq(2)  //return Text no3 element
//yada
		$("ul li:eq(2)") // bu şekilde seçici içerisinde de kullanabiliriz.
})
```

### first()  ve  last()

```jsx
	<ul>
    <li id="no1">Text no1</li>
    <li id="no2">Text no2</li>
    <li id="no3">Text no3</li>
    <li id="no4">Text no4</li>
</ul>

$(function () {
		$("ul li").fist()  //return array Text no1 element
//yada
		$("ul li:first") // bu şekilde seçici içerisinde de kullanabiliriz.
//last
		$("ul li").last()  //return array Text no4 element
//yada
		$("ul li:last") // bu şekilde seçici içerisinde de kullanabiliriz.
})
```

### odd()  ve  even()

```jsx
	<ul>
    <li id="no1">Text no1</li>
    <li id="no2">Text no2</li>
    <li id="no3">Text no3</li>
    <li id="no4">Text no4</li>
</ul>

$(function () {
		$("ul li").odd()  //return text no2, text no4  (tek index numaraları)
//yada
		$("ul li:odd") // bu şekilde seçici içerisinde de kullanabiliriz.
//last
		$("ul li").even()  //return array Text no1, text no 3 (çift index numaraları)
//yada
		$("ul li:even") // bu şekilde seçici içerisinde de kullanabiliriz.
})
```

### contains()

```jsx
	<ul>
    <li id="no1">Text no1</li>
    <li id="no2">Text no2</li>
    <li id="no3">Text no3</li>
    <li id="no4">Text no4</li>
</ul>

$(function () {
		$("ul li:contains('Text no3')")  //return array in text no3 element
})
```

### has()

```jsx
	<ul>
    <li id="no1">Text no1</li>
    <li id="no2">Text no2</li>
    <li id="no3"><span>hello</span>Text no3</li>
    <li id="no4">Text no4</li>
		<span>hello 2</span> //burayı görmez çünkü sadece ul nin altındaki li lerin içinde arar.
</ul>

$(function () {
		$("ul li").has("span").css("color","red")  //ul li nin altında span etiketi varsa bul ve rengini kırmızı ya çevirir.

		$("ul li:has("span")").css("color","red") //seçici içerisinde kullanılabilir
})
```

### not()

```jsx
	<ul>
    <li id="no1">Text no1</li>
    <li id="no2">Text no2</li>
    <li id="no3"><span>hello</span>Text no3</li>
    <li id="no4">Text no4</li>
</ul>

$(function () {
		$("ul li").not("span").css("color","red")  //ul li nin altında span etiketi hariç herşeyi seçer.

		$("ul li:not("span")").css("color","red") //seçici içerisinde kullanılabilir
})
```

### :empt

```jsx
	<ul>
    <li id="no1">Text no1</li>
    <li id="no2">Text no2</li>
    <li id="no3"></li>      //this element is empty, background-color red
    <li id="no4">Text no4</li>
</ul>

$(function () {
		$("ul li:empty").css("background-color","red") //içeriği boş olan elementi seçer
})
```

### next() ,  prev() ,  nextAll()  ,  prevAll()

```jsx
	<ul>
    <li id="no1">Text no1</li>
    <li id="no2">Text no2</li>
    <li id="no3">Text no3</li>
    <li id="no4">Text no4</li>
</ul>

$(function () {
		$("ul li").first().next()  //return Text no2 element
		$("ul li").last().prev()  //return Text no3 element

		$("ul li").first().nextAll()  //return array text no2, text no3, text no4
		$("ul li").last().prevAll()  //return array text no3, text no2, text no1
})
```

### parent()

```jsx
	<ul>
    <li id="no1">Text no1</li>
    <li id="no2">Text no2</li>
    <li id="no3">Text no3</li>
    <li id="no4">Text no4</li>
</ul>

$(function () {
		$("ul li").parent()  //return ul element
})
```

### position()

```jsx
	<ul style="position: relative">
    <li id="no1">Text no1</li>
    <li id="no2">Text no2</li>
    <li id="no3">Text no3</li>
    <li id="no4">Text no4</li>
	</ul>

$(function () {
		$("ul li:nth-child(2)").position()  //return object {top: "..", left: ".."}
})
```

### offset()

```jsx
	<ul>
    <li id="no1">Text no1</li>
    <li id="no2">Text no2</li>
    <li id="no3">Text no3</li>
    <li id="no4">Text no4</li>
	</ul>

$(function () {
		$("ul li:nth-child(2)").offset()  //return object {top: "..", left: ".."}
})
```

### scrollTop()  ,  scrollLeft()

```jsx
$(function () {
		$("window").scrollTop() //return scroll 'un o anki dikey konumu
		$("window").scrollLeft() //return scroll 'un o anki yatay konumu

		$("window").scrollTop(200) //scroll 'u 200 birim aşağıya kaydır
		$("window").scrollLeft(400) //scroll 'u 400 birim yana kaydır kaydır
})

//scroll barı izleyecek event listener ekle ve scrollbar 'ın konumu her değiştiğinde yaz
$(window).on("scroll", function(){
     console.log($(this).scrollTop())
})
```

### width()  ,  height()

```jsx
<div id="box" style="width: 150px; height: 200px; border: 5px solid red; padding: 5px">

$("#box").width()  //result 130px , iki taraftan 10px border 10px padding 'i çıkartır
$("#box").height()  //resut 180px , aynı şekilde border ve padding kırpar
$("#box").width(500)  //elementin uzunluğunu 500px yaptık.
```

### innerWidth()  ,  innerHeight()

```jsx
<div id="box" style="width: 150px; height: 200px; border: 5px solid red; padding: 5px">

$("#box").innerWidth()  //result 140px , sadece border 'ı alarak kırpar
$("#box").innerHeight()  //resut 190px , aynı şekilde borderleri kırparak ana değeri verdi

$("#box").innerWidth(500)  //elementin uzunluğunu 500px yaptık.
```

### outerWidth()  ,  outerHeight()

```jsx
<div id="box" style="width: 150px; height: 200px; border: 5px solid red; padding: 5px">

$("#box").innerWidth()  //result 150px , hiçbir border, padding gibi değeri katma
$("#box").innerHeight()  //resut 200px 

$("#box").innerWidth(500)  //elementin uzunluğunu 500px yaptık.
```

### each()

```jsx
let arr = ["Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday"];

$.each(arr, (index, value) =>{
     console.log($(this))
 })

// yada bu şekilde kullanılabilir
$(arr).each((index,value) => {...})
```

### map()

```jsx
let arr = ["Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday"];

 let res = $.map(arr, (value) =>{
     return value
 })

console.log(res)

// yada bu şekilde kullanılabilir
$(arr).map((index,value) => {...})
```

### filter()

```jsx
let arr = ["Monday","Tuesday","Wednesday","Thursday","Friday","Saturday","Sunday"];

 let res = arr.filter((value) =>{
     return value.length > 8
 })

console.log(res) //return "Wednesday"  , normal javascript filter methodu
```

### Mouse Events

[**Go to jQuery Official Docs**](https://api.jquery.com/category/events/mouse-events/)

| pageX , pageY | Sayfadaki x ve y eksenine göre konumunu döndürür. (kapsayıcı sayfadır) |
| --- | --- |
| screenX , screenY | tarayıcı dışında tüm ekrana göre x ve y konumunu döndürür (kapsayıcı ekran) |

### mousemove()

```jsx
<div id="tt" class="position-absolute bg-success rounded-pill" style="width: 15px; height: 15px; transform: translate(-50%, -50%)"></div>

$(document).on("mousemove", function(e) {
    $("#tt").css({
        top: e.pageY,
        left: e.pageX
    })
})
```

### trigger()

```jsx
<input type="text" id="input" />

$("#input").trigger("focus")
```

### one()

```jsx

$(document).one("mousemove", function(e) {
    console.log(e.pageX + e.pageY)
})
```
