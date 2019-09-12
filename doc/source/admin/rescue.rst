.. _admin_rescue:

===========
Rescue mode
===========

Overview
========

Rescue mode is a feature that can be used to boot a ramdisk for a tenant in
case the machine is otherwise inaccessible. For example, if there's a disk
failure that prevents access to another operating system, rescue mode can be
used to diagnose and fix the problem.

Support in ironic-python-agent images
=====================================

Rescue is initiated when ironic-conductor sends the ``finalize_rescue``
command to ironic-python-agent. A user `rescue` is created with a password
provided as an argument to this command. DHCP is then configured to
facilitate network connectivity, thus enabling a user to login to the machine
in rescue mode.

.. warning:: Rescue mode exposes the contents of the ramdisk to the tenant.
             Ensure that any rescue image you build does not contain secrets
             (e.g. sensitive clean steps, proprietary firmware blobs).

The below has information about supported images that may be built to use
rescue mode.

CoreOS
------

The CoreOS image supports rescue mode when used with DHCP tenant networks. You
may follow the normal process for `building a CoreOS ironic-python-agent
image`_ to create an image that supports rescue mode.

After the ``finalize_rescue`` command completes, DHCP will be configured on all
network interfaces, and a `rescue` user will be created with the specified
``rescue_password``.

TinyIPA
-------

The TinyIPA image supports rescue mode when used with DHCP tenant networks.
No special action is required to `build a TinyIPA image`_ with this support.

After the ``finalize_rescue`` command completes, DHCP will be configured on all
network interfaces, and a `rescue` user will be created with the specified
``rescue_password``.

.. _`building a CoreOS ironic-python-agent image`: https://github.com/openstack/ironic-python-agent/tree/master/imagebuild/coreos/README.rst
.. _`build a TinyIPA image`: https://github.com/openstack/ironic-python-agent/tree/master/imagebuild/tinyipa/README.rst
