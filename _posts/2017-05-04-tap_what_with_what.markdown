---
layout: post
title:  "Tap What With What?"
date:   2017-05-04 23:57:14 +0000
---


I have seen #tap being used by Avi during videos and in the solution to some of the labs and I only somewhat understood what it is really doing. Sometimes I feel that I need more explanation than the Ruby docs can give and I feel like some of the answers on Stack Overflow are over my head or they just give the answer and really don’t explain what the method is doing. So I did some searching and found a couple of websites that were useful. On the See John Code blog, he shows what the code is behind the #tap method:

```
VALUE rb_obj_tap(VALUE obj)
{
  rb_yield(obj);
  return obj;
}
```

This reveals that #tap is taking in an object as an argument, yielding the object to the block and then returning the object.

In Ruby code, it looks like this:

```
class Object
  def tap
    yield self
    self
  end
end
```

This means that #tap is a way to do something with an object inside a block of code and have it return the object itself. This is useful when you want to avoid what some of the other methods return. For example, #each returns the original array. This is helpful if you are dealing with a hash and need the hash returned. An example from Engine Yard’s blog:

```
def update_params(params) 
	params[:foo] = 'bar' 
	params 
end
```

Instead of needing to put the “params” at the end to ensure we get the hash as the return, we can use #tap:

```
def update_params(params) 
	params.tap {|p| p[:foo] = 'bar' } 
end
```

There are more examples of use, but seeing the code behind it “translated” into Ruby and some ways that it can be used really helped me understand the concept to be able to use it in future coding.


Resources:

http://seejohncode.com/2012/01/02/ruby-tap-that

https://blog.engineyard.com/2015/five-ruby-methods-you-should-be-using

