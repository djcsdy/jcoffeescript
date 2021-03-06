# JCoffeeScript

JCoffeeScript is a java library that compiles CoffeeScript 0.9.2.  JCoffeeScript is licensed under the Apache license 2.0.  Please see LICENSE for more detail.

## Usage
from the command prompt:
    prompt> echo "a = 1" | java -jar jcoffeescript.jar
    (function(){
      var a;
      a = 1;
    })();

command prompt options:
    --no-wrap   Compile the JavaScript without the top-level function safety wrapper.

from java:
    String javascript = new org.jcoffeescript.JCoffeeScriptCompiler().compile("a = 1");

from jruby:
    if "java" == RUBY_PLATFORM then
        # use jcoffeescript implementation
        require 'java'
        class CoffeeScriptCompiler

            def initialize
                @compiler = org.jcoffeescript.JCoffeeScriptCompiler.new
            end

            def compile(source)
                @compiler.compile(source)
            end
        end
    else
        # use shell out to coffee implementation
        require 'open3'
        class CoffeeScriptCompiler
            def compile(source)
                return Open3.popen3('coffee --eval --print') do |stdin, stdout, stderr|
                  stdin.puts source
                  stdin.close
                  stdout.read
                end
            end
        end
    end
    compiler = CoffeeScriptCompiler.new
    compiler.compile('a = 1')

## Finally
Thanks to Jeremy Ashkenas and all contributors to the coffeescript project.

Thanks to Raphael Speyer for helping with the design.

Thanks to Daniel Cassidy for putting a lot of work into the code.

Thanks to PandaWood for helping with the code.

Home Page: http://yeungda.github.com/jcoffeescript
