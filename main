<?php

$rows = array_map('str_getcsv', file('input.csv'));

$header = array_shift($rows);
$data = array();

function rus2translit($string) {
    $converter = array(
        'а' => 'a',   'б' => 'b',   'в' => 'v',
        'г' => 'g',   'д' => 'd',   'е' => 'e',
        'ё' => 'e',   'ж' => 'zh',  'з' => 'z',
        'и' => 'i',   'й' => 'y',   'к' => 'k',
        'л' => 'l',   'м' => 'm',   'н' => 'n',
        'о' => 'o',   'п' => 'p',   'р' => 'r',
        'с' => 's',   'т' => 't',   'у' => 'u',
        'ф' => 'f',   'х' => 'h',   'ц' => 'c',
        'ч' => 'ch',  'ш' => 'sh',  'щ' => 'sch',
        'ь' => '',  'ы' => 'y',   'ъ' => '',
        'э' => 'e',   'ю' => 'yu',  'я' => 'ya',
        
        'А' => 'A',   'Б' => 'B',   'В' => 'V',
        'Г' => 'G',   'Д' => 'D',   'Е' => 'E',
        'Ё' => 'E',   'Ж' => 'Zh',  'З' => 'Z',
        'И' => 'I',   'Й' => 'Y',   'К' => 'K',
        'Л' => 'L',   'М' => 'M',   'Н' => 'N',
        'О' => 'O',   'П' => 'P',   'Р' => 'R',
        'С' => 'S',   'Т' => 'T',   'У' => 'U',
        'Ф' => 'F',   'Х' => 'H',   'Ц' => 'C',
        'Ч' => 'Ch',  'Ш' => 'Sh',  'Щ' => 'Sch',
        'Ь' => '',  'Ы' => 'Y',   'Ъ' => '',
        'Э' => 'E',   'Ю' => 'Yu',  'Я' => 'Ya', ' ' => '_',
    );
    return strtr($string, $converter);
}


foreach ($rows as $key_a => $row) {
	foreach ($row as $key => $value) {
		$data[$key][]= $value;
	}
	
}
foreach ($header as $key => $val) {

	$new_data[$val]=$data[$key];
}

foreach($new_data AS $s_header => $val) {	
	$xml = new DomDocument('1.0', 'UTF-8'); 
	$today = date("m.d.y");

	$list = $xml->createElement("list");	
	$listAttributeName = $xml->createAttribute('name');
	$listAttributePriora = $xml->createAttribute('priority');
	$listAttributeDate = $xml->createAttribute('date');
	$listAttributeFileName = $xml->createAttribute('filename');

	$translitFileName = rus2translit($s_header);
	$translitFileName = strtolower($translitFileName);
		
		foreach($val AS $field_name) {	
			if (!empty($field_name)) {			
				$name = $list->appendChild($xml->createElement("name",$field_name)); 
				$list->appendChild($name);
			} else {
				break;
			}
		}
	
	$listAttributeName->value = $s_header;	
	$listAttributePriora->value = '1';
	$listAttributeDate->value = $today;
	$listAttributeFileName->value = $translitFileName.'.xml';
	$list->appendChild($listAttributeName);
	$list->appendChild($listAttributePriora);
	$list->appendChild($listAttributeDate);
	$list->appendChild($listAttributeFileName);

	$xml->appendChild($list);

	$xml->formatOutput = true; 
	$xml->save($translitFileName.'.xml'); 

}

echo "ok";

?>
