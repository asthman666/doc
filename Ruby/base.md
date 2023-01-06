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
	
The splat operator unpacks an array passed to a function so that each element is sent to the function as an individual parameter.	
	
	>> def func(a, b, c)
	>>   puts a, b, c
	>> end
	=> nil

	>> func(1, 2, 3)  #we can call func with three parameters
	1
	2
	3
	=> nil

	>> list = [1, 2, 3]
	=> [1, 2, 3]

	>> func(list) #We CAN'T call func with an array, even though it has three objects
	ArgumentError: wrong number of arguments (1 for 3)
	    from (irb):12:in 'func'
	    from (irb):12

	>> func(*list) #But we CAN call func with an unpacked array.
	1
	2
	3
	=> nil	
