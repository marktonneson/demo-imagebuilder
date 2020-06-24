# demo-imagebuilder

Image Builder is a tool for creating custom system images. To control Image Builder and create your custom system images, you can use the web console interface. Note that the command line interface is the currently preferred alternative, because it offers more features.

### Image Builder Terminology
#### Blueprint
* Blueprints define customized system images by listing packages and customizations that will be part of the system
* Blueprints can be edited and they are versioned
* When a system image is created from a blueprint, the image is associated with the blueprint in the Image Builder interface of the RHEL 8 web console
* Blueprints are presented to the user as plain text in the Tom’s Obvious, Minimal Language (TOML) format

#### Compose
* Composes are individual builds of a system image, based on a particular version of a particular blueprint
* Compose as a term refers to the system image, the logs from its creation, inputs, metadata, and the process itself

#### Customization
* Customizations are specifications for the system, which includes users, groups, and SSH keys

### Notes
* RHEL 7 or 8


### References and Resources
* [RHEL 8 Documentation](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/system_design_guide/creating-system-images-with-composer-web-console-interface_system-design-guide)
* [RHEL 7 Documentation](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/image_builder_guide/index)
* [Lee Whitty's Image Builder Lab](https://github.com/lwhitty/image-builder-lab)
