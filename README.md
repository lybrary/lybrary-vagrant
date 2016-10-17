# Lybrary-Vagrant

A development environment for [Lybrary](https://www.github.com/Lybrary/lybrary/) using [Vagrant](https://www.vagrantup.com/).

## Prerequisites

You will need the following applications to setup the Lybrary development environment:

* [Vagrant](https://www.vagrantup.com/)
* [VirtualBox]()
* [Git]()

## Setup

First, clone this repo:

`git clone git://github.com/Lybrary/Lybrary-Vagrant.git`

Clone the Lybrary repo into your new Lybrary-Vagrant repo:

```bash
cd Lybrary-Vagrant
git clone git://github.com/Lybrary/Lybrary.git
```

Now that both repositories are cloned we can setup the VM:

`vagrant up`

Once the VM setup process is complete you'll need to log into the VM and setup Lybrary.

```bash
vagrant ssh # Log into the VM

cd /code/Lybrary
bundle install
```

## Running Lybrary

To run Lybrary you need to use:

`rails server -b 0.0.0.0`

You should now be able to see Lybrary at: `http://192.168.33.8:3000/`!
