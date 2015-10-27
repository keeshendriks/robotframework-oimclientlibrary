robotframework-oimclientlibrary
=============

A Java based Robot Framework library for Oracle Identity Manager testing.

Description
-----------

OimClientLibrary is a library for Robot Framework that provides keywords for
interacting with the Oracle Identity Manager product (OIM). The [official OIM 11g
API](http://docs.oracle.com/cd/E40329_01/dev.1112/e27150/apis.htm) is used.

Documentation for currently available keywords is in the doc directory (generated by libdoc).

Dependencies
------------

- Oracle's proprietary OimClient (oimclient.zip), included in the OIM installation (see the [official docs](http://docs.oracle.com/cd/E40329_01/dev.1112/e27150/apis.htm#OMDEV2834))
- WebLogic's wlfucllclient.jar (see the [official docs](http://docs.oracle.com/cd/E40329_01/dev.1112/e27150/apis.htm#OMDEV2834))
- [Javalib Core](https://github.com/robotframework/JavalibCore)

Installation
------------

Either download the latest [release](http://maven-repository-jrkoiter.s3-website-eu-west-1.amazonaws.com/release/nl/fuselogic/robotframework-oimclientlibrary/) or [snapshot](http://maven-repository-jrkoiter.s3-website-eu-west-1.amazonaws.com/snapshot/nl/fuselogic/robotframework-oimclientlibrary/) version, or build the library from source by following the steps below. A working Maven installation is assumed:

1. Obtain and unzip oimclient.zip into a directory
2. Get the source of the robotframework-oimclientlibrary (ie. this library)
3. Import the oimclient.jar file into a new local Maven repository (which is referenced in the pom file):

		mvn org.apache.maven.plugins:maven-install-plugin:2.3.1:install-file -Dfile=/path/to/oimclient/oimclient.jar -DgroupId=oracle.iam.platform -DartifactId=oimclient -Dversion=11.1.2.2.0 -Dpackaging=jar -DlocalRepositoryPath=/path/to/robotframework-oimclientlibrary/my-repo

4. Build the library. It will be generated in the subdirectory "target".

		mvn package

Usage
-----

1. Obtain and unzip oimclient.zip into a directory
2. Obtain and copy wlfullclient.jar into /path/to/oimclient/lib
3. Obtain the [Javalib Core](https://github.com/robotframework/JavalibCore) library
4. Add "OimClientLibrary" to your test suite's Settings table, e.g:
   
        *** Settings ***
        | Library | nl.fuselogic.robotframework.libraries.oim.OimClientLibrary |

5. Run your test suites using Jython/jybot with the following Java system property set

		-Djava.security.auth.login.config=/path/to/oimclient/conf/authwl.conf

	and with all libraries in the classpath

		robotframework-oimclientlibrary-*.jar
		javalib-core-1.1.jar
		wlfullclient.jar
		oimclient.jar
		/path/to/oimclient/lib/*
        iam-platform-utils.jar

6. Alternatively, deploy "OimClientLibrary" to a [jrobotremoteserver](https://github.com/ombre42/jrobotremoteserver), and keep running your tests in pybot. Library definition in your tests will then be something like:
        
        *** Settings ***
        | Library | Remote | http://localhost:8270/ | With Name | OimLibrary |

Issues
------
Only a limited set of OIM features is currently exposed through this library.
If you encounter any problems or have a feature request please open an issue on this project's GitHub issue tracker.

License
-------
Copyright 2013 FuseLogic BV

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.