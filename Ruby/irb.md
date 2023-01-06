  irb(main):000:0> DateTime.class
  NameError: uninitialized constant DateTime
          from (irb):0
          from /path/to/ruby/irb:12:in '(main)'
  irb(main):001:0> require 'date'
  => true
  irb(main):002:0> DateTime.class
  => Class
