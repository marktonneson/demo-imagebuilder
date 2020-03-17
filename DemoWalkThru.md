## ImageBuilder Demo WalkThru

### Requirements
* Minimum VM: 2vCPU x 2G mem, running RHEL 7.latest or RHEL 8.latest
* Will need root or sudo to install packages
* Enough free disk space in root (/) for a complete image (~ 5GB)

### WalkThru
* Install & Config

Prior to getting started with image builder, the software must first be installed.
For RHEL 7:
```
[root@workstation] # yum install --enablerepo=rhel-7-server-extras-rpms -y cockpit cockpit-composer lorax-composer composer-cli
[root@workstation] # firewall-cmd --permanent --add-service=cockpit && firewall-cmd --reload
[root@workstation] # systemctl enable --now cockpit.socket
```
For RHEL 8:
```
[root@workstation] # yum install -y cockpit-composer lorax-composer composer-cli
[root@workstation] # systemctl enable --now cockpit.socket
```
Now that the software is installed, restart the web console so that it picks up the newly installed plugin for image builder. Also, you will enable the service that manages the build queue and other aspects of image builder.
```
[root@workstation] # systemctl restart cockpit; systemctl enable --now lorax-composer.service
```

Lastly, in the next steps, you will use a non-administrative user, **student**, to manage the image blueprints and build machine images. This user must belong to the **weldr** group.
```
[root@workstation] # useradd -G weldr student
[root@workstation] # echo 'redhat' | passwd --stdin student
```
* Log back into the Web Console
Login using the student user, with password = redhat.  Now that you are logged into the Web Console, navigate to the **Image Builder** application.
![Image 1](https://github.com/marktonneson/demo-imagebuilder/blob/master/images/image1.png)

* Navigate to the Edit Blueprint page
You can see in the **Image Builder** application that there are several blueprints available. When you are ready, go to the edit page for the **example-http-server** blueprint by clicking the **Edit Blueprint** button.
![Image 2](https://github.com/marktonneson/demo-imagebuilder/blob/master/images/image2.png)

* Filter the list of available components
On the **Edit Blueprint** page, you can see contents that are already included in the blueprint in the panel labeled **Blueprint Components**. The panel labeled **Available Components** includes contents that can be added to the blueprint.
Filter the list of **Available Components** by **mod_** to find the mod_wsgi package.
![Image 3](https://github.com/marktonneson/demo-imagebuilder/blob/master/images/image3.png)

* Add a package
Find the **mod_wsgi** package in the filtered list of **Available Components**. You can either click the package list item to view more details and options available for the package, or you can click the Add icon button for the list item to add the latest version.
Add the package **mod_wsgi** to the blueprint.
![Image 4](https://github.com/marktonneson/demo-imagebuilder/blob/master/images/image4.png)

* Commit changes
Now that you have updated the contents of the blueprint, spend some time exploring the organization of the blueprint contents. Note that blueprint contents can also be filtered, and when contents are added, their dependencies are automatically pulled in. Try filtering the blueprint contents by "python" to see if python-libs was automatically included in the blueprint as a dependency. Or click the Undo button to see how the number of dependencies changed when you added mod_wsgi.
When you are ready, click the **Commit** button to commit your changes.
![Image 5](https://github.com/marktonneson/demo-imagebuilder/blob/master/images/image5.png)

* Verify pending changes
The **Changes Pending Commit** dialog will list all changes you have made since you last committed your changes.
When you are ready, click the **Commit** button in the dialog to commit your changes.
![Image 6](https://github.com/marktonneson/demo-imagebuilder/blob/master/images/image6.png)

* You will see a confirmation message appear in the top, right side of the web console window.
![Image 7](https://github.com/marktonneson/demo-imagebuilder/blob/master/images/image7.png)

* Create image
Click the **Create Image** button to open the dialog. Select which type to create then click the **Create** button.
Images that are created for a blueprint can be found under the **Images** tab on the blueprint page. You can navigate to this page by clicking the blueprint name in the breadcrumb.
![Image 8](https://github.com/marktonneson/demo-imagebuilder/blob/master/images/image8.png)

* Optional: Cleanup environment
If you are using a non-disposable system, cleanup the environment with the following commands:
```
[root@workstation] # yum remove -y cockpit cockpit-composer lorax-composer composer-cli
[root@workstation] # userdel student && rm -rf /home/student
[root@workstation] # rm -rf /var/lib/lorax/composer/
```
