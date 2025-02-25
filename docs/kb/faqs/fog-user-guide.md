---
title: Fog User Guide
description: An overview of what fog is and how to use it 
---

# Fog User Guide

## Introduction

### Preface

This document is intended to be modified by FOG users, in fact it is
based on a document created by a FOG user. If you feel something could
be said better or put more clearly, it is encouraged that you make
changes to this document. We just ask that you keep it constructive and
in good taste. In order to edit the wiki you are now required to create
an account, as spamming of the forum has gotten pretty bad recently.

-   **What is FOG?** FOG is a Linux-based, free and open source computer
    imaging solution for Windows XP, Windows Vista, Windows 7, Windows
    8, and Linux (limited) that ties together a few open-source tools
    with a php-based web interface. FOG doesn't use any boot disks, or
    CDs; everything is done via TFTP and PXE. Your PC boots via PXE and
    automatically downloads a small Linux client. From there you can
    select many activities on the PC, including imaging the hard drive.
    Also with FOG many network drivers are built into the Linux
    client's kernel, so you don't really need to worry about nic
    drivers (unless there isn't kernel support for it yet). FOG also
    supports putting an image that came from a computer with a 80GB
    partition onto a machine with a 40GB hard drive as long as the data
    is less than 40GB. FOG supports multi-casting, meaning that you can
    image many PCs from the same stream. So it should be as fast whether
    you are imaging 1 PC or 20 PCs.

**How should FOG be implemented?** FOG is best implemented on a
dedicated server, any spare machine you have. We recommend that you have
**sufficient** hard drive space as each image you make is usually
between 5 and 10 GB. Using a RAID array allows imaging multiple
computers simultaneously without much performance degradation. A
**gigabit NIC** is recommended. For faster image compression and
decompression, provide as much processor and RAM as you can make
available.

**What features are included with FOG?** FOG is more than just an
imaging solution, FOG has grown into an imaging/cloning and network
management solution. FOG now performs tasks like installing and managing
printers, tracking user access to computers, installing applications
remotely via snap-ins, automatic user log offs and computer shutdown on
idle timeouts. If a computer is badly infected with a virus or malware,
you can boot FOG in AV mode and have it remove the viruses. You can wipe
your disks, destroying all information that was on them, restore deleted
files, or scan the disk for bad blocks.

**How much does FOG cost?** FOG is an Open Source project and licensed
under the GPL which means that you are free to use FOG on as many
computers as you like for free. This also means that if you want to make
any changes to the source code you are free to do so.

The creators of FOG make no profits from this project with the exception
of donations. FOG comes with absolutely **NO WARRANTY** and the creators
of FOG are in **NO WAY RESPONSIBLE FOR ANY DAMAGE OR LOSS CAUSED BY
FOG!** Please see the license file included with the FOG release for
more information. With that being said we attempt to do a very good job
of supporting our users, in fact it is one of the goals of FOG to have
better support than most commercial products. All support requests
should be placed through the FOG's forum which is located at:

\<<http://fogproject.org/forum/>\>

Thanks for supporting open source software and enjoy!

### Background on FOG

-   **Why FOG?** Working in an educational environment our
    organization's techs very often re-imaged computers in their day to
    day activities. For a long time we used a commercial product that in
    many ways didn't meet our needs. It wasn't web based, and you
    needed to create driver disks, floppys or USB drives. Other things
    were very difficult, such as searching for a host by MAC address and
    the product was expensive, even with an educational discount. So we
    started to investigate ways in which we could do things better, and
    as our organization struggled to make a commercial product work
    better by trying to pxe boot dos, and testing it in Windows PE, we,
    the FOG Team started to build linux based solution on our own time.
    We finally got a working version and decided to release it as open
    source since we use many other open source products, and figured we
    should give back to the community.

### Fundamental Concepts

This section provides some basic concepts that the FOG Project uses.

**PXE Network Bootstrap loading** What is iPXE and the difference
between the files? Check out the \[iPXE\](/customization/iPXE) page.

## Installing FOG

FOG is a typical
*\[LAMP\](http://en.wikipedia.org/wiki/LAMP\_%28software_bundle%29)*
software bundle, so the main server is a **L**inux box. The rest of the
components: **A**pache, **M**ySQL, **P**HP, and several other services,
are automatically downloaded and installed by the FOG installation
script.

### Requirements

This listing is for informational purposes only, as the required
components will be automatically downloaded and installed by the FOG
installation script.

-   PHP 5.3.0+
-   MySql 5+
-   Apache 2+

The LAMP setup can also be easily adjusted for a \"WAMP (Windows Apache
MySQL PHP) system\" though will require a bit more knowledge of what
packages to use and how to integrate with the FOG system.

### Installation on different distributions of Linux

-   Find here step-by-step guides written for your favorite flavor of
    Linux: [Installation manuals](Installation#Installation_manuals)

------------------------------------------------------------------------

## Network Integration

### Basic Network Setup

The FOG setup script asks several questions which might not be obvious.
These sections describe only the most generic settings.

-   **Isolated Network** The easiest method to image machines and get
    started using FOG is on a small, isolated network. The FOG setup
    program will configure all the necessary services for you completely
    automatically. This section covers only those basic steps. **See
    \[FOG on an Isolated Network\](FOG_on_an_Isolated_Network
    \"wikilink\")**

**Integrating FOG Server with Existing Network Systems** Slightly more
complicated is the task of integrating FOG into your existing network
infrastructure. This section attempts to describe the steps to link FOG
with a fairly generic enterprise system. **See \[Integrating FOG into an
Existing Network\](Integrating_FOG_into_an_Existing_Network
\"wikilink\")**

### Advanced Network Setup

#### Integrating FOG Server with Existing Network Systems in non
intrusive mode using MAC filtration

This methods allows to use Fog in existing network without the need of
controlling existing DHCP server. Requires you to input the MAC address
of FOG clients. See \[Integrating FOG into an Existing Network in non
intrusive
mode\](Integrating_FOG_into_an_Existing_Network_in_non_intrusive_mode
\"wikilink\")

#### Integrating FOG server into an existing network in non intrusive
mode using ProxyDHCP

This methods allows to use Fog in existing network without the need of
controlling existing DHCP server. Does NOT required you to input the MAC
addresses of FOG clients. See \[Setting up
ProxyDHCP\](Setting_up_ProxyDHCP \"wikilink\").

#### Wake On Lan (WOL)

-   \[Cisco WOL - Layer 3\](Cisco_Wake_on_lan \"wikilink\")
-   \[ProCurve WOL\](ProCurve_Wake_on_lan \"wikilink\")

#### Multicast/UDPCast

-   \[Cisco Multicast - Layer 3\](Cisco_Multi_Cast \"wikilink\")

\<!\-- \-:octicons-arrow-right-24:

-   \[HP Multicast - Layer 2&3\](HPMulticast \"wikilink\")

#### Full Listing of Ports used by FOG server and client

MySQL - 3306 FTP -- tcp 20,21 SSH -- tcp 22 TFTP -- udp 69 HTTP(s) --
tcp 80,443 Portmap -- tcp/udp 111 NFS -- tcp/udp 2049 Transfer ports --
tcp/udp 1024 -- 65535 As found at:
\<<http://fogproject.org/forum/threads/firewall-config.27/>\>

## Getting Started

### Quick Start - Basic Tasks

So you have a FOG server installed and setup, now what do you do? Below
are a few common \"Getting Started\" items.

1.  \[Booting into FOG and Capturing your first
    Image\](Booting_into_FOG_and_Capturing_your_first_Image
    \"wikilink\")
2.  \[Deploying your Image a single
    client\](Deploying_your_Image_a_single_client \"wikilink\")
3.  \[Deploying your Image a group of
    clients\](Deploying_your_Image_a_group_of_clients \"wikilink\")

### Tips

1.  FOG requires that all hosts be entered in the FOG Database for
    imaging. The most important part is getting the MAC address of the
    host right. FOG uses the MAC for targeting image installs and
    acquires. Using the wrong MAC could result in unpredictable results,
    including the complete erasure of the wrong pc! The IP address isn't
    that important, and the 'name' field is more for the user. Mac
    address format is 00:12:3F:C4:57:0C . Using dashes, spaces, or no
    items at all will result in the GUI not accepting the host.
2.  After hosts are entered, it is wise to group them together by
    function, hardware, or common image. The image will be shared among
    all members of a particular group. This occurs within the 'hosts'
    screen, and NOT on the groups screen. This is a little confusing, so
    it helps to think of the 'groups' screen as a task generator, rather
    than controlling group memberships.
3.  For importing hosts in a .csv file follow the format below: 1 line
    per host: \"00:c0:4f:18:62:63\",\"Hostname\",\"1.1.1.1\",\"Your
    description\",\"XP/Vista\",\"Image filename to use\"
4.  Hosts are then configured to boot via PXE boot by going into the
    BIOS. Make sure PXE boot is the FIRST option, NOT the hard disk, or
    things won't work.
5.  Configure your 'master' pc for the first image. Probably a good idea
    to run '\[sysprep\](<http://support.microsoft.com/kb/302577>)' prior
    to imaging, but not necessary. Sysprep will make your imaging life
    easier, if hardware is different, etc. See Microsoft.com for more
    details on using sysprep.

## Preparing a HOST for Cloning

-   Key Term: Host \--&gt; The computer that will be registered to FOG
    and imaged(capture/deploy). Client usually refers to the Client
    service later described in this guide.

FOG's strength can be better harnessed if some time and work is put
into preparing a master image that fits the needs of your environment.
This section covers Host preparation steps that will save you time and
headaches like:

Setting a \[Default User Profile\](Client_Setup#Set_up_Default_Profile
\"wikilink\") Installing Windows Updates Pre-Installing the \[FOG
service\](Client_Setup#Final\_[Steps_Before_Imaging]().2F_Before_Sysprep
\"wikilink\"), etc.

It also covers more advanced ideas that are guaranteed to *cause*
headaches, like:

Sysprep, \[Hardware-Independent Images
(HAL)\](Client_Setup#Hardware-[Independent_Images]()-\_Understand_HAL
\"wikilink\"), and Driver integration.

Read more about *\[Host Setup\](Client_Setup \"wikilink\")*

## FOG Benchmarks

### \[Internal Benchmarks\](Internal_Benchmarks \"wikilink\")

## Managing FOG

The FOG web interface is your primary management console. It is very
well-documented in the pages linked below: ===The Main \[Managing
FOG\](Managing_FOG \"wikilink\") Document=== The link above opens the
Main Managing FOG document and has a Table of Contents of its own.
Subcategories within the Managing Fog section include the following
sections:

-   **Understanding the FOG \[Dashboard\](Managing_FOG#Dashboard
    \"wikilink\")** Provides an overview of the GUI and explains the
    symbols used on the \[Menu Bar\](Managing_FOG#Menu_Bar
    \"wikilink\").
-   **Managing \[Hosts\](Managing_FOG#Hosts \"wikilink\")** This section
    covers management tasks such as: \[Adding a new
    host\](Managing_FOG#Adding_a_new_host \"wikilink\"), \[Managing
    Hosts\](Managing_FOG#Managing_Hosts \"wikilink\"), \[Host
    Status\](Managing_FOG#Host_Status \"wikilink\"), and \[Creating Host
    Groups\](Managing_FOG#Creating_Host_Groups \"wikilink\").
-   **Managing \[Groups of Hosts\](Managing_FOG#Groups \"wikilink\")**
    This section provides an \[Overview\](Managing_FOG#Groups
    \"wikilink\") of sorting hosts into useful Groups, and provides
    instruction on \[Managing Groups\](Managing_FOG#Managing_Groups
    \"wikilink\").
-   **Defining and Managing \[Images\](Managing_FOG#Images
    \"wikilink\")** Defines types of images: Single Partition \|
    Multiple Partition -Single Disk \| Multiple Partition - All Disks \|
    Raw Image Also describes
    \[Creating\](Managing_FOG#Creating_Images_Objects \"wikilink\"),
    \[Modifying Image Objects\](Managing_FOG#Modifying_Image_Objects
    \"wikilink\"), and \[Adding Images to Existing
    Objects\](Managing_FOG#Adding_Existing_Image_Objects \"wikilink\").
-   **\[Storage Management\](Managing_FOG#Storage_Management
    \"wikilink\") -adding additional Storage Nodes** This section
    introduces the \[concept of Storage
    Nodes\](Managing_FOG#Storage_Management \"wikilink\"), which provide
    scalability to FOG with the ability to \"share the load of computers
    being imaged.\" Also covered are \[Adding Storage
    Nodes\](Managing_FOG#Adding_a_Storage_Node \"wikilink\"), Monitoring
    \[Image Replication\](Managing_FOG#Monitoring_The_Master_Node
    \"wikilink\") between nodes, and Understanding the \[role of the
    \"Master Node\"\](Managing_FOG#Master_Node_Status \"wikilink\") in a
    group. In addition, this section details the necessary steps to
    \[include PXE and TFTP
    Services\](Managing_FOG#Including\_[multiple_PXE]().2F_TFTP_servers
    \"wikilink\") for a node located on a remote network segment.
-   **Defining types of \[Administrative FOG Users\](Managing_FOG#Users
    \"wikilink\")** The difference between a regular FOG user and a
    \[Mobile user\](Managing_FOG#Overview_7 \"wikilink\") Also covered
    are \[Creating\](Managing_FOG#Creating_Accounts \"wikilink\") and
    \[Modifying\](Managing_FOG#Modifying_Users \"wikilink\") FOG user
    accounts

## FOG \[Tasks\](Managing_FOG#Tasks \"wikilink\")

This is a major section of FOG Management because all day-to-day client
management is initiated within the FOG Tasks section. The \[Overview
Section\](Managing_FOG#Overview_8 \"wikilink\") provides a quick list of
tasks available within FOG. \[General Tasks\](Managing_FOG#General_Tasks
\"wikilink\") - Basic Imaging Tasks:

Capturing an image (includes video tutorial) Deploying an image
Multicasting

\[Advanced Tasks\](Managing_FOG#Advanced_Tasks \"wikilink\") - Describes
tasks other than imaging:

Debug Capture - Unicast (Debug) Send - Unicast (Debug) Send - Unicast
(Without Snapins) Deploy All Snapins Deploy Single Snapin Memory Test
Wake Up Fast Wipe Normal Wipe Full Wipe Disk Surface Test File Recovery
Virus Scan Hardware Inventory Donate Torrent-Cast

### Delayed Tasks, or \[Scheduling Tasks\](Managing_FOG#Scheduling
\"wikilink\") in the future

Describes advanced settings available for scheduling tasks including
Shutdown after Execution, \[Single
Task\](Managing_FOG#Single_Execution_Scheduling \"wikilink\")
scheduling, and \[setting a CRON-Style
Task\](Managing_FOG#Cron_Style_Task_Scheduling \"wikilink\").

### \[Adding Printers\](Managing_FOG#Printers \"wikilink\") to FOG

How to add printers to FOG. This allows the \[FOG Service to manage
printers\](Managing_FOG#Printer_Manager \"wikilink\") on FOG Clients

## The \[FOG Client Service\](Managing_FOG#The_FOG_Client_Service
\"wikilink\")

### Legacy Client

-   A service that runs on client computers allowing FOG to better
    manage them. Provides Active Directory integration, the ability to
    change a Hostname, Green Power management, Snap-in installation,
    User tracking, Printer Management, and more.

For FOG 1.3.0 Power Management, see \[Power
Management\](Power_Management \"wikilink\").

-   The FOG client can be partially or fully-enabled by \[modifying the
    ini file.\](Managing_FOG#Module_specific_configuration_settings
    \"wikilink\")

#### \[Installing\](Managing_FOG#Installation \"wikilink\") the FOG
Client

-   **\[Client install location\](Managing_FOG#Installation
    \"wikilink\")**
    -   After installing FOG server on your machine, log into the web
        gui. If you take note of the Footer of every page of the web gui
        you will see a few links there. One being the FOG Client. This
        link will take you to the Client Management page. Here is where
        you will find the Legacy Client and New Client services, along
        with FOG Crypt.
    -   **NOTE:** It is not recommended to use the Legacy and New Client
        services in the same environment.
-   A typical client installation, Silent installation, and a video
    tutorial.

#### Advanced Description of \[FOG
Services\](Managing_FOG#Functions_and_Operation \"wikilink\")

More detail on: ::Auto Log Out Hostname Changer Host Register Task
Reboot Directory Cleaner Display Manager \[Green FOG\](Green_FOG
\"wikilink\") Snapin Client User Tracker User Cleanup Printer Manager
Client Updater

#### Firewall Exceptions

-   Run these in Administrative Command Prompt (cmd) on the host to
    allow communication between the FOG Client Service installed on the
    Host and the FOG Server
-   Past setups suggested disabling the firewall, but this is less
    secure

##### x86 (32bit)

> netsh advfirewall firewall add rule name=\"Fog Client\" dir=in
> action=allow program=\"%ProgramFiles%FOGFOGService.exe\" netsh
> advfirewall firewall add rule name=\"Fog Service\" dir=in action=allow
> program=\"%ProgramFiles%FOGFOGServiceConfig.exe\" netsh advfirewall
> firewall add rule name=\"Fog Tray\" dir=in action=allow
> program=\"%ProgramFiles%FOGFOGTray.exe\"

##### x64 (64bit)

> netsh advfirewall firewall add rule name=\"Fog Client\" dir=in
> action=allow program=\"%ProgramFiles(x86)%FOGFOGService.exe\" netsh
> advfirewall firewall add rule name=\"Fog Service\" dir=in action=allow
> program=\"%ProgramFiles(x86)%FOGFOGServiceConfig.exe\" netsh
> advfirewall firewall add rule name=\"Fog Tray\" dir=in action=allow
> program=\"%ProgramFiles(x86)%FOGFOGTray.exe\"

#### \[Updating\](Managing_FOG#Keeping_Clients_up_to_date \"wikilink\")
the FOG Client

How to update the FOG client.

#### The \[FOG Tray\](Managing_FOG#FOG_Tray \"wikilink\")

Describes the Windows application that runs in the taskbar

#### \[Troubleshooting\](Managing_FOG#Troubleshooting \"wikilink\") the
FOG Client

Logs are usually located at \<font color=\"red\"\>C:fog.log\</font\>. If
the log is not here, this generally means the log path was changed
during installation, and is probably in fog's program directory.

## Snap-ins

-   A FOG \[Snap-in\](Managing_FOG#Snap-ins \"wikilink\") is anything
    that can be run on a Windows client. This can be *just about
    anything*, including: installing applications like Firefox or
    Microsoft Office, adding an icon or shortcut to the desktop, or
    tweaking a registry key. This section covers \[Creating a
    Snap-in\](Managing_FOG#Creating\_[a_Snapin]().2F_Overview
    \"wikilink\"), adjusting the FOG server to handle snap-ins \[larger
    than 2MB\](Managing_FOG#Preparing_the_FOG_Server \"wikilink\"),
    \[Uploading the Snap-in\](Managing_FOG#Uploading_the_Snapin
    \"wikilink\") into the FOG system, and
    \[Linking\](Managing_FOG#Linking_the_Snapin_to_Hosts \"wikilink\")
    the Snap-in to hosts.

## FOG Plugins

Plugins enhance FOG's functionality. See \[Plugins\](Plugins
\"wikilink\") to activate and manage plugins.

### LDAP Plugin

-   Allows you to link with a LDAP server to add an user validation
-   You can add mulitple LDAP servers
-   You can config the DN base and the port of the LDAP Server
-   If FOG can not connect with the LDAP Server, FOG tries to do a local
    validation
-   If the user does not exist, FOG create one with the mobile profile

### Location Plugin

-   Allows you to direct hosts at separate locations and manage through
    a centralized server
-   Hosts will be imaged from their location setup, rather than trying
    to pull from a random node/server across, potentially, WAN links
-   Same works for \"Tftp\" in that it will direct the host to get it's
    kernel and init from it's related location
-   Can also be used to direct the host to download it's snapins from
    the relevant location

### Access Control Plugin

-   \<span style=\"background-color:RED; padding: 1px\"\> **Removed in
    1.3.0** \</span\>
-   To give a layer of security and control over the task and imaging
    processes as well as limit the GUI items from \"designated\"
    controls
-   For Example: IT vs. Regular User

### Capone Plugin

-   Ideally for retail markets and computer shops
-   The Capone plugin allows FOG to recognize similar hardware platforms
    and push your specified image to them with minimal (or no)
    interaction
-   In FOG terms a \"Quick Image\" without any registration
-   As of FOG v1.3.0-r2651 the fog user can now add Image Deploy to the
    Fog iPXE Menu(For All Hosts) and then select the exact image desired
    without having to do any registration. BUT intervention is still
    required to start imaging.

### WOL Broadcast Plugin

-   Allowing the Fog user to specify different broadcast address on your
    network
-   WOL will use those set values to send the WOL Packets to the
    broadcast addresses, rather than staying only on layer 2
-   WOL packets operate at the layer 2 of a network meaning that it can
    only reach it's \"Subnet\"
-   WOL Broadcast directly tells a packet to send to other broadcast
    addresses so that it network passes on the traffic

### Example Plugin

-   If you would like to create your own plugins here is a template to
    follow.

## FOG Server Maintenance

-   \[Backing up FOG\](Backing_up_FOG \"wikilink\")
-   \[Restoring FOG from Backup\](Restoring_FOG_from_Backup
    \"wikilink\")
-   \[Upgrading the FOG Server\](Upgrading_the_FOG_Server \"wikilink\")

## Advanced Installations

### Separate TFTP and DHCP Server

In this setup, the TFTP server and the DHCP server are hosted on a
separate server. The TFTP server holds the PXE boot files including the
Linux Kernel, boot file system image, and pxe config files. The DHCP
server is the server that assigns the clients with IP addresses and
network connection information.

Click here for detailed steps: \[Separate TFTP and DHCP
Server\](Separate_TFTP_and_DHCP_Server \"wikilink\")

### Additional TFTP / DHCP Server on separate subnet

This setup allows FOG to manage systems at a remote network location by
installing the necessary services to allow clients to PXE boot to a
Storage Node: \[Including multiple PXE / TFTP
servers\](Multiple_TFTP_servers \"wikilink\")

This extends the work done in the above article, \[Including multiple
PXE / TFTP servers\](Multiple_TFTP_servers \"wikilink\"), and extends it
a bit to allow for FOG nodes to be used in various locations that pull
from a central server. \[ Using remote FOG nodes for distributed
deployment\](Fog_deployment_nodes \"wikilink\")

### Separate NFS Server

Edit the storage node definition with the IP address of your NFS server
and set the image location to the path on the nfs server. Make sure it
has a file called .mntcheck in the root of the share, a directory called
dev and a .mntcheck file in the dev folder.

if you want to mount it on the fog server too, follow these steps:-

-   mv /images /imagesold
-   mkdir /images
-   edit /etc/fstab

For example if your server name is mynfsserver and the share on it is
called fogimages

> mynfsserver:/fogimages /images nfs defaults 0 0

then type

> mount -a

**KNOWN ISSUE** You will get an error \"Ftp connection to storage server
has failed\" at the end of capturing images though. You will have to
manually rename and move the file from the dev directory to the
directory below.

If your NFS server supports ftp as well, enable ftp on it too with the
username and password specified in the storage server settings and this
message will go away.

Hopefully someone will re-write POST_Stage2.php to change this at some
point as if you already have the NFS share mounted why do we do this bit
with ftp?

You may also get an infinite loop of the following \<<message:->\>

> \"Unable to find a valid task ID based on the clients mac address of:
> \<mac address\>\".

if you add an @ sign before the ftp commands it appears to have fixed
the issue.

so line 133 of /var/www/fog/service/Post_Stage2.php would look like this

> if (@ftp_rename ( \$ftp, \$src, \$dest ) \|\| \@ftp_rename ( \$ftp,
> \$srcdd, \$dest ))

### Change NFS location

This is **not about a seperate NFS server** in general, but about how to
**change the local storage directory** and export it correctly.

See \[Change NFS location\](Change_NFS_location \"wikilink\") for more.

## Upgrading to Trunk

-   \<span style=\"background-color:Yellow;\"\>Trunk installs are almost
    always buggy.\</span\> This is bleeding edge and if you wish to
    update to trunk be prepared to update at least once a week or even
    once a day. At all times developers are making changes to correct
    problems
-   \[Upgrade_to_trunk\](Upgrade_to_trunk \"wikilink\")

## Other Advanced Topics

-   \[Building a Custom Kernel\](Building_a_Custom_Kernel \"wikilink\")
-   \[Creating Custom FOG Service
    Modules\](Creating_Custom_FOG_Service_Modules \"wikilink\")
-   \[Modifying the Init Image\](Modifying_the_Init_Image \"wikilink\")
-   \[Translating FOG\](Translating_FOG \"wikilink\")
-   \[Fog Tweaks\](Fog_Tweaks \"wikilink\")
-   \[Bypass Host Registration\](Bypass_Host_Registration \"wikilink\")
-   \[Building undionly.kpxe\](Building_undionly.kpxe \"wikilink\")
-   \[Chainloading PXE to iPXE using
    pxelinux.0\](Chainloading_PXE_to_iPXE_using_pxelinux.0 \"wikilink\")
-   \[Auto driver Install\](Auto_driver_Install \"wikilink\")

## Troubleshooting

This section is intended to bring together the most common issues from
the \[forums\](<http://www.fogproject.org/forum>).

### Troubleshooting Installation and Configuration Issues

-   \[Knowledge Base\](Knowledge_Base \"wikilink\")
-   \[Password Central\](Password_Central \"wikilink\")
-   \[Troubleshooting an image push to a
    client\](Troubleshooting_an_image_push_to_a_client \"wikilink\")
-   \[Troubleshooting a capture\](Troubleshooting_a_capture
    \"wikilink\")
-   \[ Troubleshooting a multicast\](Multicasting \"wikilink\")
-   \[Troubleshooting Driver Issues\](Troubleshooting_Driver_Issues
    \"wikilink\")
-   \[Speeding up the Graphical User
    Interface\](Speeding_up_the_Graphical_User_Interface \"wikilink\")
-   \[Bottleneck\](Bottleneck \"wikilink\") / Imaging Speed Issues
-   \[Advanced_Boot_Menu_Configuration_options\](Advanced_Boot_Menu_Configuration_options
    \"wikilink\")
-   \[Troubleshooting Host Management Showing Hosts as
    Down\](Troubleshooting_Host_Management_Showing_Hosts_as_Down
    \"wikilink\")
-   \[Troubleshoot_TFTP\](Troubleshoot_TFTP \"wikilink\")

## Appendix C: Alternative Resources

For Microsoft sysprep information, see this page:
\<<http://vernalex.com/guides/sysprep/video.shtml>\>

FOG install HOWTO:
\<<http://www.howtoforge.com/installing-fog-computer-imaging-solution-on-fedora8>\>

FOG sourceforge page: \<<http://freeghost.sf.net/>\>

Deployment Forum at Edugeek contains many Fog related threads
\<<http://www.edugeek.net/forums/o-s-deployment/>\>
