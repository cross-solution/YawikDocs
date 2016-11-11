==============
FAQ: XML Feeds
==============


Can I export jobs via xml feeds?
--------------------------------

Yes. YAWIK offers since 0.28 a default xml feed for all public job openings via the route ``lang/export/xml``. Means for
our demo https://yawik.org/demo/en/export/xml.

If you want do modify the xml structure to fit you needs, override the view ``jobs/export/feed``. The view script gets
injected a paginator containing jobs as ``jobs``.

If you need different XML formats for different channels (in case you are offering multiposting) you can access feeds
for different channels by extending the route name with the channel name. Example: our demo offers a channel ``yawik``.
The feed for this channel can be accessed via https://yawik.org/demo/en/export/xml . If YAWIK finds a view script named
``feed.yawik.xml.phtml``, it uses it to render the xml. Otherwise it uses the default structure defined by
``feed.xml.phtml``. You can access a channel feed via: https://yawik.org/demo/en/export/xml/yawik

Channel feeds only contain jobs, which are public on a certain feed. The URLs to job openings and application forms are
containing the channel name, which makes counting easy.

If you use the ``YawikSolr`` module, Solr results are injected into the feeds automatically. Data, which are not
available in solr are lazy loaded from mongo.


