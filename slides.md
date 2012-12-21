# PHP - правильный путь

!SLIDE

# PHP 
## правильный путь

!SLIDE

# Экскурс в историю

!SLIDE

* **PHP/FI (1995)**
  * HTML шаблонизатор и обработчик форм

* **PHP/FI 2.0 (1997)**
  * Тоже что и первое, но быстрее

* **PHP 3 (1998)**
  * Новое API
  * Расширение ядра модулями

!SLIDE

* **PHP 4 (2000)**
  * Zend Engine
  * Первый шаблонизатор на шаблонизаторе (Smarty)

* **PHP 5**
  * Быстрее, выше, сильнее
  * ООП
  * ФП
  * Трейты

* **PHP 6?**

!SLIDE

# Абсолтно верного пути нет

## есть Best Practice

!SLIDE

# #1 Будь в теме

# &nbsp;

* Следи за миром вокруг

* Используй только последнюю версию **PHP (5.4)**

* Примененяй новые фишки языка на практике

* Изучай новые пути решения старых задач

!SLIDE

# #2 Используй ООП

##   

* Абстрактные классы и Интерфейсы
* <s>Наследование</s>
* Трейты

!SLIDE

# #3 Используй ФП

##  

* Рекурсия 
* Функции высшего порядка
* Замыкания

!SLIDE

# #4 Метапрограммируй

##  

* Reflection API
* Magic Methods

!SLIDE

# #5 Делай по стандарту

## PSR, PSR-1, PSR-2

*http://www.php-fig.org/*

*by PHP Framework Interop Group*

!SLIDE

* **PSR-0:** пространства имён 
* **PSR-1:** стандартные элементы кода 
* **PSR-2:** расширенные и частные случаи PSR-1

!SLIDE

# #6 Автоматизируй стандартизацию

## PHP Coding Standards Fixer

*http://cs.sensiolabs.org/*

!SLIDE

# #7 Пиши документацию

## PHPDoc

*http://www.phpdoc.org/*

!SLIDE

# Хорошо

@@@ php

<?php
/**
 * Translate array.
 *
 * @param  array  $array         Array with source text to translate
 * @param  string $fromLanguage  Source language
 * @param  string $toLanguage    Destenation language
 * @param  bool   $translit      If true function return transliteration of source text 
 * @return array|bool            Array  with translated text or false if exists errors
 */     
public function translateArray($array, $fromLanguage = "en", $toLanguage = "ru", $translit = false) 
{
	if (empty($this->_errors)) {
		$text = implode("[<#>]", $array);
		$response = $this->translateText($text, $fromLanguage, $toLanguage, $translit);
		return $this->_explode($response);
	} else {
		return false;
	}
}
@@@

!SLIDE

# Плохо

@@@ php

<?php

//
// Function to translate array.
//    
public function translateArray($array, $fromLanguage = "en", $toLanguage = "ru", $translit = false) 
{
	if (empty($this->_errors)) {
		$text = implode("[<#>]", $array);
		$response = $this->translateText($text, $fromLanguage, $toLanguage, $translit);
		return $this->_explode($response);
	} else {
		return false;
	}
}
@@@

!SLIDE

# Очень плохо

@@@ php

<?php
/*
    .___________..______           ___      .__   __.      _______. __      
    |           ||   _  \         /   \     |  \ |  |     /       ||  |     
    `---|  |----`|  |_)  |       /  ^  \    |   \|  |    |   (----`|  |     
        |  |     |      /       /  /_\  \   |  . `  |     \   \    |  |     
        |  |     |  |\  \----. /  _____  \  |  |\   | .----)   |   |  `----.
        |__|     | _| `._____|/__/     \__\ |__| \__| |_______/    |_______|
                                                                            
                      ___   .___________. _______      _______.
                     /   \  |           ||   ____|    /       |
                    /  ^  \ `---|  |----`|  |__      |   (----`
                   /  /_\  \    |  |     |   __|      \   \    
                  /  _____  \   |  |     |  |____ .----)   |   
                 /__/     \__\  |__|     |_______||_______/    
                                                               
             ___      .______      .______           ___   ____    ____ 
            /   \     |   _  \     |   _  \         /   \  \   \  /   / 
           /  ^  \    |  |_)  |    |  |_)  |       /  ^  \  \   \/   /  
          /  /_\  \   |      /     |      /       /  /_\  \  \_    _/   
         /  _____  \  |  |\  \----.|  |\  \----. /  _____  \   |  |     
        /__/     \__\ | _| `._____|| _| `._____|/__/     \__\  |__|     
*/
public function translateArray($array, $fromLanguage = "en", $toLanguage = "ru", $translit = false) 
{
	if (empty($this->_errors)) {
		$text = implode("[<#>]", $array);
		$response = $this->translateText($text, $fromLanguage, $toLanguage, $translit);
		return $this->_explode($response);
	} else {
		return false;
	}
}
@@@

!SLIDE

# #8 Управляй зависимостями

##  

* Ваш проект зависит от нескольких библиотек

* ...которые зависят от других библиотек

* ...которые конфликтуют с определёнными версиями предыдущих библиотек

!SLIDE

## Хватит это терпеть!

<img src='images/998990.jpg' />

!SLIDE

## Composer
*http://getcomposer.org/*

## <s>PEAR</s>

!SLIDE

Ставим:

@@@ sh
curl -s https://getcomposer.org/installer | php
@@@

Пишем, что хотим в `composer.json`:

@@@ json
{
    "require": {
        "monolog/monolog": "1.2.*"
    }
}
@@@

Устанавливаем:

@@@ sh
php composer.phar install
@@@

Подключаем в проект:

@@@ php
<?php
require 'vendor/autoload.php';
@@@

!SLIDE

# #9 Сравнивай чётко

##   

@@@ php
<?php
$a = 5;   // 5 as an integer

var_dump($a == 5);       // compare value; return true
var_dump($a == '5');     // compare value (ignore type); return true
var_dump($a === 5);      // compare type/value (integer vs. integer); return true
var_dump($a === '5');    // compare type/value (integer vs. string); return false

/**
 * Strict comparisons
 */
if (strpos('testing', 'test')) {    // 'test' is found at position 0, which is interpreted as the boolean 'false'
    // code...
}

vs.

if (strpos('testing', 'test') !== false) {    // true, as strict comparison was made (0 !== false)
    // code...
}
@@@

!SLIDE

# #10 Склеивай красиво

##   

@@@ php
<?php
	$a  = 'Multi-line example';    // concatenating assignment operator (.=)
	$a .= "\n";
	$a .= 'of what not to do';

// vs.

	$a = 'Multi-line example'      
	    . "\n"                     
	    . 'of what to do';
@@@

!SLIDE

# #11 ...или вообще не склеивай

##   

@@@ php
<?php
	echo 'phptherightway is ' . $adjective . '.'
	    . "\n"
	    . 'I love learning' . $code . '!';

// vs.

	echo "phptherightway is $adjective.\n I love learning $code!"
@@@

@@@ php
<?php
	$juice = array('apple', 'orange', 'plum');

	echo 'I drank some juice made of ' . $juice[1]} 's';

// vs.

	echo "I drank some juice made of {$juice[1]}s";
@@@

!SLIDE

# #12 Не пиши else лишний раз

##   

@@@ php
<?php
function test($a)
{
    if ($a) {
        return true;
    } else {
        return false;
    }
}

// vs.

function test($a)
{
    if ($a) {
        return true;
    }
    return false;
}
@@@

!SLIDE

@@@ php
<?php
function test($a)
{
    if ($a) {
        return $a;
    } else {
        return false;
    }
}

// vs.

function test($a)
{
    $b = false;

    if ($a) {
        $b = $a
    }

    return $b;
}
@@@

!SLIDE

# #13 Используй jQuery стиль

##   

@@@ php
<?php
    $_data = array (
        'addon' => $addon_scheme->getId(),
        'priority' =>  $addon_scheme->getPriority(),
    );

    db_query("REPLACE INTO ?:addon_descriptions ?e", array(
        'lang_code' => $translation['lang_code'],
        'addon' =>  $addon_scheme->getId(),
        'name' => $translation['value'],
        'description' => $translation['description']
    ));

    return array(
        'status' => Response::STATUS_OK,
        'data' => array(
            'settings' => $result,
            'search' => $params
        )
    );
@@@

!SLIDE

# #14 Лови - бросай

## 

@@@ php
	<?php
	$email = new Fuel\Email;
	$email->subject('My Subject');
	$email->body('How the heck are you?');
	$email->to('guy@example.com', 'Some Guy');

	try
	{
	    $email->send();
	}
	catch(Fuel\Email\ValidationFailedException $e)
	{
	    // The validation failed
	}
	catch(Fuel\Email\SendingFailedException $e)
	{
	    // The driver could not send the email
	}
@@@

!SLIDE

# #15 БазДань правильно

## PDO

@@@ php
	<?php
	$pdo = new PDO('sqlite:users.db');
	$stmt = $pdo->prepare('SELECT name FROM users WHERE id = :id');
	$stmt->bindParam(':id', $_GET['id'], PDO::PARAM_INT); //<-- Automatically sanitized by PDO
	$stmt->execute();
@@@

## Aura SQL
## Doctrine2 DBAL
## ZF Db

!SLIDE

# #16 Защищай

## OWASP Security Guide

*https://www.owasp.org/index.php/Guide_Table_of_Contents*

!SLIDE

# #17 Фильтруй

## strip_tags
## htmlspecialchars
## htmlentities

!SLIDE

# #17 Тестируй

## PHPUnit

*http://www.phpunit.de/manual/current/en/* 

## Selenium

*http://seleniumhq.org/*

## Behat

*http://behat.org/*

!SLIDE

# #18 Деплой

## Capistrano

*https://github.com/capistrano/capistrano*

## Chef 

*http://www.opscode.com/chef/*

!SLIDE

# #18 Пиши **** код!

<img src="images/bl.jpg" height="500px"/>

!SLIDE

# Спасибо!

## http://8xx8.ru
## @8xx8ru
## avk@8xx8.ru