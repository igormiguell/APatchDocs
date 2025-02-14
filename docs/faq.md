# FAQ

## What is APatch?

::: info
[Here](/what-is-apatch) is a more complete introduction.
:::

APatch is a root solution similar to Magisk or KernelSU which is one of the best of both. It combines Magisk easy and convenient installation method via `boot.img` with KernelSU powerful kernel patching abilities.

## What is the difference of APatch and Magisk?

Magisk modifies the `init` system with a patch to the `ramdisk` of your boot image. APatch patches the kernel directly.

## What is the difference of APatch and KernelSU?

KernelSU requires your device's kernel source code, which is not always provided by the OEM. APatch only need your stock `boot.img`.

## What is the difference of APatch, Magisk and KernelSU?

APatch allows you to optionally not modify SELinux, this means the app thread can be rooted without `libsu` and `IPC`.

**KPModule** provided.

## What is KPModule?

KPM is a module that runs in kernel space and allows code to execute in kernel space, similar to **Loadable Kernel Modules** (LKM).

Additionally, the KPM provides the ability to execute `inline-hook` and `syscall-table-hook` in kernel space.

Please read [How to write KPM](https://github.com/bmax121/KernelPatch/blob/main/doc/zh-CN/module.md) for more information.

## What is the relationship of APatch and KernelPatch?

APatch relies on KernelPatch. It inherits all of its capabilities and has been expanded.

You can install just KernelPatch, but this does not allow you to use APM.

[Learn more about KernelPatch](https://github.com/bmax121/KernelPatch).

## What is SuperKey？

KernelPatch adds a new system call (syscall) to provide all capabilities to apps and programs in userspace, this syscall is referred to as **SuperCall**. When an app/program tries to invoke **SuperCall**, it needs to provide an access credential, known as the **SuperKey**. **SuperCall** can only be successfully invoked if the **SuperKey** is correct and if it's not the caller will remain unaffected.

## How to process the SELinux?

KernelPatch not modify the SELinux context but bypasses SELinux via hook. This allows you to root an Android thread within the app context without the need to use `libsu` to start a new process and then perform `IPC`.

In addition, APatch uses the `magiskpolicy` to add addition support of SELinux directly. 

## WebUI of APM/KPM

The APatch source code has been derived and modified from KernelSU, so APatch introduced WebUI feature in version [10568](https://github.com/bmax121/APatch/releases/tag/10568) after KernelSU introduced WebUI feature.

APatch WebUI implementation and requirements is completely same as KernelSU, WebUI designed for KernelSU modules can run perfectly in APatch.

If you want to design WebUI for APM or KPM, please refer to the [WebUI introduction](https://kernelsu.org/guide/module-webui.html) of KernelSU for further information.

## Can not install modules (os error 2/5/22)?

Remove the root permission of "Shell" app in SuperUser page.

## App granted/lost root permission automatically when rebooting device?

Read [this](https://t.me/APatchChannel/74) for more details.

## Can I use LSPosed?

LSPosed relies on Riru or Zygisk to run, but APatch does not support Riru or Zygisk by default, so you can not use LSPosed directly.

However, APatch can add the Zygisk support or allow LSPosed run without any Zygisk implementation enabled by installing APMs.

Here are two solutions about running LSPosed on APatch:

1. Refer to [Zygisk support?](#zygisk-support) part to add the Zygisk support.
2. If you only need to use LSPosed without other Zygisk features, you can try [Zloader](https://github.com/Mufanc/z-loader) [for LSPosed](https://t.me/mufanc_chan/28) to load LSPosed simply.

::: warning
Zloader is **NOT** compatible with any Zygisk implementation, and you can not use any APMs depend on Zygisk either. Please disable or uninstall any Zygisk implementation before using Zloader.
:::

::: danger
Zloader had **NO** code commits or new version releases after version `0.1.3` released.

We no longer recommends using this method, please consider using Zygisk instead.
:::

## Can not use Shamiko?

We can not support Shamiko due to its proprietary.

::: danger
**Any issues caused by using Shamiko will not be supported by APatch developers, use as your own risk.**
:::

## Zygisk support? {#zygisk-support}

Same as KernelSU, APatch does not have built-in Zygisk support.

Thanks to the commitment of community, there is already had several APMs or APatch compatible Magisk modules which can be used to provide Zygisk support for APatch. Here are some APMs that provide Zygisk support:

- [ZygiskNext](https://github.com/Dr-TSNG/ZygiskNext): The earlist APM that provides Zygisk environment for KernelSU, with most-completed functions supported. It's a full implementation of Zygisk API, and provides some extra features based on or outside of Zygisk. The release version `0.9.1.1` and any other releases before it are free software, releases after this version are proprietary. This APM initially supports APatch at version `1.0.3`.

- [Zygisk_mod](https://github.com/Admirepowered/Zygisk_mod): Before ZygiskNext officially supports APatch, this APM was set to provides Zygisk environment for APatch. With ZygiskNext's officially supports APatch, this APM has been stopped update and archived.

- [ReZygisk](https://github.com/PerformanC/ReZygisk): A free Zygisk implementation appeared after ZygiskNext become proprietary, still in early development, and some feature in ZygiskNext is not supported at this APM.

- [NeoZygisk](https://github.com/JingMatrix/NeoZygisk): An another free Zygisk implementation after the implementations above, which only aims to provide a minimal Zygisk API and remove any other parts. Its Zygisk API Design is directly derives from the Magisk's Zygisk API Design, so this implementation should be most similar to Magisk's Built-in Zygisk in theory.

You can choose one of Zygisk implementations above, or use your own Zygisk implementation.

::: warning

As we said above, APatch **does NOT** have built-in Zygisk support, so we **CAN NOT** and **WILL NOT** guarantee the avalibility, usability, stability or any other warrenties about any elements related to Zygisk. 

If you run into a trouble with APatch when using any Zygisk implementation and/or any modules depends on Zygisk, **DO NOT** report your bug directly to us, report bug to the developer(s) of the APM first instead.

:::

## Cannot pass the root-detecting app?

If your software is working properly, don't worry too much about the detection software.
