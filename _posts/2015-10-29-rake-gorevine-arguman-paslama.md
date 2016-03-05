---
layout: post
title: "Rake Görevine Arguman Paslama"
date: 2015-10-29 22:42
comments: true
---

#### Yöntem 1

{% highlight ruby %}
task :print do
  name = ENV['name']
  p name
end
{% endhighlight %}

{% highlight sh %}
$ rake print
nil

$ rake print name="askin"
"askin"
{% endhighlight %}


#### Yöntem 2

{% highlight ruby %}
task :print, [:name, :age] do |task, args|
  puts task
  puts "name is: #{args.name}"
  puts "age is: #{args.age}"
end
{% endhighlight %}

{% highlight sh %}
$ rake print["osman",8]
print
name is: osman
age is: 8
{% endhighlight %}
