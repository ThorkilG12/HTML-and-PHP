# Allow user to add new categories. Sanitize according to my rules:

* Remove characters that cannot be part of names or places. Like # ¤ % & ? = < ] etc...
* Uppercase first letter
* Allow UTF-8 (All countries in Europe should be possible)
* Use semi-colon as delimiter in input
* Remove comma
* Resulting string should de comma delimited
* Turn multi-space into single space
* Trim
* Allow categories to start with number

![From dirty to clean](https://github.com/ThorkilG12/HTML-and-PHP/blob/master/Fun%20with%20Clean%20Categories/p1.jpg "From Dirty to Clean and Delimited")

## The code
```html
<!DOCTYPE html>
<html>
<title>Fun with Categories</title>
<meta name="viewport" content="width=device-width, initial-scale=1">
<body>
<p><input type="text" id="inp" placeholder="Enter cats - use semicolon as delimiter" size="100"></p>
<button type="button" onclick="update()">Request data</button>
<p id="result"></p>
<script>
"use strict"
document.getElementById("inp").value = "B:,.M¤%&/W ;λgreek;;;бжЖrussian;H<>ell\oj;com,m()/a; Łó*dź ;1 spc;3   spc;æøå danish ;Euro€ "
function update() {
  var postdata = (document.getElementById("inp").value.replace(",", "").split(';').filter(Boolean)).map(s => s.trim());
  console.log(postdata)
  var xhttp = new XMLHttpRequest();
  xhttp.onreadystatechange = function() {
    if (this.readyState == 4 && this.status == 200) {
      document.getElementById("result").innerHTML = JSON.parse(this.responseText);
    }
  };
  xhttp.open("POST", "funWithCleanCats.php", true);
  xhttp.setRequestHeader("Content-Type", "application/json"); 
  xhttp.send(JSON.stringify({"cats":postdata}));
}
</script>
</body>
</html>
```
```php
<?php
header("Content-Type: application/json"); 
$jsonData = json_decode(file_get_contents("php://input"));
$arrFromHtml = $jsonData->cats;
$cleanCats = array_map(function ($element) { 
	$clean = preg_replace('~[^\p{L}\d\s]+|(\s)+~u','$1', $element);
	// You can allow tex. 'dot' and 'at' like this:  [^\p{L}\d\s.@]
	return mb_strtoupper(mb_substr($clean, 0, 1)) . mb_substr($clean, 1);
}, $arrFromHtml);
echo json_encode('*' . strip_tags(implode(',', $cleanCats)) . '*');
```
/T
