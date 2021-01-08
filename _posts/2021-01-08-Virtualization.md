---
layout: post
author: puttaraju
title: Containers
tags: [VM, Containers]
---

virtual machine (VM) is a computer that isn’t directly tied to any physical hardware.
* VMs run operating systems on virtual CPUs (VCPUs) with their own virtual address spaces and virtual devices
* VMs present OSs with an environment that looks and feels like physical hardware, but is actually created entirely within software!
* By abstracting away any concrete physical hardware, VMs make it possible for a single computer to run multiple virtualized OSs simultaneously

Hypervisors : programs responsible for setting up and managing VMs,
* single hypervisor “host” typically managing one or more individual VM “guests.”
* Some well-known hypervisors include VirtualBox, VMware, Parallels, and QEMU and crosvm!


Crostini: Crostini in chromeos gives users a local Debian-based Linux environment
* Crostini provides collection of tools and infrastructure that enables ChromeOS to run Linux applications within a secure, sandboxed environment.
* It provides everything one would expect from a standard Linux installation, such as shell access, root-privileges, permission to install packages, etc…
* To maintain the strict security model of ChromeOS, this environment lives within a container, within a virtual machine.
* This double-encapsulation helps to ensure that even if the Linux installation is compromised, the rest of user’s system isn’t compromised along with it.


CROSVM: https://chromium.googlesource.com/chromiumos/platform/crosvm/
* crosvm is a lot like VirtualBox or QEMU a Virtual Machine Manager
* first VMM written in Rust.
* It only implements just enough functionality to run lightweight, secure, and performant Linux VMs.
* Rust’s strong memory and data-race safety, expressive syntax, and excellent C interoperability makes it a fantastic language for writing VMMs
* Firecracker is a fork of crosvm that’s being developed by Amazon to speed up their serverless infrastructure.
* Crosvm and Firecracker are not general purpose VMMs, but are designed to do the bare minimum to virtualize a Linux kernel, which gives them performance and code size benefits over general purpose VMMs like QEMU. Hence Firecracker is also termed as MicroVM by Amazon.
* Crosvm depends on libminijail
