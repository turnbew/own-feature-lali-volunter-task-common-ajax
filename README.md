TASK DATE: 10.11.2017 - FINISHED: 10.11.2017

TASK SHORT DESCRIPTION: - (NEW AJAX object created by Lajos Deli)

GITHUB REPOSITORY CODE: feature/lali-volunter-task-common-ajax

ORIGINAL WORK: https://github.com/BusinessBecause/network-site/tree/feature/lali-volunter-task-common-ajax

CHANGES

	IN FILES: 
	
		IN USAGE
		
			\network-site\addons\default\modules\fundraising\js\fundraising.js
	
				CHANGED CODE: 
				
					FROM: 
					
					
					TO: 
					
						
	
		\network-site\system\cms\config\asset.php
		
			ADDED CODE: 
			
				$add_library(array(
					'js' => array('_commons/common_ajax.js')
				));
		
	
		ADDED NEW FILE: \network-site\assets\_commons\common_ajax.js
		
			CODE IN IT: 
		
				/*
				 *	GLOBAL variables
				 *
				 *	AJAX.asynch		- boolean, default value true - can be true or false 		 
				 *	AJAX.method 	- string, default value POST - can be GET, POST, PUT
				 *	AJAX.base_url	- string, default value = BASE_URI
				 *	AJAX.data		- string or object, default value empty object {} 	
				 *	AJAX.data_type	- string, default value text, can be text, xml, json, script or html
				 *	AJAX.success	- function, default: empty function
				 *	AJAX.error		- function, default: function(response) {console.log(response);alert('Something went wrong. Please, try again!');};
				 *	AJAX.complete	- function, default: empty function
				 *	AJAX.cache		- boolean, default: false - can be true or false
				 *	
				 *	
				 *	GLOBAL functions
				 *	
				 * 	AJAX.construct(VOID) : VOID
				 *	AJAX.call(request_url, sent_params, callback_success_fn, callback_error_fn, callback_complete_fn)
				 *	
				*/

				
				(function($) {
						
					$.object_ajax = {
						
						//variables
						default_async				:	true,				//true or false - false is depricated, recommended true
						default_mehtod 				:	"",					//POST or GET
						default_base_url			:	"",		
						default_data				:	{},					//Can be anything, default is an empty object
						default_data_type			:	"",					//text, xml, json, script or html
						default_success_function	:	function(){},		//function will be evaulated if call was succes
						default_error_function		:	function(){},		//function will be evaulated if call caused error
						default_complete_function	:	function(){},		//function will be evaulated if call was completed
						default_cache				:	false,
						
						

						
						//functions
						/*
						 * @input: VOID
						 *
						 * @output: VOID
						*/
						ajaxInitialization : function () 
						{
							$.object_ajax.default_base_url = BASE_URI;			
							$.default_error_function = function(response) { 
															console.log(response);
															alert('Something went wrong. Please, try again!');
														};
							$.object_ajax.default_mehtod = "POST";
							$.object_ajax.default_data_type = "text";			
						},	
						
						
						
						
						/*
						 * Makes a beautiful AJAX call using jQuery
						 *
						 * @input: (there's no Dependency Injection - params order important) 
						 *	- request_url: STRING, required : url to the server side script
						 *	- sent_params: ANY, non required, default value is {} : passed data to server side script
						 * 	- callback_success: FUNCTION non required, default is empty function : callback function which will be evaulated when ajax call was success
						 * 	- callback_error: FUNCTION non required, default is empty function : callback function which will be evaulated when ajax call produced error
						 * 	- callback_complete: FUNCTION non required, default is empty function : callback function which will be evaulated when ajax call was completed
						 *
						 * @output: VOID or returns response (if call is synchronous - not recommended)
						*/
						ajaxCall : function(request_url, sent_params, callback_success, callback_error, callback_complete)
						{
							var data 		= (sent_params != undefined) 		? sent_params 		: $.object_ajax.default_data;
							var succes 		= (callback_succes != undefined) 	? callback_success 	: $.object_ajax.default_success_function;
							var error 		= (callback_error != undefined) 	? callback_error 	: $.object_ajax.default_error_function;
							var complete 	= (callback_complete != undefined)	? callback_complete	: $.object_ajax.default_complete_function;
							var response 	= $.ajax({
												url 	: BASE_URI + request_url, 
												type 	: default_mehtod,
												data 	: data,			
												dataType: dt,
												async	: true,
												success	: succes(), 
												error	: error(),
												complete: complete()
											});		
							if (!default_async) return $.trim(response);
						},
						
						
						
					}; //END $.object_ajax object

					
					//GLOBAL variables of $.object_ajax object
					AJAX			= 	$.object_ajax;
					AJAX.asynch 	=	$.object_ajax.default_async;
					AJAX.method 	=	$.object_ajax.default_mehtod;
					AJAX.base_url 	=	$.object_ajax.default_base_url;
					AJAX.data	 	=	$.object_ajax.default_base_url;
					AJAX.data_type 	=	$.object_ajax.default_data_type;
					AJAX.success 	=	$.object_ajax.default_success_function;
					AJAX.error	 	=	$.object_ajax.default_error_function;
					AJAX.complete 	=	$.object_ajax.default_complete_function;
					AJAX.cache	 	=	$.object_ajax.default_cache;
					
					
					//GLOBAL functions of $.object_ajax object
					AJAX.construct = function () {$.object_ajax.ajaxInitialization();}
					AJAX.call = function(u, d, cs, ce, cc) {return $.object_ajax.ajaxCall(u, d, cs, ce, cc);}
					
				})(jQuery);


				//when DOM is loaded
				$(function() {
					
					//Initialization
					AJAX.construct();
				})							
