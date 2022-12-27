---
title: JDK 라이센스(LISENCE)
description: Oracle JDK 라이센스 이슈와 오픈 소스 대안에 대하여...
published: true
date: 2022-12-27T09:59:07.690Z
tags: java, jdk, lisence
editor: markdown
dateCreated: 2022-12-27T09:54:47.450Z
---

> 번역 예정
{.is-warning}

## Oracle JDK Lisence

**The Oracle JDK (Java Development Kit) is a version of the JDK that is distributed by Oracle**, the company that develops and maintains the Java programming language. The Oracle JDK is available under a proprietary license that allows users to download and use the software for free, but it also includes some restrictions on how the software can be used and distributed.

The Oracle JDK license includes terms that specify how the software can be used and distributed. For example, the license allows users to use the Oracle JDK to develop, test, and deploy Java applications, **but it prohibits users from distributing the Oracle JDK as part of a commercial product or service.** Additionally, the license requires users to include certain notices and disclaimers when distributing Java applications that use the Oracle JDK.

**It's important to note that the Oracle JDK is not the only version of the JDK available.** There are also versions of the JDK that are released under open source licenses, such as the OpenJDK, which allows users to modify and distribute the software without incurring any additional licensing fees.

### Oracle JDK in Commercial Applications

**Using the Oracle JDK in commercial applications can potentially give rise to licensing issues** if the terms of the Oracle JDK license are not followed. The Oracle JDK license allows users to use the software to develop, test, and deploy Java applications, but it prohibits users from distributing the Oracle JDK as part of a commercial product or service.

For example, if a company develops a software product that includes the Oracle JDK as a component and distributes that product to customers, the company would need to obtain a separate license from Oracle in order to do so. **This is because the Oracle JDK license does not allow users to distribute the JDK as part of a commercial product.**

In addition to this, the Oracle JDK license requires users to include certain notices and disclaimers when distributing Java applications that use the Oracle JDK. Failure to include these notices and disclaimers could potentially result in licensing issues.

### How to circumvent commercial application licensing issues with Oracle JDK

There are a few ways in which you can potentially circumvent commercial application licensing issues with the Oracle JDK:

- **Use a different version of the JDK**: Instead of using the Oracle JDK, you could consider using a version of the JDK that is released under an open source license, such as the OpenJDK. This would allow you to use the JDK to develop, test, and deploy your commercial application without incurring any additional licensing fees.

- **Obtain a commercial license from Oracle**: If you need to use the Oracle JDK in your commercial application and are unable to use an alternative version of the JDK, you could potentially obtain a commercial license from Oracle. This would allow you to use the Oracle JDK in your commercial application in accordance with the terms of the license.

- **Avoid distributing the Oracle JDK as part of your commercial application**: Instead of distributing the Oracle JDK as part of your commercial application, you could consider including instructions for users to download and install the Oracle JDK themselves. This would allow you to use the Oracle JDK in your commercial application without violating the terms of the license.

> **What can happen if you violate the Oracle JDK's commercial license?**
> 
> Violating the terms of the Oracle JDK's commercial license can potentially result in legal consequences. The Oracle JDK is licensed under a proprietary license that allows users to download and use the software for free, but it also includes some restrictions on how the software can be used and distributed.
> 
> **If you violate the terms of the Oracle JDK's commercial license, Oracle may choose to take legal action against you in order to enforce the terms of the license. This could potentially include filing a lawsuit against you in order to seek damages or other remedies.**
> 
> It's important to carefully review the terms of the Oracle JDK's commercial license and ensure that you are in compliance with them in order to avoid any potential legal consequences. If you have any questions or concerns about using the Oracle JDK in a commercial application, it's recommended to seek legal advice.
{.is-warning}


## Open source licensed JDKs

There are several versions of the Java Development Kit (JDK) that are released under open source licenses:

- **OpenJDK**: The OpenJDK is an open source implementation of the JDK that is developed and maintained by the OpenJDK community. It is available under the GNU General Public License (GPL) v2 with the Classpath Exception. 

- **AdoptOpenJDK**: AdoptOpenJDK is a version of the OpenJDK that is built and distributed by the AdoptOpenJDK community. It is available under the GPL v2 with the Classpath Exception.

- **Eclipse OpenJ9**: Eclipse OpenJ9 is a version of the JDK that is developed and maintained by the Eclipse Foundation. It is available under the Eclipse Public License (EPL).

- **Amazon Corretto**: Amazon Corretto is a version of the JDK that is developed and maintained by Amazon Web Services. It is available under the GPL v2 with the Classpath Exception.

- **GraalVM**: GraalVM is a high-performance runtime that includes a version of the JDK. It is developed and maintained by Oracle and is available under the GPL v2 with the Classpath Exception.


It's important to note that the above list is not exhaustive and there may be other versions of the JDK that are released under open source licenses.

> **Appendix: Classpath Exception?**
> 
> The Classpath Exception is a clause that is often included in the GNU General Public License (GPL) v2 to allow users to link GPL-licensed software with other software that is not covered by the GPL.
> 
> The Classpath Exception allows users to distribute a combination of GPL-licensed software and other software as long as the GPL-licensed software is used solely for the purpose of running the other software. This means that users are allowed to use GPL-licensed software to run other software, but they are not allowed to modify the GPL-licensed software or distribute it as a standalone product.
> 
> The Classpath Exception is often included in open source software licenses in order to allow users to more easily use the software in conjunction with other software that may be licensed under different terms. It is commonly used in conjunction with the GPL v2 in open source Java projects, such as the OpenJDK and AdoptOpenJDK.

> **Appendix: About AdoptOpenJDK**
>
> AdoptOpenJDK is a version of the Java Development Kit (JDK) that is developed and maintained by the AdoptOpenJDK community. AdoptOpenJDK is an open source implementation of the JDK, which means that it is freely available for anyone to use, modify, and distribute.
>
> AdoptOpenJDK provides pre-built, open source binary releases of the JDK for a variety of platforms, making it easy for users to download and install the JDK on their systems. AdoptOpenJDK also offers long-term support for its binaries through a subscription model, which can be helpful for users who need assistance with using the JDK or who want to ensure that their applications remain compatible with future versions of the JDK.
>
> AdoptOpenJDK is available under the GNU General Public License (GPL) v2 with the Classpath Exception, which allows users to use, modify, and distribute the software as long as they follow the terms of the license.
> 
> AdoptOpenJDK is based on OpenJDK. However, there are a few key differences between the two:
> 
> - **Development and maintenance**: OpenJDK is developed and maintained by the OpenJDK community, while AdoptOpenJDK is developed and maintained by the AdoptOpenJDK community.
> 
> - **License**: Both OpenJDK and AdoptOpenJDK are available under the GNU General Public License (GPL) v2 with the Classpath Exception.
> 
> - **Binaries**: OpenJDK provides open source binary releases of the JDK, while AdoptOpenJDK provides pre-built, open source binaries of the JDK for a variety of platforms.
> 
> - **Support**: OpenJDK does not offer any official support for its binaries, while AdoptOpenJDK offers long-term support for its binaries through a subscription model.
> 
> Both OpenJDK and AdoptOpenJDK are open source implementations of the JDK that can be used to develop, test, and deploy Java applications. The main difference between the two is the way in which they are developed, maintained, and supported.

> **Appendix: GPL v2 license and EPL license**
> 
> The GNU General Public License (GPL) v2 and the Eclipse Public License (EPL) are both open source licenses that are commonly used for software projects. Here is a brief overview of each license:
> 
> - **GNU General Public License (GPL) v2**: The GPL v2 is a widely-used open source license that allows users to freely use, modify, and distribute software as long as they follow the terms of the license. The GPL v2 requires users to distribute any modifications they make to the software under the same license, and it also requires users to make the source code of the software available to others.
> 
> - **Eclipse Public License (EPL)**: The EPL is an open source license that is specifically designed for use with Eclipse-based software. Like the GPL v2, the EPL allows users to freely use, modify, and distribute software as long as they follow the terms of the license. The EPL requires users to distribute any modifications they make to the software under the same license, and it also requires users to make the source code of the software available to others.
> 
> Both the GPL v2 and the EPL are designed to promote the sharing and collaboration of software, and they are commonly used in open source projects. However, there are some differences between the two licenses, and it's important to carefully review the terms of each license before using or distributing software under either of them.

## Additional information about JDKs

There are a few additional things to consider when it comes to JDK licensing:

- **Different versions of the JDK may have different licenses**: It's important to be aware that different versions of the JDK may have different licenses. For example, the Oracle JDK is available under a proprietary license, while the OpenJDK is available under the GNU General Public License (GPL) v2 with the Classpath Exception. It's important to carefully review the terms of the license for the specific version of the JDK you are using to ensure that you are in compliance with them.

- **Using the JDK to develop commercial applications may require a commercial license**: If you are using the JDK to develop commercial applications, you may need to obtain a commercial license from the provider of the JDK in order to do so. This is particularly the case with the Oracle JDK, which prohibits users from distributing the JDK as part of a commercial product or service without a separate commercial license.

- **Using the JDK may require you to include certain notices and disclaimers**: Some versions of the JDK, such as the Oracle JDK, may require you to include certain notices and disclaimers when distributing applications that use the JDK. It's important to carefully review the terms of the license for the specific version of the JDK you are using to ensure that you are including the required notices and disclaimers.

- **Licensing issues can be complex**: JDK licensing can be a complex topic, and it's important to seek legal advice if you have any questions or concerns about using the JDK in your projects.

