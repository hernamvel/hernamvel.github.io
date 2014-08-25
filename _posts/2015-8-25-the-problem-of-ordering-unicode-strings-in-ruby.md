---
layout: post
title: The problem of ordering unicode strings in Ruby
category: ruby
---

As having our [company](http://f2p.co) a substantial presence in Colombia, we usually have to deal with the problem
of handling content that is written in Spanish within our software products.

Here the typical problem is to order a list person names, where some of them are spelled with funny characters 
like: &aacute;, &oacute; or &ntilde;.  For example:

* Hern&aacute;n
* Mar&iacute;a
* &Aacute;lvaro
* Andy

For a spanish speaker, the proper result for ordering something like this:

persons = ['&aacute;lvaro', 'alberto', 'andy']

is:

['alberto', '&aacute;lvaro', 'andy']

But a standard ruby's persons.sort command will return:

['alberto', 'andy', '&aacute;lvaro']

That happens due the &aacute; unicode character. Fortunately, there are several solutions available in 
github for this problem. My solution is to use the 'sort_alphabetical' gem.  It's pretty simple:

In your gemfile include:

    gem 'sort_alphabetical'
    
And insead of calling sort, use sort_alphabetical:

persons.sort_alphabetical

And you will have the correct answer:

['alberto', '&aacute;lvaro', 'andy']

Hope this helps :)


