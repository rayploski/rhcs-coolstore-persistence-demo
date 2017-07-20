App Dev Cloud with JBoss Cool Store Persistence Demo 
==========================================
This demo is to install JBoss Cool Store in the Cloud with PostgreSQL data persistence on any OpenShift Container Platform. It delivers a fully functioning JBoss Cool Store containerized on OSE and backed by a persistent data store.

The Cool Store is a retail web store demo where you will find rules, decision tables, events, and a ruleflow 
that is leveraged by a web application. The web application is a WAR built using the JBoss BRMS
generated project as a dependency, providing an example project showing how developers can focus on the 
application code while the business analysts can focus on rules, events, and ruleflows in the 
JBoss BRMS product web based dashboard.

Alongside the Cool Store is a PostgreSQL database container that provides persistent storage for the JBoss BRMS platform and connected via Kubernetes services.

This demo environment is fully containerized, it uses a custom maven settings to deploy all built JBoss BRMS knowledge artifacts
into an external maven repository (not your local repository), in /tmp/maven-repo.


Install on OpenShift
--------------------
1. First ensure you have an OpenShift container based installation, such as one of the followling installed first:

  - [OCP Install Demo](https://github.com/redhatdemocentral/ocp-install-demo)

  - or your own OpenShift installation.

2. [Download and unzip this demo.](https://github.com/redhatdemocentral/rhcs-coolstore-persistence-demo/archive/master.zip)

3. Download JBoss EAP & JBoss BRMS, add to installs directory (see installs/README). 

4. Run 'init.sh' or 'init.bat' file. 'init.bat' must be run with Administrative privileges:

```
   # The installation needs to be pointed to a running version
   # of OpenShift, so pass an IP address such as:
   #
   $ ./init.sh 192.168.99.100  # example for OCP.
```

Login to Cool Store to start exploring a retail web shopping project (the address will be generated by the init script):

  - OCP example:
    [http://rhcs-coolstore-p-demo.192.168.99.100.xip.io/business-central](http://rhcs-coolstore-p-demo.192.168.99.100.xip.io/business-central) ( u:erics / p:jbossbrms1! )

  - OCP example web app:
    [http://rhcs-coolstore-p-demo.192.168.99.100.xip.io/brms-coolstore-demo](http://rhcs-coolstore-p-demo.192.168.99.100.xip.io/brms-coolstore-demo)

5. Want to build the Cool Store demo from scratch? Try these hands-on <a href="https://bpmworkshop.github.io/#/4" target="_blank">online workshops</a>.


Note before running demo:
-------------------------
This project can be installed on any OpenShift platform, such as OpenShift Container Platform.
It's possible to install it on any available installation by pointing this installer to an OpenShift IP address:
```
  $ ./init.sh IP
```

If for any reason the installation breaks or you want a new JBoss BRMS installation, just remove the project rhcs-brms-install-demo
entry in the OpenShift console and re-run the installation.

Should your local network DNS not handle the resolution of the above address, giving you page not found errors, you can apply the
following to your local hosts file:

```
$ sudo vi /etc/hosts

# add host for OCP demo resulution
192.168.99.100   rhcs-coolstore-p-demo.192.168.99.100.xip.io 
```

To clone a repository in the running container, the following actions would need to occur from a developer's machine.

1. Execute port forwarding through the OpenShift CLI. This will open a tunnel between the developer's machine and the pod through
	 the OpenShift API pod proxy. The command window will block while the session is open:

   ```
   # Read-only access to repo on port 9418.
   #
   $ oc port-forward $(oc get pod -l=deploymentconfig=rhcs-coolstore-p-demo --template='{{ range .items }} {{ .metadata.name }} {{ end }}') 9418:9418

   # Read-write access to repo on port 8001.
   #
   $ oc port-forward $(oc get pod -l=deploymentconfig=rhcs-coolstore-p-demo --template='{{ range .items }} {{ .metadata.name }} {{ end }}') 8001:8001
   ```

2. Clone the repository. In another window, clone the remote repository:

   ```
   # Read-only access to repo on port 9418.
   #
   $ git clone git://localhost:9418/coolstore-demo

   # Read-write access to repo on port 8001.
   #
   $ git clone git://localhost:8001/coolstore-demo
   ```


Supporting Articles
-------------------
- [How to add Cloud persistent storage to JBoss Cool Store](http://www.schabell.org/2016/04/howto-add-cloud-persistent-storage-to-jboss-coolstore.html)

- [Ultimate Cloud Guide to Retail in the Cloud with JBoss Cool Store](http://www.schabell.org/2016/03/ultimate-cloud-guide-retail-cloud-jboss-coolstore.html)


Released versions
-----------------
- v1.5 - JBoss BRMS 6.4.0 and JBoss EAP 7.0.0 with Cool Store leveraging postgresql persistence installed on any given OpenShift installation and loading mulitple projects.

- v1.4 - JBoss BRMS 6.4.0 and JBoss EAP 7.0.0 with Cool Store leveraging postgresql persistence installed on any given OpenShift installation and port forwarding for git repo access configured.

- v1.3 - JBoss BRMS 6.4.0 and JBoss EAP 7.0.0 with Cool Store leveraging postgresql persistence installed on any given OpenShift installation.

- v1.2 - JBoss BRMS 6.3.0 and JBoss EAP 6.4.7 with Cool Store leveraging postgresql persistence installed on Red Hat CDK.

- v1.1 - JBoss BRMS 6.2.0.GA-redhat-1-bz-1334704 and JBoss EAP 6.4.4 with Cool Store leveraging postgresql persistence installed on Red Hat CDK.

- v1.0 - JBoss BRMS 6.2.0-BZ-1299002, JBoss EAP 6.4.4 with Cool Store leveraging postgresql persistence installed on Red Hat CDK using OpenShift Enterprise image.


![OSE pods](https://github.com/redhatdemocentral/rhcs-coolstore-persistence-demo/blob/master/docs/demo-images/rhcs-coolstore-p-pods.png?raw=true)

![JBoss BRMS](https://github.com/redhatdemocentral/rhcs-coolstore-persistence-demo/blob/master/docs/demo-images/coolstore-shoppingcart-2.png?raw=true)

![Decision Table](https://github.com/redhatdemocentral/rhcs-coolstore-persistence-demo/blob/master/docs/demo-images/coolstore-decision-table.png?raw=true)

![Cloud Suite](https://github.com/redhatdemocentral/rhcs-coolstore-persistence-demo/blob/master/docs/demo-images/rhcs-arch.png?raw=true)

