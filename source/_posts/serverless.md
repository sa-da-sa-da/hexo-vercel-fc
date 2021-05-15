---
title: 1、serverless到底是个什么鬼
categories: Serverless
tags: Serverless
date: 2021-05-15 16:27:24
updated: 2021-05-15 16:27:24
---

## 什么是 Serverless

要说Serverless是什么，直译过来就是无服务器。根据 CNCF 的定义，Serverless 是指构建和运行不需要服务器管理的应用程序的概念。CloudFlare对其定义：


>Serverless computing is a method of providing backend services on an as-used basis. A Serverless provider allows users to write and deploy code without the hassle of worrying about the underlying infrastructure. A company that gets backend services from a serverless vendor is charged based on their computation and do not have to reserve and pay for a fixed amount of bandwidth or number of servers, as the service is auto-scaling. Note that although called serverless, physical servers are still used but developers do not need to be aware of them.


谷歌翻译过来就是：

>无服务器计算是一种按需提供后端服务的方法。无服务器提供程序允许用户编写和部署代码，而不必担心底层基础结构。从无服务器供应商处获得后端服务的公司将根据其计算费用，而不必保留和支付固定数量的带宽或服务器数量，因为该服务是自动扩展的。请注意，尽管称为无服务器，但仍使用物理服务器，但开发人员无需了解它们。


## Serverless 概述

想象一下，你所在的公司的关键应用程序存在着性能方面的问题。该应用程序需要供客户7*24小时访问使用，在工作期间，CPU和内存使用率都应经达到了100%。这直接导致了客户访问的响应时间增加。

大约十年前，解决这类问题的方案是为应用程序及数据库采购和部署新的硬件资源，在安装所有必需的软件和应用程序代码，然后进行所有功能和性能的质量分析工作，最后迁移应用程序。这类方案的成本可能达到数百万、数千万资金的开销。然而，如今针对这个问题，客户可以直接借助新技术通过不同的方法来解决——Serverless就是其中之一。

在这里，我们将首先解释无服务器模型，并开始使用通过一些项目上手各大云服务提供商，学习如何构建和运行一些Serverless函数

## Serverless 模型

要理解Serverless模型，首先要理解如何构建传统应用程序，如移动Web应用程序。图1-1显示了一个传统的本地数据中心应用程序架构，你需要处理应用程序开发和部署的每个层级，包括硬件设置、软件安装、数据库、网络、中间件和存储设置。此外，您还需要一个工程师团队来配置和运维这套架构，而这项工作非常耗时，并且成本高昂。此外，这些服务器的生命周期，一般只有5-6年，这意味着最终每隔几年就需要升级一次基础设施。

还远没有结束，因为还必须执行常规的服务器维护，包括设置服务器重启周期和执行常规补丁更新。即使做了所有的这些基础工作，并确保系统正常运行，在实际过程中，系统仍会发生故障，并导致应用宕机。Serverless模型完全改变了这种模式，因为他抽象了所有关于数据中心配置和管理、服务器和软件的复杂性。

Serverless模型是指对最终对用户完全隐藏服务器管理和维护工作的应用程序。在Serverless模型中，开发人员可以专注于业务代码和应用程序本身，他们不需要关心将执行或运行应用程序的服务器，或者关于这些服务器的性能，或者他们的任何限制。Serverless模型是高度可扩展的，并且非常灵活。使用Serverless模型，您可以专注于对你来说更重要的事情，这很可能是去解决业务问题。Serverless模型使用户可以专注于应用程序架构，而无须考虑服务器。

“无服务器”一次可能会令人困惑。Serverless并不意味着根本不需要服务器，而是不需要考虑配置服务器、管理软件和安装补丁等工作。“无服务器”模型意味着采用不需要自己管理的服务器。如果Serverless架构实施得当，可以在降低成本和提供卓越运行方面表现出巨大优势，从而提高整体生产力。但是，在应对Serverless架构所带来的挑战时，你也必须小心，需要确保应用程序不出现性能、资源瓶颈或安全性方面的问题。

Serverless近来已经变得非常流行，许多大型组织已经将其完整的基础设施转移到Serverless架构，并成功运行它们，而且能以更低的成本获得更好的应用性能。目前有许多的Serverless框架设计，是的构建、测试和部署Serverless应用程序变得更加简单。

## Serverless 优势

使用Serverless有诸多好处。

1. 无须管理服务器

配置和管理服务器是一项复杂的任务。在开始使用服务器之前，可能需要几天甚至几个月时间来配置和测试这些服务器。如果在一个特定的时间周期内没能正常完成，他可能成为软件发布到市场的潜在性障碍。Serveless模型可以屏蔽开发团队的所有系统工程工作，为项目提供极大便利

2. 高可用性和容错性

Serverless应用程序具有内置高可用性（HA）的架构，因此，你无需担心这些功能的实现。Serverless 使用区域和可用区的概念来维护服务的高可用性。可用区在区域内是处于相互隔离的位置，你可以通过以下方式来开发应用程序：如果其中一个可用区出现故障，应用程序将继续在另一个可用区内运行。

3. 灵活拓展

我们都希望开发的应用程序能够获得成功，这需要确保在应用程序必须进行拓展之前准备就绪。显然，我们不希望在最开始的时候就是使用规格非常高的服务器（因为这会增加成本，浪费资源），而是希望在我们想要或者需要时才这样做。使用无服务器模型可以非常轻松地拓展应用程序。无服务器模型在你定义的限制下运行美因茨将来你可以轻松突破这些限制，只需要在控制台上单机几下，就可以调整应用程序的计算能力、内存、IO需求等等，并且这可以在几分钟内完成。同时，这也有助于控制成本。

4. 提高开发生产力


在无服务器模型钟，无服务器供应商可以轻松设置硬件、网络以及安装和管理软件。开发人员只需要专注于实现业务逻辑，而不必担心底层的系统工程工作，从而提高开发人员的工作效率。

5. 无空闲容量

使用无服务器模型，无需提前配置计算和存储容量。我们可以根据应用程序的需要进行拓展和收缩。例如，运行一个电子商务网站，那么在节日期间可能需要比其他时候更高的容量。因此，你只需要在特定的某段时间内拓展资源。

此外，如今的无服务器模型可以使用实际使用量付费模式，这意味着你不需要为任何没有使用的，你只需要点击几下即可拓展收缩底层硬件。这会节省很多系统工程工作的时间，并且可以更快的启动应用程序。这是很多公司采用无服务器模型的关键因素之一。

6. 分钟级部署

如今的无服务器模型通过完成所有繁重琐碎的工作并消除任何底层基础设置的管理需求来简化应用程序的部署，这些服务都遵循DevOps最佳实践原则。
