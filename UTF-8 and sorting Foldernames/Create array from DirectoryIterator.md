### As always, there are problems with locale letters here in Euro-land
Let's get somo data. I'm using a folder on a windows PC localized for Denmark.
What you see below is the right way to sort.

I'm using the city of Łódź to have some characters that is outside the Western codepage that was mostly used some deecades ago. Notice how Aberdeen and the danish city Aalborg are sorted. From old time, the "double a" was used insteadt of Å. The "double a" is pronounced as Å. T the end of the danish alfabeth is ...STUVWXYZÆØÅ.
The Euro symbol is the only character in this demo that accupy three bytes. 

<img src="https://github.com/ThorkilG12/HTML-and-PHP/blob/master/UTF-8%20and%20sorting%20Foldernames/image.png" width="40%">

#### Let's create a PHP array:
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


