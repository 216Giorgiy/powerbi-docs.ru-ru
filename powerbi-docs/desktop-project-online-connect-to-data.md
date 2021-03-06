---
title: 'Project Online: подключение к данным через Power BI Desktop'
description: 'Project Online: подключение к данным через Power BI Desktop'
author: davidiseminger
manager: kfile
ms.reviewer: ''
ms.custom: seodec18
ms.service: powerbi
ms.subservice: powerbi-desktop
ms.topic: conceptual
ms.date: 12/06/2018
ms.author: davidi
LocalizationGroup: Connect to data
ms.openlocfilehash: a1f55d09de68d5ac29b81c72f3b1dc6cf98c1597
ms.sourcegitcommit: c8c126c1b2ab4527a16a4fb8f5208e0f7fa5ff5a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/15/2019
ms.locfileid: "54289953"
---
# <a name="project-online-connect-to-data-through-power-bi-desktop"></a>Project Online: подключение к данным через Power BI Desktop
К данным в Project Online можно подключиться с помощью Power BI Desktop.

## <a name="step-1-download-power-bi-desktop"></a>Шаг 1. Скачивание Power BI Desktop
1. [Скачайте Power BI Desktop](http://go.microsoft.com/fwlink/?LinkID=521662) и запустите программу установки, чтобы установить **Power BI Desktop** на свой компьютер.

## <a name="step-2-connect-to-project-online-with-odata"></a>Шаг 2. Подключение к Project Online с помощью OData
1. Откройте **Power BI Desktop**.
2. На *экране приветствия* выберите **Получить данные**.
3. Выберите **канал OData** и щелкните **Подключить**.
4. Введите адрес для канала OData в поле URL-адреса и нажмите кнопку ОК.
   
   Если адрес сайта вашего веб-приложения Project имеет формат https://\<имя_клиента\>.sharepoint.com/sites/pwa, адрес канала для OData должен иметь быть в формате https://\<имя_клиента\>.sharepoint.com/sites/pwa/\_api/Projectdata.
   
   В нашем примере используется https://contoso.sharepoint.com/sites/pwa/default.aspx
5. Power BI Desktop предложит вам пройти проверку подлинности учетной записи Office 365. Выберите учетную запись организации и введите свои учетные данные.
   
   ![](media/desktop-project-online-connect-to-data/image.png)

Обратите внимание, что учетная запись, используемая для подключения к веб-каналу OData, должна иметь на сайте Project Web App уровень доступа не ниже Portfolio Viewer (просмотр портфеля проектов). 

Здесь можно выбрать таблицы, к которым нужно подключиться, и создать запрос.  Хотите узнать, как приступить к работе?  В следующей записи блога показано, как создавать диаграммы сгорания на основе данных Project Online.  В записи блога для подключения к Project Online используется Power Query, но то же самое относится и к Power BI Desktop.

[Создание диаграмм сгорания для проектов с помощью Power Pivot и Power Query](http://blogs.office.com/2014/03/24/creating-burndown-charts-for-project-using-power-pivot-and-power-query/)

