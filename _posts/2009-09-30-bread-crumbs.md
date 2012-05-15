--- 
layout: post
title: Bread Crumbs
wordpress_id: 378
wordpress_url: http://tmayad.loonyb.in/?p=378
date: 2009-09-30 11:37:43 +05:30
---

I want bread crumbs for my site. I want DRY code. Bread crumbs are
invariably derived from the site navigation tree. So I want one to be
derived from the other or both be derived from the same source. After a
little help from [[mattmatt](http://github.com/mattmatt/crumble)] I came
up with this one:

-   I want to define my site structure some where.

{% highlight python %}
site = {
    home:{name:'Home', controller:'home', action:'index'},
    services:{name:'Services', controller:'home', action:'services',
        pages:{
            oneservice:{name:'Service One', controller:'home', action:'serviceone'},
            anotherservice:{name:'Service Two', controller:'home', action:'anotherservice'},
        },
    products:{name:'Products', restController:products},
    help:{name:'Help', url:'/help.html'},
}
{% endhighlight %}

-   All the nav menus will be generated as unordered lists. I should be
    able to call it as

{% highlight python %}
nav(site)                                         #create top level site nav menu
nav(site['services'])                        # create nav menu for the services section of the site
nav('services')                                #complicated: will have to search for the services in the site tree, at any depth
#nav(url, name, action, controller, etc)    #use named parameters to construct url and look for the page with the url in the site tree
{% endhighlight %}

-   And bread crumbs will be generated again as unordered lists, using

{% highlight python %}
crumbs()                                         #generate bread crumbs trail using current target url
#all other calls of nav except for crumbs(site) which would be dumb anyway.
{% endhighlight %}
