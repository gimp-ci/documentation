# GIMP CI Documentation

This is centralized documentation which helps to onboard a new maintainer or
contributor to the [GIMP CI system][build].

# Project Goals

* Make configuration of the [GIMP CI system][build] transparent for developers
  and contributors.
* Provide a means for contributors of [GIMP][gimp] to easily provision a
  development environment for building GIMP.
* Make use of modern technologies and concepts such as infrastructure as code,
  continuous integration, and continuous delivery.

The above goals will be met when a contributor is able to:

1. Fully provision a Jenkins build system for building GIMP.
2. Fully provision a GIMP development environment for contributing to GIMP.

# Developing new infrastructure

If you need to develop new infrastructure as code, then it should be broken out
into Ansible roles and referenced by Ansible playbooks.  See [creating ansible
roles](creating-ansible-roles.md).

# About build.gimp.org

* Point of Contact: [Sam Gleske](https://github.com/samrocketman)
* Sponsors: [flamingtext][ft] provides hardware for the build system and
  majority of bandwidth.  [The GNOME Foundation][gnome] provides the HTTP load
  balancer.
* Currently, none of the automation scripts are being used to configure
  [build.gimp.org][build].  The automation scripts are being developed to
  replace it.

There is an HTTP load balancer in front of GIMP build server controlled by the
[GNOME infrastructure team][gnome-infra].  SSL is terminated by this load
balancer.

On the back end, the Jenkins build system lives on a virtual machine provided by
[flamingtext][ft].  Host is CentOS 6 and the guest is Debian Testing.  GIMP
developers prefer to develop GIMP on [Debian Testing][debian] so that is the OS
of choice for the GIMP CI system.

Hardware specs:

* CPU: Intel(R) Core(TM) i7 CPU 870 @ 2.93GHz stepping 05 (6 cores available to
  guest)
* RAM: 8GB (4GB available to guest)
* Disk: 2x500GB HDD (150GB available to guest)
* Virtualization Layer: VMWare
* Network speed: Gigabit LAN; dual 100BaseT WAN.

[watchdog is configured][watchdog] on the build system to monitor the health of
Jenkins and repair it automatically.

[build]: https://build.gimp.org/
[debian]: https://www.debian.org/releases/
[ft]: http://www.flamingtext.com/
[gimp]: https://www.gimp.org/
[gnome-infra]: https://mail.gnome.org/mailman/listinfo/gnome-infrastructure
[gnome]: https://www.gnome.org/foundation/
[watchdog]: https://github.com/gimp-ci/misc-scripts/tree/master/watchdog
