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

