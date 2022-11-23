	require 'pp'
	
	def headers()
		headers = {"one" => "eins", "two" => "knee"}
	end
	
	headers = headers()
	puts "headers variable #{headers.class == Hash ? 'is' : 'is not'} hash"
	pp headers

	# output:
	# headers variable is hash
	# {"one"=>"eins", "two"=>"knee"}


	def met(&block)
		puts "This is met method"
		block.call
		met2(block)
	end
	
	def met2(block)
		puts "This is met2 method"
		block.call
	end
	
	met {puts "This is &block example"}
	
	# output:
	# This is met method
	# This is &block example
	# This is met2 method
	# This is &block example