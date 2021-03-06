# Packer-AWS

Website: https://www.packer.io
IRC: #packer-tool on Freenode
Mailing list: Google Groups
Packer is a tool for building identical machine images for multiple platforms from a single source configuration.

Packer is lightweight, runs on every major operating system, and is highly performant, creating machine images for multiple platforms in parallel. Packer comes out of the box with support for many platforms, the full list of which can be found at https://www.packer.io/docs/builders/index.html.

Support for other platforms can be added via plugins.

The images that Packer creates can easily be turned into Vagrant boxes.

Quick Start
Note: There is a great introduction and getting started guide for those with a bit more patience. Otherwise, the quick start below will get you up and running quickly, at the sacrifice of not explaining some key points.

First, download a pre-built Packer binary for your operating system or compile Packer yourself.

After Packer is installed, create your first template, which tells Packer what platforms to build images for and how you want to build them. In our case, we'll create a simple AMI that has Redis pre-installed. Save this file as quick-start.json. Export your AWS credentials as the AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY environment variables.

{
  "variables": {
    "access_key": "{{env `AWS_ACCESS_KEY_ID`}}",
    "secret_key": "{{env `AWS_SECRET_ACCESS_KEY`}}"
  },
  "builders": [{
    "type": "amazon-ebs",
    "access_key": "{{user `access_key`}}",
    "secret_key": "{{user `secret_key`}}",
    "region": "us-east-1",
    "source_ami": "ami-af22d9b9",
    "instance_type": "t2.micro",
    "ssh_username": "ubuntu",
    "ami_name": "packer-example {{timestamp}}"
  }]
}
Next, tell Packer to build the image:

$ packer build quick-start.json
...
Packer will build an AMI according to the "quick-start" template. The AMI will be available in your AWS account. To delete the AMI, you must manually delete it using the AWS console. Packer builds your images, it does not manage their lifecycle. Where they go, how they're run, etc. is up to you.

Documentation
Comprehensive documentation is viewable on the Packer website:

https://www.packer.io/docs
