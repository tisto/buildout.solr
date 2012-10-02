==============================
collective.recipe.solrinstance
==============================

Prerequisits
------------

Install Java runtime environment (Ubuntu 12.04 LTS)::

    $ sudo apt-get install openjdk-7-jre


https://code.gocept.com/svn/osha/osha.extranet/trunk/development.cfg
https://code.gocept.com/svn/osha/osha.extranet/trunk/base.cfg
https://dev.inigo-tech.com/svn/ilo/buildout/branch/xmpp/solr.cfg
http://code.google.com/p/contentmirror/issues/attachmentText?id=76&aid=-4316447007337831768&name=test-buildout.cfg&token=sPQVUF7_sLAXgCtb3kq-4g2hBew%3A1346368603220


===============
collective.solr
===============

Installation
------------

- add to eggs section in buildout
- activate in add-on controlpanel
- activate in solf controlpanel: http://localhost:8080/Plone/@@solr-controlpanel

- reindex content: http://localhost:8080/Plone/@@solr-maintenance/reindex


=============
alm.solrindex
=============

http://blogs.sourceallies.com/2009/10/solr-%E2%80%93-features-and-configuration-details/
http://plonexp.leocorn.com/leocornus/leocornus.buildout.cfgrepo/xps13
http://plonexp.leocorn.com/leocornus/leocornus.buildout.cfgrepo/xps15

buildout.cfg::

    [instance]
    ...
    environment-vars =
          SOLR_URI http://127.0.0.1:8983/solr

    [solr]
    ...
    additional-solrconfig =
        <requestHandler name="/dataimport" class="org.apache.solr.handler.dataimport.DataImportHandler">
            <lst name="defaults">
                <str name="config">data-config.xml</str>
            </lst>
        </requestHandler>


data-config.xml::

    <dataConfig>
      <dataSource type="JdbcDataSource"
                  driver="com.mysql.jdbc.Driver"
                  url="jdbc:mysql://localhost/jungzeelandia"
                  user="jungzeelandia"
                  password=""/>
      <document>
        <entity name="id"
                query="select id,name,rezeptcode from rezepte">
        </entity>
      </document>
    </dataConfig>