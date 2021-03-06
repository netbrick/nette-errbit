Nette Errbit (Airbrake) error logger
===================================

Errbit (Airbrake) error handler for nette applications.
For communication with errbit it use package [flippa/errbit-php](https://github.com/flippa/errbit-php). 

[![Latest Stable Version](https://poser.pugx.org/netbrick/nette-errbit/v/stable.svg)](https://packagist.org/packages/netbrick/nette-errbit)
[![Latest Unstable Version](https://poser.pugx.org/netbrick/nette-errbit/v/unstable.svg)](https://packagist.org/packages/netbrick/nette-errbit)
[![License](https://poser.pugx.org/netbrick/nette-errbit/license.svg)](https://packagist.org/packages/netbrick/nette-errbit)


**Warning:** This logger isn't working well od developemnt mode in nette. Handling errors in production is fine. In development you have Tracy with all stack trace and you don't need to log this errros on errbit.

Instalation
-----------

Install package via composer:

``` bash
composer require netbrick/nette-errbit
```

Usage
-----

In Nette application add config file:


``` yml
parameters:
	errbit:
		send_errors: true
		api_key: your-api-key
		host: errbit-host.com
		port: 80                                        # optional
		secure: false                                   # optional
		project_root: /your/project/root                # optional
		environment_name: production                    # optional
		params_filters: ['/password/', '/card_number/'] # optional
		backtrace_filters: ['#/some/long/path#']        # optional
```

All configurations are based on package [flippa/errbit-php](https://github.com/flippa/errbit-php)

In nette application you add this line to *bootstrap.php* after you create *$container*:

``` php
Netbrick\Errbit\ErrbitLogger::register($container->parameters['errbit']);
Netbrick\Errbit\ErrbitLogger::ignoreNotices();
Netbrick\Errbit\ErrbitLogger::addIgnoreMessage('Some exception message text');

// Default log priorities: error, exception. To rewrite call:
Netbrick\Errbit\ErrbitLogger::setLogPriorities(array('error', 'exception', 'access'));
```

**Thats it!** You should see your logs in your errbit



