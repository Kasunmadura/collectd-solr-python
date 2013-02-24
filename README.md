collectd-solr-python
====================

Python-based plugin to put various [Solr 4.X] (http://lucene.apache.org/solr/) stats to [collectd](http://collectd.org)

Data captured includes:

 * TODO

Cores are detecting automatically. XML structure
Munin plugins from [Distilled Media Ltd.] (https://github.com/distilledmedia/munin-plugins/) and [Gasol Wu] (https://github.com/Gasol/munin-solr-plugins/)
were used as donors.
[powdahoud's redis-collectd-plugin] (https://github.com/powdahound/redis-collectd-plugin/) was used as template also.

Install
-------
 0. Place stats requestHandler in solrconfig.xml for all cores, since stats.jsp is not working since 4.x
   <requestHandler
     name="/admin/stats"
     class="org.apache.solr.handler.admin.SolrInfoMBeanHandler" />

 1. Place collectd-solr.py in /usr/lib/collectd/plugins/python
 2. Configure the plugin (see below).
 3. Restart collectd.

Configuration
-------------
Add the following to your collectd config

    <LoadPlugin python>
      Globals true
    </LoadPlugin>

    <Plugin python>
      ModulePath "/usr/lib/collectd/plugins/python"
      Import "collectd-solr"

      <Module collectd-solr>
        Host "localhost"
        Port 8080
        URL "/solr"
        AdminURL "admin/stats?stats=true"
      </Module>
    </Plugin>
