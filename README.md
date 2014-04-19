Laravel-Country-Validator
=========================

A simple country validation rule for Laravel

##How to install
1. Clone or download this repo.
2. Copy the ``custom`` folder into your Laravel project's ``app/`` directory.
3. Make sure the validator is included
	- In your Laravel project's ``app/start/global.php`` file at the top you'll see something like this.
	
				ClassLoader::addDirectories(array(
			    app_path() . '/commands',
			    app_path() . '/controllers',
			    app_path() . '/models',
			    app_path() . '/database/seeds',	
			));
	- You'll want to add ``app_path() . '/custom',`` into it so it becomes
	
			ClassLoader::addDirectories(array(
						    app_path() . '/commands',
						    app_path() . '/controllers',
						    app_path() . '/models',
						    app_path() . '/database/seeds',
							app_path() . '/custom',	
						));
4. Excellent! You're doing well. Now, you need to register the validation resolver:

		Validator::resolver(function($translator, $data, $rules, $messages)
		{
		    return new CountryValidator($translator, $data, $rules, $messages);
		});
		

Copy and paste that into your ``routes.php`` or ``global.php`` file.

5. Add a validation error message in ``app/lang/en/validation.php`` in the validation language lines array

####For example
    "country" => "The :attribute must be a country",
	"accepted" => "The :attribute must be accepted.",
    "active_url" => "The :attribute is not a valid URL.",
    "after" => "The :attribute must be a date after :date.",


##How to use
Simply the ``country`` rule like any other validation rule. 

####For example

		$rules = [
			'country' => 'required|country'
		];
		$validator = Validator::make($data, $rules);
		///