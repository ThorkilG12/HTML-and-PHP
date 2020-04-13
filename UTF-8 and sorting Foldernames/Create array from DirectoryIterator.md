### As always, there are problems with locale letters here in Euro-land
Let's get somo data. I'm using a folder on a windows PC localized for Denmark




```php
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
```

