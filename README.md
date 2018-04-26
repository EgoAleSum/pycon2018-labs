# Hands-on labs for PyCon 2018

This repository contains the hands-on labs for the Microsoft booth at PyCon 2018.

## Create a lab

Please create a **subfolder for each lab**. Each folder needs to contain:

1. A `README.md` file describing the lab
1. A `hol.md` file with the lab's content (if you need to add images inline, place them in a folder called `images`)

In addition to the two files above, you can **optionally** add:

1. A `requirements.md` file containing a description of the software that needs to be pre-installed on the demo VM
1. An `azuredeploy.json` file containing, which is an ARM template describing the resources that needs to be pre-provisioned before the lab starts.
1. An `assets` folder containing documents that need to be copied inside the VM (in a subfolder on the Desktop named after the lab)

The instructions to create a lab are present here: https://github.com/LearnOnDemandSystems/guides/tree/b00c85c0b42f656ee7d60fd7907625e4a5973de2/idl2 This document also describes the custom additions to the Markdown format for the lab.

## Info

1. Each lab offers a VM connected via RDP, that runs Windows 10 and has 4 GB of RAM. VMs are running on Hyper-V and they *might* have support for nested virtualization (to be confirmed).
1. In addition to the software that you require, each VM will have pre-installed a web browser (Edge), Visual Studio Code and [Anaconda](https://www.anaconda.com/download/).
1. Each lab user will have access to an Azure subscription (an empty Resource Group specifically created). All resources provisioned during the lab are automatically destroyed at the end.
1. Please avoid adding links in the `hol.md` file, as those would open on the client machine rather than in the VM.

## Sample

Sample lab Markdown file is here: https://github.com/sriramdasbalaji/AzurefunctionsBuildHOL/tree/master/HOL
