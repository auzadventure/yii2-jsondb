Json Flat File 
===============
Extension to Add and Save a flat file json

Installation
------------

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
php composer.phar require --prefer-dist auzadventure/yii2-jsondb "*"
```

or add

```
"auzadventure/yii2-jsondb": "*"
```

to the require section of your `composer.json` file.


Usage
-----

Once the extension is installed, simply use it in your code by  :

```
<?php 
$json_path = Url::to('@app/path/json_file.json')

$jsonDB = \auzadventure\jsondb\JsonDB($json_path); 

It will save a record in the json format with a lastID 

{
    "data": {
        "1": {
            "date": "today",
            "msg": "milk is good"
        }
    },
    "conf": {
        "lastID": 1
    }
}

```


## Insert 

``` $jsonDB->insert($array) ```

## FindAll

``` $jsonDB->findAll() ```

## Find Field = Val 

``` ->find(string $field, string $val) 

# Find 

->findOne($id) 

```


## Sample Model to extend 

```
<?php 

namespace app\models;

use Yii;
use yii\base\Model;
use auzadventure\jsondb\JsonDB;
use yii\helpers\Url;


class Ads extends Model {
	
	public $title;
	public $url;
	public $blurp;
	
	public $filepath;
	public $jsondb; 
	public $id; 
	
	public function rules()
    {
        return [
            // name, email, subject and body are required
            [['title', 'url', 'blurp'], 'required'],
            
        ];
    }
	
	
	public function __construct() {
		$this->filepath = $this->getFilePath();
		$this->jsondb = new JsonDB($this->filepath);
	}
	
	
	public function getFilePath() {
		return Url::to('@app/data/ads.json');
	}
	
	
	public function findAll() {
		return $this->jsondb->findAll()->data;
	}
	
	public function save() {
		
		$file = self::getFilePath();
		
		$jsondb = new JsonDB($file);
		$jsondb->insert(['title'=>$this->title,
						 'url'=>$this->url,
						 'blurp'=>$this->blurp
						]);
			
	}
	
	public function delete($id) {
		return $this->jsondb->deleteByID($id);
	}

}
```
