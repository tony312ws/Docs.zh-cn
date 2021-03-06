---
uid: web-api/overview/releases/whats-new-in-aspnet-web-api-22
title: 什么是 ASP.NET Web API 2.2 中的新增功能 |Microsoft Docs
author: microsoft
description: ''
ms.author: riande
ms.date: 12/25/2014
ms.assetid: 99c59ae4-167e-4f66-a6cd-d3f1098c4e4a
msc.legacyurl: /web-api/overview/releases/whats-new-in-aspnet-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: ef08a3bb397ff54795ca6c70cdcc35206cf122f5
ms.sourcegitcommit: 45ac74e400f9f2b7dbded66297730f6f14a4eb25
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "41825074"
---
<a name="whats-new-in-aspnet-web-api-22"></a>什么是 ASP.NET Web API 2.2 中的新增功能
====================
by [Microsoft](https://github.com/microsoft)

本主题介绍什么是 ASP.NET Web API 2.2 的新增功能。

- [下载](#download)
- [文档](#documentation)
- [ASP.NET Web API 2.2 中的新增功能](#newf)

    - [OData v4](#OData)
    - [属性路由改进](#ARI)
    - [Web API 客户端支持 Windows Phone 8.1](#phone)
- [已知的问题和重大更改](#known-issues)
- [Bug 修复](#bug-fixes)
- [Microsoft.AspNet.OData 5.2.1 章](#odata521)
- [Microsoft.AspNet.WebAPI 5.2.2](#522RC)
- [Microsoft.AspNet.WebAPI 5.2.3 Beta](#523)

<a id="download"></a>
## <a name="download"></a>下载

运行时功能将发布为 NuGet 库中的 NuGet 包。 所有运行时程序包遵循[语义化版本控制](http://semver.org/)规范。 最新的 ASP.NET Web API 2.2 包具有以下版本:"5.2.0"。 可以安装或更新通过这些程序包[NuGet](http://www.nuget.org/packages/Microsoft.AspNet.WebApi/)。 此版本还包括在 NuGet 上的相应本地化的包。

可以安装或使用 NuGet 包管理器控制台更新为已发布的 NuGet 包：

[!code-console[Main](whats-new-in-aspnet-web-api-22/samples/sample1.cmd)]

<a id="documentation"></a>
## <a name="documentation"></a>文档

教程和有关 ASP.NET Web API 2.2 的其他信息是可通过 ASP.NET 网站 ([https://www.asp.net/web-api](../../index.md))。

<a id="newf"></a>
## <a name="new-features-in-aspnet-web-api-22"></a>ASP.NET Web API 2.2 中的新增功能

<a id="OData"></a>
### <a name="odata-v4"></a>OData v4

此版本添加了对 OData v4 协议的支持。 有关详细信息，请参阅[Web API OData v4 文档。](../odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint.md)

下面是一些主要功能和更改的 OData v4:

- [支持的 OData 模型中的别名属性](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataModelAliasingSample/)
- [支持 ComplexTypeAttribute、 AssociationAttribute、 TimesTampAttribute 和 ConcurrencyCheckAttribute ODataConventionModelBuilder 中](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataEtagSample/)
- [提供功能来提供友好标题的操作](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataActionsSample/)
- 将与 ODL UriParser 集成
- 为支持[enum](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataEnumTypeSample/ODataEnumTypeSample/)，[包容](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataContainmentSample/)和[单一实例](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataSingletonSample/)
- 强制转换为基元类型的支持
- [添加了的 OData 函数的支持](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataFunctionSample/)
- [支持的函数调用的参数的别名](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataFunctionSample/)
- [在模型中支持 camel 大小写的命名约定](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataCamelCaseSample/)
- 在 $ $filter 中的 cast （） 的支持
- 对打开的复杂类型的支持
- 已删除的 EntitySetController 和 AsyncEntitySetController
- [已更改为 $ref $link](http://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataServiceSample/)
- [添加了的属性路由支持](https://aspnet.codeplex.com/SourceControl/latest#Samples/WebApi/OData/v4/ODataAttributeRoutingSample/)
- 使用 OData 核心库 6.4.0

<a id="ARI"></a>
### <a name="attribute-routing-improvements"></a>属性路由改进

属性路由现在提供了一个名为 IDirectRouteProvider，可完全控制如何发现和配置属性路由的扩展点。 IDirectRouteProvider 负责提供的操作和控制器以及关联的路由信息来指定这些操作需要何种路由配置的情况完全列表。 调用 MapAttributes/MapHttpAttributeRoutes 时，可能会指定 IDirectRouteProvider 实现。

自定义 IDirectRouteProvider 将是最简单通过扩展我们的默认实现，DefaultDirectRouteProvider。 此类提供了单独可重写虚拟方法，以更改用于发现属性、 创建路由项，以及发现路由前缀和区域前缀的逻辑。

以下是有关使用此新的扩展点可以做些什么的一些示例：

1. 支持路由属性的继承

    示例:

    此处 like"/ api/值/10"的请求已成功将返回"成功： 10"

    [!code-csharp[Main](whats-new-in-aspnet-web-api-22/samples/sample2.cs)]
2. 按照您喜欢某些约定提供属性路由的默认路由名称。 默认情况下，属性路由不会自动创建属性路由的名称。
3. 修改属性路由的路由模板在一个中心位置，然后最终路由表中。

<a id="phone"></a>
### <a name="web-api-client-support-for-windows-phone-81"></a>Windows Phone 8.1 的 web API 客户端支持

现在可以使用 Web API 客户端 NuGet 包以实现 Web API 客户端逻辑，面向 Windows Phone 8.1 时或从通用应用中。

<a id="known-issues"></a>
## <a name="known-issues-and-breaking-changes"></a>已知的问题和重大更改

本部分介绍的已知的问题和 ASP.NET Web API 2.2 中的重大更改。

### <a name="odata-v4"></a>OData v4

#### <a name="model-builder"></a>模型生成器

问题： 重载的函数可能不会公开为 FunctionImport

如果有两个重载的函数，也要 FunctionImport 然后请求中 System.InvalidOperationException ~/GetAllConventionCustomers(CustomerName={customerName}) 结果如下所示。

[!code-xml[Main](whats-new-in-aspnet-web-api-22/samples/sample3.xml)]

解决方法： 此问题的解决方法是将这两个函数重载添加 FunctionImports 为。

#### <a name="odata-routing"></a>OData 路由

包含 URL 的字符串文本编码斜杠 (%2f) 和 backslash(%5C) OData 资源路径中使用它们时，会导致 404 错误。

例如，字符串文本可以用作 OData 资源路径中的函数的参数或实体集的键值。

/Employees/Total.GetCount(Name='Name%2F')

/Employees('Name%5C')

当服务收到此类请求的主机将取消转义时那些转义序列，然后再将它们传递到 Web API 运行时。 这可防止攻击，如下所示：  
  
`http://www.contoso.com/..%2F..%2F/Windows/System32/cmd.exe?/c+dir+c:`

这会导致要返回 404 错误 （找不到） 的 Web API OData 堆栈。 若要防止出现此错误，您的客户端应使用双转义序列的反斜杠 （%252f) 和反斜杠 （%255 C)。 这不会针对查询字符串，如 /Employees？ $filter = 名称 eq '名称 %2f

**请注意取消转义的斜杠 （'/') 和反斜杠 （"） 不能使用 OData 资源路径的字符串文字。应只作为路径分隔符出现斜杠和反斜杠不应出现在 OData 资源路径根本。（均可在 OData 查询字符串的某些部分中使用。）**

解决方法： 您可以重写 DefaultODataPathHandler 进行实际解析它们之前转义的反斜杠和字符串文本中的反斜杠的分析方法。 您可以找到这种方法的示例。

### <a name="odata-v3"></a>OData v3

#### <a name="queryable"></a>[查询]

不推荐使用 [Queryable] 属性。 新的 OData v3 应用程序应使用**System.Web.Http.OData.EnableQueryAttribute**。

**ODataHttpConfigurationExtensions.EnableQuerySupport**扩展方法现在将添加**EnableQueryAttribute**到全局筛选器集合。 如果有任何控制器 **[Queryable]** 属性，则调用`config.EnableQuerySupport()`将导致 **[Queryable]** 属性失败

若要解决此问题的建议的方法是替换的所有实例**QueryableAttribute**与**System.Web.Http.OData.EnableQueryAttribute**。

备用解决方法是在 Web API 配置中使用以下代码：

[!code-csharp[Main](whats-new-in-aspnet-web-api-22/samples/sample4.cs)]

### <a name="attribute-routing"></a>属性路由

问题： 修饰 FromUri 属性的复杂类型的模型绑定时的行为以不同的方式使用属性路由。

以下链接跟踪此问题，还有一种解决方法有关的详细信息。  
[http://aspnetwebstack.codeplex.com/workitem/1944](http://aspnetwebstack.codeplex.com/workitem/1944)

问题： 基架 MVC/Web API 到具有 5.2.0 项目包导致 5.1.2 打包以一种是在项目中尚不存在

有关 ASP.NET MVC 5.2 更新 NuGet 包不会更新 Visual Studio 工具，如 ASP.NET 基架或 ASP.NET Web 应用程序项目模板。 它们使用以前版本的 ASP.NET 运行时包 (例如 5.1.2 Update 2 中)。 因此，ASP.NET 基架将安装以前版本 (例如 5.1.2 Update 2 中) 的所需的包，如果它们尚不在你项目中可用。 但是，在 Visual Studio 2013 RTM 或 Update 1 中的 ASP.NET 基架不会覆盖在项目中最新的包。 如果您使用 ASP.NET 基架 Web API 2.2 或 ASP.NET MVC 5.2 更新你的项目的包后，请确保了一致的 Web API 和 ASP.NET MVC 版本。

<a id="bug-fixes"></a>
## <a name="bug-fixes-and-minor-feature-updates"></a>Bug 修复和细微的功能更新

此版本还包括几个 bug 修复和细微的功能更新。 您可以找到完整的列表：

- [5.2 包](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=v5.2%20RC|v5.2%20RTM&assignedTo=All&component=Web%20API|Web%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="odata521"></a>
## <a name="microsoftaspnetodata-521"></a>Microsoft.AspNet.OData 5.2.1 章

Microsoft.AspNet.OData 5.2.1 章包中包含 NuGet 依赖项更新，但任何 bug 修复。 利用此更新，不再严格的依赖项上 Microsoft.OData.Core 6.4.0，但其中一个可以升级到 6.4.0 和 7.0.0 之间的任何版本。

<a id="522RC"></a>
## <a name="microsoftaspnetwebapi-522"></a>Microsoft.AspNet.WebAPI 5.2.2

在此版本中我们所做的更改的依赖关系`Json.Net 6.0.4`。 有关详细信息的此版本中新增`Json.NET`，请参阅[Json.NET 6.0 第 4 版-JSON 合并、 依赖关系注入](http://james.newtonking.com/archive/2014/08/04/json-net-6-0-release-4-json-merge-dependency-injection)。 此版本不包含任何其他新功能或 bug 修复，Web API 中。 我们随后更新了我们拥有依赖于此新版本的 Web API 的所有依赖包。

<a id="523"></a>
## <a name="microsoftaspnetwebapi-523-beta"></a>Microsoft.AspNet.WebAPI 5.2.3 Beta

你可以阅读发行[此处](https://blogs.msdn.com/b/webdev/archive/2014/12/17/asp-net-mvc-5-2-3-web-pages-5-2-3-and-web-api-5-2-3-beta-releases.aspx)。 此版本包含仅 bug 修复。 可以使用[此查询](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&amp;status=Closed&amp;type=All&amp;priority=All&amp;release=v5.2.3%20Beta&amp;assignedTo=All&amp;component=Web%20API&amp;sortField=LastUpdatedDate&amp;sortDirection=Descending&amp;page=0&amp;reasonClosed=Fixed)若要查看此版本中修复的问题的列表。
