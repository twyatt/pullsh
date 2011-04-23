Features
--------
* Includes simple configuration app.
* Pulls and executes remote shell script.
* (Optional) Includes launch agent to execute on start up and every hour.

Installation
------------
1. Download the [pullsh.dmg] and run the included installer.
2. Run the *Configure pullsh* application included with the [pullsh.dmg] file.

Configuration
-------------
pullsh expects that a host be configured to provide a shell script to pull and execute; the following is an example setup in Rails:

app/controllers/pullsh_controller.rb
	class PullshController < ApplicationController
	  def script
	    response.headers['X-Execute'] = 'yes'
	    render :layout => false
	  end
	end

app/views/pullsh/script.erb
	#!/bin/bash
	
	OUTPUT="/tmp/pullsh.test"
	echo `date` >> ${OUTPUT}
	echo "Hello world from `whoami`." >> ${OUTPUT}
	echo >> ${OUTPUT}