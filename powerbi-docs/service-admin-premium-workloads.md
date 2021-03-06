---
title: Настройка рабочих нагрузок в Power BI Premium
description: Сведения о настройке рабочих нагрузок в емкости Power BI Premium.
author: minewiskan
ms.author: owend
manager: kfile
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-admin
ms.topic: conceptual
ms.date: 04/01/2019
LocalizationGroup: Premium
ms.openlocfilehash: fbff4b744cf4a35f2fe1d0ae46f4676cd5f1db77
ms.sourcegitcommit: 8525b6365f3e224176730f4b8e5dae83f540a4ff
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/01/2019
ms.locfileid: "58795252"
---
# <a name="configure-workloads-in-a-premium-capacity"></a>Настройка рабочих нагрузок в емкости Premium

Эта статья описывает включение и настройку рабочих нагрузок для емкостей Power BI Premium. По умолчанию емкости поддерживают только рабочие нагрузки, связанные с выполнением запросов Power BI. Вы можете включить и настроить дополнительные рабочие нагрузки для **[искусственного интеллекта (Cognitive Services)](service-cognitive-services.md)**, **[потоков данных](service-dataflows-overview.md#dataflow-capabilities-on-power-bi-premium)** и **[отчетов с разбивкой на страницы](paginated-reports-save-to-power-bi-service.md)**.

## <a name="default-memory-settings"></a>Параметры памяти по умолчанию

Рабочие нагрузки запросов оптимизированы для ресурсов, определенных SKU емкости Premium, и ограничены ими. Емкости Premium также поддерживают дополнительные рабочие нагрузки, способные использовать ресурсы емкости. Значения памяти по умолчанию для этих рабочих нагрузок основаны на узлах емкости, доступных для вашего номера SKU. Параметры максимального объема памяти не являются накопительными. Объем памяти до максимального указанного значения выделяется динамически для искусственного интеллекта и потоков данных, но статически для отчетов с разбивкой на страницы. 

### <a name="microsoft-office-skus-for-software-as-a-service-saas-scenarios"></a>Номера SKU Microsoft Office для сценариев SaaS (программное обеспечение как услуга)

|                     | EM2                      | EM3                       | P1                      | P2                       | P3                       |
|---------------------|--------------------------|--------------------------|-------------------------|--------------------------|--------------------------|
| Искусственный интеллект (Cognitive Services) | По умолчанию 20 %; минимум подлежит уточнению| По умолчанию 20 %; минимум подлежит уточнению | По умолчанию 20 %; минимум подлежит уточнению | По умолчанию 20 %; минимум подлежит уточнению | По умолчанию 20 %; минимум подлежит уточнению |
| Потоки данных | Н/Д |По умолчанию 20 %; не менее 12 %  | По умолчанию 20 %; не менее 5 %  | По умолчанию 20 %; не менее 3 % | По умолчанию 20 %; не менее 2 %  |
| Отчеты с разбивкой на страницы | Н/Д |Н/Д | По умолчанию 20 %; не менее 10 % | По умолчанию 20 %; не менее 5 % | По умолчанию 20 %; не менее 2,5 % |
| | | | | | |

### <a name="microsoft-azure-skus-for-platform-as-a-service-paas-scenarios"></a>Номера SKU Microsoft Azure для сценариев PaaS (платформа как услуга)

|                  | A1                       | A2                       | A3                      | A4                       | A5                      | A6                        |
|-------------------|--------------------------|--------------------------|-------------------------|--------------------------|-------------------------|---------------------------|
| Искусственный интеллект (Cognitive Services) | Н/Д                      | По умолчанию 20 %; минимум подлежит уточнению                      | По умолчанию 20 %; минимум подлежит уточнению                     | По умолчанию 20 %; минимум подлежит уточнению | По умолчанию 20 %; минимум подлежит уточнению | По умолчанию 20 %; минимум подлежит уточнению |
| Потоки данных         | По умолчанию 40 %; не менее 40 % | По умолчанию 24 %; не менее 24 % | По умолчанию 20 %; не менее 12 % | По умолчанию 20 %; не менее 5 %  | По умолчанию 20 %; не менее 3 % | По умолчанию 20 %; не менее 2 %   |
| Отчеты с разбивкой на страницы | Н/Д                      | Н/Д                      | Н/Д                     | По умолчанию 20 %; не менее 10 % | По умолчанию 20 %; не менее 5 % | По умолчанию 20 %; не менее 2,5 % |
| | | | | | |

## <a name="configure-workloads"></a>Настройка рабочих нагрузок

Вы можете максимально увеличить емкость доступных ресурсов, включая рабочие нагрузки, только если они будут использоваться. Изменяйте параметры, только если параметры по умолчанию не соответствуют требованиям к ресурса емкости.  

### <a name="to-configure-workloads-in-the-power-bi-admin-portal"></a>Настройка рабочих нагрузок на портале администрирования Power BI

1. Выберите емкость в разделе **Параметры емкости** > **Емкости Premium**.

1. В разделе **Дополнительно** разверните **Рабочие нагрузки**.

1. Включите одну или несколько рабочих нагрузок и задайте значение для параметра **Максимальный объем памяти**.   

    
    ![Включение рабочих нагрузок](media/service-admin-premium-workloads/admin-portal-workloads.png)

1. Щелкните **Применить**.

> [!NOTE]
> При включении рабочей нагрузки отчетов с разбивкой на страницы учитывайте, что они позволяют запускать собственный код для отрисовки отчета (например, динамически изменять цвет текста в зависимости от содержимого). Power BI Premium выполняет отчеты с разбивкой на страницы в автономной области в пределах емкости. Максимальный объем памяти, указанный для этой области, используется независимо от активности рабочей нагрузки. Если в этой же емкости вы используете отчеты или потоки данных Power BI, выделяйте для отчетов с разбивкой на страницы не слишком много памяти, чтобы они не ухудшали работу других рабочих нагрузок. В редких случаях рабочая нагрузка отчетов с разбивкой на страницы может стать недоступной. В такой ситуации для этой рабочей нагрузки на портале администрирования отображается состояние ошибки, а пользователи при отрисовке отчета получают сообщения о превышении времени ожидания. Чтобы устранить эту проблему, отключите эту рабочую нагрузку и снова включите ее.

### <a name="rest-api"></a>API-интерфейсы REST

Рабочие нагрузки можно включить и назначить емкости с помощью REST API [емкостей](https://docs.microsoft.com/rest/api/power-bi/capacities).

## <a name="monitoring-workloads"></a>Мониторинг рабочих нагрузок

[Приложения метрик емкости Power BI Premium](service-admin-premium-monitor-capacity.md) предоставляет метрики, связанные с наборами данных, потоками данных и отчетами с разбивкой на страницы, для мониторинга рабочих нагрузок, которые включены для ваших емкостей. 

## <a name="next-steps"></a>Дальнейшие действия

[Использование и оптимизация ресурсов емкости Power BI Premium](service-premium-understand-how-it-works.md)   
[Самостоятельная подготовка данных в Power BI с помощью потоков данных](service-dataflows-overview.md)   
[Сведения об отчетах с разбивкой на страницы в Power BI Premium](paginated-reports-report-builder-power-bi.md)   

Появились дополнительные вопросы? [Спросить в сообществе Power BI](http://community.powerbi.com/)