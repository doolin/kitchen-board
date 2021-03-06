# kitchen-board (halo api console)
Author: *Alfonso Adriasola* - *aadriasola@cloudpassage.com*

Ruby console with a CloudPassage api session going

##Requirements and Dependencies
Ruby > 2.0 , most often tested on Ruby 2.1.5

Run bundle install, it should install:
* json
* faraday
* oauth2
* awesome_print

##Installation
Clone, download, or fork the git repo, then configure as below.

###Configuration
You need to provide three ENV variables for your account, with the user specific api credentials
available to you via the  CloudPassage admin view.

These can be set in various ways, via .bashrc , via inline , etc. 
```
HALO_KEY_ID = 'xxxxx'
HALO_SECRET_KEY  = 'xxxxxxxxxxxx'
HALO_HOST = 'api.cloudpassage.com'
```

Launch locally as :

`./halo_console.rb`

If all is set up correctly you will see the following prompt


```
CloudPassage API Ruby Command Line Interface
********************************************
```

##Usage

Running `halo_console.rb` will create a `cp` object with the API session token embedded.
A command prompt appears so you can fire requests.
The responses are shown by default in  json format, it also responds to .to_hash and .json for transport.
Use `to_hash` to get the response into a Ruby hash format.


###*Example Commands*

```ruby
cp.get(:fim_policies)

cp.get(:groups).to_hash

cp.get "fim_policies/{id}"


```

For PUT and POST actions, parameters can be supplied as JSON,
this will be handled by RestClient and submitted the right way


```ruby
cp.put "group/{id}", "{group:{name:"load balancers"}}"
```

Given a correctly formatted json file of a file integrity policy "file.json" you could execute

```ruby
my_json_policy = File.read("file.json")

cp.post "fim_policies", my_json_policy
```

###*Output*
A response object that is by default showing the json version, but can be made into a Ruby Hash by the .to_hash method
