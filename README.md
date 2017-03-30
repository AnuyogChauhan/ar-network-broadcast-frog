
ar-network
===============


###Instructions###

preface: the Makefile has most of the repeatable functions within the repository.  Most of the instructions are calls to the makefile, but you can always inspect the Makefile for sequential shell commands.  Also - as of this writing, the ENS client is not complete - there are stubs in the unit tests.

The unit tests assume a recently built, running docker image as generated by the instructions below.

There aren't any special python libraries used, so stock python 2.7 should work.

---

How to build the docker image:

prerequisites:

* make sure the submodule has been downloaded and initialized by either typing _make init_ or typing _git submodule update --init_ within the repository.


How to build the docker image:

    make build

How to run the docker image with the flags that expose the port the unittests are looking for:

    make run

How to run the unit tests:

    make test
 
 ----

### Notes for ENS Implementation ###


The base assumption here, is that <text>ar_client_base.py</text>, <text>ar_server.py</text>, and <text>ar_client_control.py</text> will run the traditional network architecture version of the app.
And <text>ar_client_base_ens.py</text>, <text>ar_server_ens.py</text>, and <text>ar_client_control_ens.py</text> will run the EDGE version of the app.

The <text>&#42;&#x5f;ens.py</text> files each has code comments and pseudocode according to my current understanding of the EDGE application.  Anything that needs to be changed can absolutely be changed within the <text>	&#42;&#x5f;ens.py</text> files


I've written out the directory structure, and notes on each file.

		./
		├── Dockerfile.traditional 			# initial 'traditional network architecture' Dockerfile  -- Anderson's TODO: redis in this container for tests
		├── Dockerfile.ens 							# ENS dockerfile - modify away!
		├── Makefile 										# parallel build/buildens, run/runens 
		├── README.md 									# this file
		├── ar_client_base.py      # client class (will be used by base NUC app)
		├── ar_client_base_ens.py  # client class (will be used by base NUC app) - instructions have been written in pseudocode! - feel free to modify!
		├── ar_client_control.py	 # client broadcast class (will be used by base NUC app)
		├── ar_client_control_ens.py	# client broadcast class (will be used by base NUC app) - instructions have been written in pseudocode! - feel free to modify!
		├── ar_server.py					 # traditional server arch server class
		├── ar_server_ens.py			 # ENS architecture server class (modify away if necessary)
		├── ens										 # folder of useful ens classes - add any if necessary!
		│   ├── DockerfilePy
		│   ├── __init__.py
		│   ├── ensclient.py
		│   ├── ensiwc.so
		│   ├── enswmain.py
		│   ├── enswr.py
		│   ├── libensiwc.so
		│   └── workloadPy.sh
		├── lib										# networking-common submodule
		│   ├── README.md
		│   ├── SimpleBroadcast.py
		│   ├── SimpleClient.py
		│   ├── SimpleServer.py
		│   ├── __init__.py
		│   └── boomerang
		│       ├── Makefile
		│       ├── boomerang_client.py
		│       ├── boomerang_server.py
		│       └── deployment.py
		└── tests.py							# networking tests
