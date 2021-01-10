---
layout: post
author: puttaraju
title: Virtualization
tags: [Virtualization]
---

Virtual Machine (VM) is a computer that isn’t directly tied to any physical hardware.
* VMs run operating systems on virtual CPUs (VCPUs) with their own virtual address spaces and virtual devices
* VMs present OSs with an environment that looks and feels like physical hardware, but is actually created entirely within software!
* By abstracting away any concrete physical hardware, VMs make it possible for a single computer to run multiple virtualized OSs simultaneously

Hypervisors : programs responsible for setting up and managing VMs,
* single hypervisor “host” typically managing one or more individual VM “guests.”
* Some well-known hypervisors include VirtualBox, VMware, Parallels, and QEMU and crosvm!

![KVM and Qemu](https://upload.wikimedia.org/wikipedia/commons/thumb/4/40/Kernel-based_Virtual_Machine.svg/500px-Kernel-based_Virtual_Machine.svg.png "KVM")

KVM, the Kernel-based Virtual Machine, is a Type 1 hypervisor that’s built directly into the Linux kernel itself
* KVM is implemented as a kernel module, allowing Linux to become a hypervisor simply by loading a module
- KVM provides full virtualization on hardware platforms that provide hypervisor instruction support (such as the Intel VT ,AMD-V)
+ KVM also supports paravirtualized guests, including Linux and Windows

CROSVM: https://chromium.googlesource.com/chromiumos/platform/crosvm/
* crosvm is a Virtual Machine Manager (VMM), or Type 2 hypervisor, crosvm is a lot like VirtualBox or QEMU (but QEMU/Virtualbox are general purpose VMMs)
* first VMM written in Rust. Rust’s strong memory and data-race safety and excellent C interoperability makes it a fantastic language for writing VMMs
* It only implements just enough functionality to run lightweight, secure, and performant Linux VMs
* Firecracker is a fork of crosvm that’s being developed by Amazon to speed up their serverless infrastructure
* Crosvm and Firecracker are not general purpose VMMs, but are designed to do the bare minimum to virtualize a Linux kernel, which gives them performance and code size benefits over general purpose VMMs like QEMU. Hence Firecracker is also termed as MicroVM by Amazon
* Crosvm depends on libminijail
* It runs entirely in userspace and works in tandem with KVM’s kernel component to set up and execute VMs
* crosvm defines the virtual hardware platform and memory-layout of a VM, manages the execution lifecycle of the VM

Crostini: Crostini in chromeos gives users a local Debian-based Linux environment
* Crostini provides collection of tools and infrastructure that enables ChromeOS to run Linux applications within a secure, sandboxed environment
* It provides everything one would expect from a standard Linux installation, such as shell access, root-privileges, permission to install packages, etc…
* To maintain the strict security model of ChromeOS, this environment lives within a container, within a virtual machine
* This double-encapsulation helps to ensure that even if the Linux installation is compromised, the rest of user’s system isn’t compromised along with it

Minijail : provides all of the Linux sandbox features in that one binary
* using single program that can start and enter namespaces, apply seccomp rules, manage capabilities, and so on
* minijail uses Linux capabilities to reduce the privileges a process needs
* minijail uses seccomp to restrict the system calls that processes can make


References

- [Anatomy of KVM](https://developer.ibm.com/tutorials/l-hypervisor/)
