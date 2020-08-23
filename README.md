# Install Hive

Open Terminal

Download Hive
```wget https://downloads.apache.org/hive/hive-2.3.7/apache-hive-2.3.7-bin.tar.gz```

extract Hive
```tar -xvf apache-hive-2.3.7-bin.tar.gz```

Become admin
```sudo su```

Move the file from the current location to /usr/local/
```sudo mv apache-hive-2.3.7-bin /usr/local/```

go to new file location /usr/local/apache-hive-2.3.7-bin
```cd apache-hive-2.3.7-bin/conf```

copy hive-default template to be in hive-default
```cp hive-default.xml.template hive-default.xml```

Open hive-default.xml
```gedit hive-default.xml```

Add the location of your parent file in the database default configurations
```
<property>
    <name>javax.jdo.option.ConnectionURL</name>
    <value>jdbc:derby:;databaseName=/usr/local/apache-hive-2.3.7-bin/metastore_db;create=true</value>
    <description>
      JDBC connect string for a JDBC metastore.
      To use SSL to encrypt/authenticate the connection, provide database-specific SSL flag in the connection URL.
      For example, jdbc:postgresql://myhost/db?ssl=true for postgres database.
    </description>
  </property>
```
save and close the file

Test Hive
```sudo hive```



