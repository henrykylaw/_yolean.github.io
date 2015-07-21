---
layout: post
title: Merits of Subversion for configuration storage
author: Staffan
---

I tried to think outside the box (while inside the box is version controlled JSON) on how our servers can store Visual Planning instance configuration. We're looking at [Consul](https://consul.io/) for our [Microservices](http://martinfowler.com/articles/microservices.html) approach so I figured it might be able to manage frontend related config as well. Then I stumbled upon a blog post (by those who produce our business cards) on managing configuration files with [Git and Consul](http://lifeinvistaprint.com/techblog/configuration-management-git-consul/):

> Think about all the reasons why revision control systems are so valuable. They give you an audit trail for all changes. They give you exceptional tools for analyzing what has changed

Our templates for Visual Planning boards have been version controlled on customer servers since day 1. While "audit trail" is appealing to some, the primary value we get is that history - with commit comments - helps communication between maintainers over time because we document our decisions. Anyone in our tech team can do the next revision of any customer's config, and we can share responsibility with their IT.

For configuration we use - an untrendy choice - not Git but Subversion. Why?

 * Easier for non-coders, particularily with [TortoiseSVN](http://tortoisesvn.net/).
 * You actually do get an audit trail, unlike Git where version history can be rewritten.
 * There's a REST interface out of the box, with access to historical revisions, (`GET /svn/config/file.json?p=123`).
 * Supports file locking and role based access control.

Git, or more specifically the branch-rebase-merge model, serves us great for development. But in the Microservices approach each service may, or even should, have its own datastore so let's chose based on merit.
