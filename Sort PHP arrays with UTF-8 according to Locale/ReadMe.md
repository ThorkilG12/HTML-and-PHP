### As always, there are problems with locale letters here in Euro-land
Let's get somo data. I'm using a folder on a windows PC localized for Denmark.
The image below - from Windows Explorer - is the right way to sort.

I'm using the city of Łódź to have some characters that is outside the Western codepage that was mostly used some deecades ago. Notice how Aberdeen and the danish city Aalborg are sorted. From old time, the "double a" was used insteadt of Å. The "double a" is pronounced as Å. The end of the danish alfabeth is ...STUVWXYZÆØAAÅ. Notice the "double A" between Ø and Å. 
The Euro symbol is the only character in this demo that accupy three bytes. 

<img src="https://github.com/ThorkilG12/HTML-and-PHP/blob/master/Sort%20PHP%20arrays%20with%20UTF-8%20according%20to%20Locale/image.png" width="40%">


#### Let's create a PHP array:
##### PHP 7.4 - Apache 2.4 - Windows 2012R2 
```php
$di = new DirectoryIterator('C:\SetupInfo\cities');
$allFiles = array();
foreach ($di as $fileinfo) {
  if (!$fileinfo->isDot()) {
		array_push($allFiles,	['name'	=>$fileinfo->getBasename(), 
			'length'		=>strlen($fileinfo->getBasename()),
			'okLength'		=>mb_strlen($fileinfo->getBasename()),
			'modDate'		=>date('Y-m-d_H:i:s', $fileinfo->getMTime()), 
			'type'	=>$fileinfo->isDir() ? 'Dir' : 'File',
			'ext'	=>$fileinfo->getExtension()
		]);
	}
}
echo "<pre>";echo "DirIterate: ";print_r($allFiles);echo "</pre>";
```
Now we have an array, and we can sort it by using this function:
```php
function utf8_sort_by_column(&$arr, $col) {
    $sort_col = array();
    foreach($arr as $key=>$row) {
        $sort_col[$key] = $row[$col];
    }
	collator_asort(collator_create(''), $sort_col);	
	$result = array();
	foreach($sort_col as $key=>$row) {
		array_push($result, $arr[$key]);
	}	
	return $result;
}
# Call the function and create the '$sorted' array;
$sorted = utf8_sort_by_column($allFiles, 'name');
```
Let's print the see that the order is correct. and that the 'mb_strlen()' does it's job.
```
array_map(function ($e) {echo $e['name'], ' ', $e['okLength'], '<br>';}, $sorted);
```
	€urocity 8
	Aberdeen 8
	city65001.txt 13
	createlist.cmd 14
	index.html 10
	Lodz 4
	Łódź 4
	part1.html 10
	part2.html 10
	Preußisch Oldendorf 19
	Überlingen 10
	zagre 5
	Zagreb 6
	Ælligelyng 10
	østerb 6
	Østerby 7
	Aalborg 7
	Ålestrup 8
The most important line, in all this, is this one: `collator_asort(collator_create('da'), $sort_col);`

Lot's of articles in StackOverflow is using the `array_multisort` function, but even if I use the `SORT_LOCALE_STRING` it does not sort correct.

My guess is that we need a MB_ version of `PHP array_multisort()`

I might have mis-understood something, so if anyone can use `PHP array_multisort()` to sort this ['ab','æa','øa','åa','aa','€u','Łó'] correct, please let me know.

Here you have the correct danish result: `€u,ab,Łó,æa,øa,aa,åa` 

/T
