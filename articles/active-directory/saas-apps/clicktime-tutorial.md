---
title: 教程：Azure Active Directory 与 ClickTime 的集成 | Microsoft 文档
description: 了解如何在 Azure Active Directory 和 ClickTime 之间配置单一登录。
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeedes
ms.openlocfilehash: fe8dd3f0771a2692488ddea2000b06d0ed212faf
ms.sourcegitcommit: 16ddc345abd6e10a7a3714f12780958f60d339b6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36216440"
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a>教程：Azure Active Directory 与 ClickTime 的集成

本教程介绍了如何将 ClickTime 与 Azure Active Directory (Azure AD) 进行集成。

将 ClickTime 与 Azure AD 集成可提供以下优势：

- 可以在 Azure AD 中控制谁有权访问 ClickTime
- 可以让用户使用其 Azure AD 帐户自动登录到 ClickTime（单一登录）
- 可以在一个中心位置（即 Azure 门户）管理帐户

如需了解有关 SaaS 应用与 Azure AD 集成的详细信息，请参阅 [Azure Active Directory 的应用程序访问与单一登录是什么](../manage-apps/what-is-single-sign-on.md)。

## <a name="prerequisites"></a>先决条件

若要配置 Azure AD 与 ClickTime 的集成，需要具有以下项：

- Azure AD 订阅
- 启用了 ClickTime 单一登录的订阅

> [!NOTE]
> 为了测试本教程中的步骤，我们不建议使用生产环境。

测试本教程中的步骤应遵循以下建议：

- 除非必要，请勿使用生产环境。
- 如果没有 Azure AD 试用环境，可以[获取一个月的试用版](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>方案描述
在本教程中，将在测试环境中测试 Azure AD 单一登录。 本教程中概述的方案包括两个主要构建基块：

1. 从库中添加 ClickTime
2. 配置和测试 Azure AD 单一登录

## <a name="adding-clicktime-from-the-gallery"></a>从库中添加 ClickTime
要配置 ClickTime 与 Azure AD 的集成，需要从库中将 ClickTime 添加到托管 SaaS 应用列表。

**要从库中添加 ClickTime，请执行以下步骤：**

1. 在 **[Azure 门户](https://portal.azure.com)** 的左侧导航面板中，单击“Azure Active Directory”图标。 

    ![“Azure Active Directory”按钮][1]

2. 导航到“企业应用程序”。 然后转到“所有应用程序”。

    ![“企业应用程序”边栏选项卡][2]
    
3. 若要添加新应用程序，请单击对话框顶部的“新建应用程序”按钮。

    ![“新增应用程序”按钮][3]

4. 在搜索框中，键入“ClickTime”，在结果面板中选择“ClickTime”，然后单击“添加”按钮添加该应用程序。

    ![结果列表中的 ClickTime](./media/clicktime-tutorial/tutorial_clicktime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>配置和测试 Azure AD 单一登录

在本部分中，将基于名为“Britta Simon”的测试用户配置并测试 ClickTime 的 Azure AD 单一登录。

若要运行单一登录，Azure AD 需要知道与 Azure AD 用户相对应的 ClickTime 用户。 换句话说，需要在 Azure AD 用户与 ClickTime 中的相关用户之间建立链接关系。

可通过将 Azure AD 中“用户名”的值指定为 ClickTime 中“用户名”的值，建立此链接关系。

若要配置并测试 ClickTime 的 Azure AD 单一登录，需要完成以下构建基块：

1. **[配置 Azure AD 单一登录](#configure-azure-ad-single-sign-on)** - 使用户能够使用此功能。
2. **[创建 Azure AD 测试用户](#create-an-azure-ad-test-user)** - 使用 Britta Simon 测试 Azure AD 单一登录。
3. **[创建 ClickTime 测试用户](#create-a-clicktime-test-user)** - 在 ClickTime 中创建 Britta Simon 的对应用户，并将其链接到用户的 Azure AD 表示形式。
4. **[分配 Azure AD 测试用户](#assign-the-azure-ad-test-user)** - 使 Britta Simon 能够使用 Azure AD 单一登录。
5. **[测试单一登录](#test-single-sign-on)** - 验证配置是否正常工作。

### <a name="configure-azure-ad-single-sign-on"></a>配置 Azure AD 单一登录

在本部分中，将在 Azure 门户中启用 Azure AD 单一登录并在 ClickTime 应用程序中配置单一登录。

**若要配置 ClickTime 的 Azure AD 单一登录，请执行以下步骤：**

1. 在 Azure 门户中，在 ClickTime 应用程序集成页上，单击“单一登录”。

    ![配置单一登录链接][4]

2. 在“单一登录”对话框中，选择“基于 SAML 的单一登录”作为“模式”以启用单一登录。
 
    ![“单一登录”对话框](./media/clicktime-tutorial/tutorial_clicktime_samlbase.png)

3. 在“ClickTime 域和 URL”部分中，执行以下步骤：

    ![ClickTime 域和 URL 单一登录信息](./media/clicktime-tutorial/tutorial_clicktime_url.png)

    a. 在“标识符”文本框中，键入 URL：`https://app.clicktime.com/sp/`
    
    b. 在“回复 URL”文本框中，使用以下模式键入 URL： 

    | |
    |--|
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |

4. 在“SAML 签名证书”部分中，单击“证书(base64)”，并在计算机上保存证书文件。

    ![证书下载链接](./media/clicktime-tutorial/tutorial_clicktime_certificate.png) 

5. 单击“保存”按钮。

    ![配置单一登录“保存”按钮](./media/clicktime-tutorial/tutorial_general_400.png)

6. 在“ClickTime 配置”部分中，单击“配置 ClickTime”打开“配置登录”窗口。 从“快速参考”部分中复制“SAML 单一登录服务 URL”

    ![ClickTime 配置](./media/clicktime-tutorial/tutorial_clicktime_configure.png) 

7. 在另一个 Web 浏览器窗口中，以管理员身份登录到 ClickTime 公司站点。

8. 在顶部工具栏中，单击“首选项”，并单击“安全设置”。

9. 在“单一登录首选项”配置部分中，执行以下步骤：
   
    ![安全设置](./media/clicktime-tutorial/tic777280.png "安全设置")
   
    a.  选择“允许”通过“Azure AD”使用单一登录 (SSO) 进行登录。
   
    b. 在“标识提供者终结点”文本框中，粘贴从 Azure 门户复制的“SAML 单一登录服务 URL”。
   
    c.  在记事本中打开从 Azure 门户下载的 base-64 编码证书，复制内容，然后将其粘贴到“X.509 证书”文本框中。
   
    d.  单击“ **保存**”。

> [!TIP]
> 之后在设置应用时，就可以在 [Azure 门户](https://portal.azure.com)中阅读这些说明的简明版本了！  从“Active Directory”>“企业应用程序”部分添加此应用后，只需单击“单一登录”选项卡，即可通过底部的“配置”部分访问嵌入式文档。 可在此处阅读有关嵌入式文档功能的详细信息：[ Azure AD 嵌入式文档]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>创建 Azure AD 测试用户
本部分的目的是在 Azure 门户中创建名为 Britta Simon 的测试用户。

![创建 Azure AD 测试用户][100]

**若要在 Azure AD 中创建测试用户，请执行以下步骤：**

1. 在 Azure 门户的左窗格中，单击“Azure Active Directory”按钮。

    ![“Azure Active Directory”按钮](./media/clicktime-tutorial/create_aaduser_01.png) 

2. 若要显示用户列表，请转到“用户和组”，然后单击“所有用户”。
    
    ![“用户和组”以及“所有用户”链接](./media/clicktime-tutorial/create_aaduser_02.png) 

3. 若要打开“用户”对话框，在“所有用户”对话框顶部单击“添加”。
 
    ![“添加”按钮](./media/clicktime-tutorial/create_aaduser_03.png) 

4. 在“用户”对话框中，执行以下步骤：
 
    ![“用户”对话框](./media/clicktime-tutorial/create_aaduser_04.png) 

    a. 在“名称”文本框中，键入 **BrittaSimon**。

    b. 在“用户名”文本框中，键入 BrittaSimon 的“电子邮件地址”。

    c. 选择“显示密码”并记下“密码”的值。

    d. 单击“创建”。
 
### <a name="create-a-clicktime-test-user"></a>创建 ClickTime 测试用户

为了使 Azure AD 用户能够登录到 ClickTime，必须将其预配到 ClickTime 中。  
对于 ClickTime，需要手动执行预配。

> [!NOTE]
> 可以使用 ClickTime 提供的任何其他 ClickTime 用户帐户创建工具或 API 来预配 Azure AD 用户帐户。

**若要预配用户帐户，请执行以下步骤：**
1. 登录到 **ClickTime** 租户。
2. 在顶部工具栏中，单击“公司”，并单击“人员”。
   
    ![人员](./media/clicktime-tutorial/tic777282.png "人员")
3. 单击“添加用户”。
   
    ![添加人员](./media/clicktime-tutorial/tic777283.png "添加人员")
4. 在“新建人员”部分中，执行以下步骤：
   
    ![人员](./media/clicktime-tutorial/tic777284.png "人员")
   
    a.  在“全名”文本框中，键入用户的全名，例如 Britta Simon。 
  
    b.  在“电子邮件地址”文本框中，键入用户的电子邮件，例如 brittasimon@contoso.com。
       
    > [!NOTE]
    > 如果需要，可以设置新人员对象的其他属性。
   
    c.  单击“ **保存**”。

### <a name="assign-the-azure-ad-test-user"></a>分配 Azure AD 测试用户

在本部分中，将通过向 Britta Simon 授予 ClickTime 的访问权限使之能够使用 Azure 单一登录。

![分配用户角色][200] 

**要将 Britta Simon 分配到 ClickTime，请执行以下步骤：**

1. 在 Azure 门户中打开应用程序视图，导航到目录视图，接着转到“企业应用程序”，并单击“所有应用程序”。

    ![分配用户][201] 

2. 在应用程序列表中，选择“ClickTime”。

    ![应用程序列表中的 ClickTime 链接](./media/clicktime-tutorial/tutorial_clicktime_app.png) 

3. 在左侧菜单中，单击“用户和组”。

    ![“用户和组”链接][202] 

4. 单击“添加”按钮。 然后在“添加分配”对话框中选择“用户和组”。

    ![“添加分配”窗格][203]

5. 在“用户和组”对话框的“用户”列表中，选择“Britta Simon”。

6. 在“用户和组”对话框中单击“选择”按钮。

7. 在“添加分配”对话框中单击“分配”按钮。
    
### <a name="test-single-sign-on"></a>测试单一登录

在本部分中，使用访问面板测试 Azure AD 单一登录配置。

当在访问面板中单击 ClickTime 磁贴时，应当会自动登录到 ClickTime 应用程序。
有关访问面板的详细信息，请参阅 [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md)（访问面板简介）。

## <a name="additional-resources"></a>其他资源

* [有关如何将 SaaS 应用与 Azure Active Directory 集成的教程列表](tutorial-list.md)
* [什么是使用 Azure Active Directory 的应用程序访问和单一登录？](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/clicktime-tutorial/tutorial_general_01.png
[2]: ./media/clicktime-tutorial/tutorial_general_02.png
[3]: ./media/clicktime-tutorial/tutorial_general_03.png
[4]: ./media/clicktime-tutorial/tutorial_general_04.png

[100]: ./media/clicktime-tutorial/tutorial_general_100.png

[200]: ./media/clicktime-tutorial/tutorial_general_200.png
[201]: ./media/clicktime-tutorial/tutorial_general_201.png
[202]: ./media/clicktime-tutorial/tutorial_general_202.png
[203]: ./media/clicktime-tutorial/tutorial_general_203.png

