---
title: 教程：Azure Active Directory 与 Replicon 集成 | Microsoft Docs
description: 了解如何在 Azure Active Directory 与 Replicon 之间配置单一登录。
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2018
ms.author: jeedes
ms.openlocfilehash: 70a67f5205ee9b1249d3db2cda3eb4af9acabe31
ms.sourcegitcommit: 16ddc345abd6e10a7a3714f12780958f60d339b6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36230166"
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a>教程：Azure Active Directory 与 Replicon 集成

在本教程中，了解如何将 Replicon 与 Azure Active Directory (Azure AD) 集成。

将 Replicon 与 Azure AD 集成提供以下优势：

- 可在 Azure AD 中控制谁有权访问 Replicon。
- 可以让用户使用其 Azure AD 帐户自动登录到 Replicon（单一登录）。
- 可在中心位置（即 Azure 门户）管理帐户。

如需了解有关 SaaS 应用与 Azure AD 集成的详细信息，请参阅 [Azure Active Directory 的应用程序访问与单一登录是什么](../manage-apps/what-is-single-sign-on.md)。

## <a name="prerequisites"></a>先决条件

若要配置 Azure AD 与 Replicon 的集成，需要以下项：

- Azure AD 订阅
- 启用了 Replicon 单一登录的订阅

> [!NOTE]
> 为了测试本教程中的步骤，我们不建议使用生产环境。

测试本教程中的步骤应遵循以下建议：

- 除非必要，请勿使用生产环境。
- 如果没有 Azure AD 试用环境，可以[获取一个月的试用版](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="scenario-description"></a>方案描述
在本教程中，将在测试环境中测试 Azure AD 单一登录。 本教程中概述的方案包括两个主要构建基块：

1. 从库中添加 Replicon
2. 配置和测试 Azure AD 单一登录

## <a name="adding-replicon-from-the-gallery"></a>从库中添加 Replicon
要配置 Replicon 与 Azure AD 的集成，需要从库中将 Replicon 添加到托管 SaaS 应用列表。

**若要从库中添加 Replicon，请执行以下步骤：**

1. 在 **[Azure 门户](https://portal.azure.com)** 的左侧导航面板中，单击“Azure Active Directory”图标。

    ![“Azure Active Directory”按钮][1]

2. 导航到“企业应用程序”。 然后转到“所有应用程序”。

    ![“企业应用程序”边栏选项卡][2]

3. 若要添加新应用程序，请单击对话框顶部的“新建应用程序”按钮。

    ![“新增应用程序”按钮][3]

4. 在搜索框中，键入“Replicon”，在结果面板中选择“Replicon”，然后单击“添加”按钮添加该应用程序。

    ![结果列表中的 Replicon](./media/replicon-tutorial/tutorial_replicon_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>配置和测试 Azure AD 单一登录

在本部分中，将基于名为“Britta Simon”的测试用户配置和测试 Replicon 的 Azure AD 单一登录。

若要运行单一登录，Azure AD 需要知道与 Azure AD 用户相对应的 Replicon 用户。 换句话说，需要建立 Azure AD 用户与 Replicon 中相关用户之间的链接关系。

通过将 Azure AD 中“用户名”的值指定为 Replicon 中“用户名”的值来建立此链接关系。

若要配置和测试 Replicon 的 Azure AD 单一登录，需要完成以下构建基块：

1. **[配置 Azure AD 单一登录](#configure-azure-ad-single-sign-on)** - 使用户能够使用此功能。
2. **[创建 Azure AD 测试用户](#create-an-azure-ad-test-user)** - 使用 Britta Simon 测试 Azure AD 单一登录。
3. **[创建 Replicon 测试用户](#create-a-replicon-test-user)** - 在 Replicon 中创建 Britta Simon 的对应用户，并将其链接到该用户的 Azure AD 表示形式。
4. **[分配 Azure AD 测试用户](#assign-the-azure-ad-test-user)** - 使 Britta Simon 能够使用 Azure AD 单一登录。
5. **[测试单一登录](#test-single-sign-on)** - 验证配置是否正常工作。

### <a name="configure-azure-ad-single-sign-on"></a>配置 Azure AD 单一登录

在本部分中，将在 Azure 门户中启用 Azure AD 单一登录并在 Replicon 应用程序中配置单一登录。

**若要配置 Replicon 的 Azure AD 单一登录，请执行以下步骤：**

1. 在 Azure 门户中，在 **Replicon** 应用程序集成页上，单击“单一登录”。

    ![配置单一登录链接][4]

2. 在“单一登录”对话框中，选择“基于 SAML 的单一登录”作为“模式”以启用单一登录。

    ![“单一登录”对话框](./media/replicon-tutorial/tutorial_replicon_samlbase.png)

3. 在“Replicon 域和 URL”部分中，执行以下步骤：

    ![Replicon 域和 URL 单一登录信息](./media/replicon-tutorial/tutorial_replicon_url.png)

    a. 在“登录 URL”文本框中，使用以下模式键入 URL：`https://na2.replicon.com/<companyname>/saml2/sp-sso/post`

    b. 在“标识符”文本框中，使用以下模式键入 URL：`https://global.replicon.com/<companyname>`

    c. 在“回复 URL”文本框中，使用以下模式键入 URL：`https://global.replicon.com/!/saml2/<companyname>/sso/post`

    > [!NOTE]
    > 这些不是实际值。 请使用实际登录 URL、标识符和回复 URL 更新这些值。 请联系 [Replicon 客户端支持团队](https://www.replicon.com/customerzone/contact-support)获取这些值。 

4. 在“SAML 签名证书”部分中，单击“元数据 XML”，并在计算机上保存元数据文件。

    ![证书下载链接](./media/replicon-tutorial/tutorial_replicon_certificate.png) 

5. 单击“保存”按钮。

    ![配置单一登录“保存”按钮](./media/replicon-tutorial/tutorial_general_400.png)

6. 在另一个 Web 浏览器窗口中，以管理员身份登录 Replicon 公司站点。

7. 若要配置 SAML 2.0，请执行以下步骤：

    ![启用 SAML 身份验证](./media/replicon-tutorial/ic777805.png "启用 SAML 身份验证")

    a. 要显示 **EnableSAML Authentication2** 对话框，请将以下内容追加到 URL 中的公司密钥后面：`/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2`

    * 下面显示完整 URL 的架构：`https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2`

   b. 单击 **+** 展开 **v20Configuration** 部分。

   c. 单击 **+** 展开 **metaDataConfiguration** 部分。

   d. 单击“选择文件”，选择标识提供者元数据 XML 文件，并单击“提交”。

### <a name="create-an-azure-ad-test-user"></a>创建 Azure AD 测试用户

本部分的目的是在 Azure 门户中创建名为 Britta Simon 的测试用户。

   ![创建 Azure AD 测试用户][100]

**若要在 Azure AD 中创建测试用户，请执行以下步骤：**

1. 在 Azure 门户的左窗格中，单击“Azure Active Directory”按钮。

    ![“Azure Active Directory”按钮](./media/replicon-tutorial/create_aaduser_01.png)

2. 若要显示用户列表，请转到“用户和组”，然后单击“所有用户”。

    ![“用户和组”以及“所有用户”链接](./media/replicon-tutorial/create_aaduser_02.png)

3. 若要打开“用户”对话框，在“所有用户”对话框顶部单击“添加”。

    ![“添加”按钮](./media/replicon-tutorial/create_aaduser_03.png)

4. 在“用户”对话框中，执行以下步骤：

    ![“用户”对话框](./media/replicon-tutorial/create_aaduser_04.png)

    a. 在“姓名”框中，键入“BrittaSimon”。

    b. 在“用户名”框中，键入用户 Britta Simon 的电子邮件地址。

    c. 选中“显示密码”复选框，然后记下“密码”框中显示的值。

    d. 单击“创建”。

### <a name="create-a-replicon-test-user"></a>创建一个 Replicon 测试用户

本部分的目的是在 Replicon 中创建名为“Britta Simon”的用户。 Replicon 支持在默认情况下启用的自动用户预配。 有关如何配置自动用户预配的更多详细信息，请参见[此处](replicon-provisioning-tutorial.md)。

如果需要手动创建用户，请执行以下步骤：

1. 在 Web 浏览器窗口中，以管理员身份登录 Replicon 公司站点。

2. 转到“管理”\>“用户”。

    ![用户](./media/replicon-tutorial/ic777806.png "用户")

3. 单击“+添加用户”。

    ![添加用户](./media/replicon-tutorial/ic777807.png "添加用户")

4. 在“用户配置文件”部分中，执行以下步骤：

    ![用户配置文件](./media/replicon-tutorial/ic777808.png "用户配置文件")

    a. 在“登录名”文本框中，键入要预配的 Azure AD 用户的 Azure AD 电子邮件地址，如 **BrittaSimon@contoso.com**。

    b. 对于“身份验证类型”，选择“SSO”。

    c. 在“部门”文本框中，键入用户的部门。

    d. 对于“员工类型”，选择“管理员”。

    e. 单击“保存用户配置文件”。

>[!NOTE]
>可以使用任何其他 Replicon 用户帐户创建工具或 Replicon 提供的 API 来预配 Azure AD 用户帐户。

### <a name="assign-the-azure-ad-test-user"></a>分配 Azure AD 测试用户

在本部分中，通过授予 Britta Simon 访问 Replicon 的权限，允许她使用 Azure 单一登录。

![分配用户角色][200]

**若要将 Britta Simon 分配到 Replicon，请执行以下步骤：**

1. 在 Azure 门户中打开应用程序视图，导航到目录视图，接着转到“企业应用程序”，并单击“所有应用程序”。

    ![分配用户][201]

2. 在应用程序列表中，选择“Replicon”。

    ![应用程序列表中的 Replicon 链接](./media/replicon-tutorial/tutorial_replicon_app.png)

3. 在左侧菜单中，单击“用户和组”。

    ![“用户和组”链接][202]

4. 单击“添加”按钮。 然后在“添加分配”对话框中选择“用户和组”。

    ![“添加分配”窗格][203]

5. 在“用户和组”对话框的“用户”列表中，选择“Britta Simon”。

6. 在“用户和组”对话框中单击“选择”按钮。

7. 在“添加分配”对话框中单击“分配”按钮。

### <a name="test-single-sign-on"></a>测试单一登录

在本部分中，使用访问面板测试 Azure AD 单一登录配置。

当在访问面板中单击 Replicon 磁贴时，应当会自动登录到 Replicon 应用程序。
有关访问面板的详细信息，请参阅 [Introduction to the Access Panel](../active-directory-saas-access-panel-introduction.md)（访问面板简介）。

## <a name="additional-resources"></a>其他资源

* [有关如何将 SaaS 应用与 Azure Active Directory 集成的教程列表](tutorial-list.md)
* [什么是使用 Azure Active Directory 的应用程序访问和单一登录？](../manage-apps/what-is-single-sign-on.md)
* [配置用户预配](replicon-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/replicon-tutorial/tutorial_general_01.png
[2]: ./media/replicon-tutorial/tutorial_general_02.png
[3]: ./media/replicon-tutorial/tutorial_general_03.png
[4]: ./media/replicon-tutorial/tutorial_general_04.png

[100]: ./media/replicon-tutorial/tutorial_general_100.png

[200]: ./media/replicon-tutorial/tutorial_general_200.png
[201]: ./media/replicon-tutorial/tutorial_general_201.png
[202]: ./media/replicon-tutorial/tutorial_general_202.png
[203]: ./media/replicon-tutorial/tutorial_general_203.png
