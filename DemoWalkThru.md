## ImageBuilder Demo WalkThru

### Requirements
* Minimum VM: 1vCPU x 1G mem, running RHEL 7.latest or RHEL 8.latest
* Will need root or sudo to install packages

### WalkThru
* Install & Config
Elevate to root
```
[student@workstation] $ sudo -i
```

Prior to getting started with image builder, the software must first be installed.
```
[root@workstation] # yum install -y cockpit-composer lorax-composer composer-cli
```

Now that the software is installed, restart the web console so that it picks up the newly installed plugin for image builder. Also, you will enable the service that manages the build queue and other aspects of image builder.
```
[root@workstation] # systemctl restart cockpit; systemctl enable --now lorax-composer.service
```

Lastly, in the next steps, you will use a non-administrative user, **student**, to manage the image blueprints and build machine images. This user must belong to the **weldr** group.
```
[root@workstation] # usermod -a -G weldr student
```
* Log back into the Web Console
Now that you are logged into the Web Console, navigate to the **Image Builder** application.
!(/images/image1.png)

* Navigate to the Edit Blueprint page
You can see in the **Image Builder** application that there are several blueprints available. When you are ready, go to the edit page for the **example-http-server** blueprint by clicking the **Edit Blueprint** button.
!(/images/image2.png)

* Filter the list of available components
On the **Edit Blueprint** page, you can see contents that are already included in the blueprint in the panel labeled **Blueprint Components**. The panel labeled **Available Components** includes contents that can be added to the blueprint.
Filter the list of **Available Components** by **nodejs** to find the nodejs package.
!(/images/image3.png)

* Add a package
Find the **nodejs** package in the filtered list of **Available Components**. You can either click the package list item to view more details and options available for the package, or you can click the Add icon button for the list item to add the latest version.
Add the package **nodejs** to the blueprint.
!(/images/image4.png)

* Commit changes
Now that you have updated the contents of the blueprint, spend some time exploring the organization of the blueprint contents. Note that blueprint contents can also be filtered, and when contents are added, their dependencies are automatically pulled in. Try filtering the blueprint contents by "npm" to see if it was automatically included in the blueprint as a dependency. Or click the Undo button to see how the number of dependencies changed when you added nodejs.
When you are ready, click the **Commit** button to commit your changes.
!(/images/image5.png)

* Verify pending changes
The **Changes Pending Commit** dialog will list all changes you have made since you last committed your changes.
When you are ready, click the **Commit** button in the dialog to commit your changes.
!(/images/image6.png)

You will see a confirmation message appear in the top, right side of the web console window.
!(/images/image7.png)

* Create image
Click the **Create Image** button to open the dialog. Select which type to create then click the **Create** button.
Images that are created for a blueprint can be found under the **Images** tab on the blueprint page. You can navigate to this page by clicking the blueprint name in the breadcrumb.
!(/images/image8.png)
