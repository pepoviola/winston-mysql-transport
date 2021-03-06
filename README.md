A Mysql transport for [winston][0].

## Installation

### Installing winston-mysql-transport via npm

``` sh
  $ npm install winston
  $ npm install winston-mysql-transport
```
(or add it to your package.json)

## Usage

First you must generate your log table

``` sql
/*file : extras/schema.sql*/
CREATE TABLE IF NOT EXISTS `my_database`.`log_table` (
	`id` int(10) NOT NULL AUTO_INCREMENT,
	`level` varchar(45) NOT NULL,
	`message` text NOT NULL,
	`timestamp` datetime NOT NULL,
	`meta` varchar(255),
  `meta_stack` text NOT NULL,
	`hostname` varchar(255),
	PRIMARY KEY (`id`)
);
```

And in your code...

``` js
  var winston = require('winston');
  
  //
  // Requiring `winston-mysql-transport` will expose
  // `winston.transports.Mysql`
  //
  require('winston-mysql-transport').Mysql;
  
  options = {
  	database : "my_database",
  	table : "log_table",
  	user : "root"
  }
  
  winston.add(winston.transports.Mysql, options);
```

You can find a list of options that you can pass here :

[https://github.com/felixge/node-mysql#connection-options][1]

## Unsupported
This transport does not support (yet) :

* **streaming**
* **querying**
* **Saving of metadata (implement stack saving only)** 

[0]: https://github.com/flatiron/winston
[1]: https://github.com/felixge/node-mysql#connection-options
