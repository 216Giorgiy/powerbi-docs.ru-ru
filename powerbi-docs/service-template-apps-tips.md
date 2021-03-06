---
title: Советы по созданию приложений-шаблонов в Power BI (предварительная версия)
description: Советы по созданию запросов, моделей данных, отчетов и панелей мониторинга для разработки эффективных приложений-шаблонов.
author: maggiesMSFT
manager: kfile
ms.reviewer: ''
ms.service: powerbi
ms.subservice: powerbi-service
ms.topic: conceptual
ms.date: 02/05/2019
ms.author: maggies
ms.openlocfilehash: 282638c7c1c8a60ee93292602766d63fd0fe436e
ms.sourcegitcommit: 8207c9269363f0945d8d0332b81f1e78dc2414b0
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/14/2019
ms.locfileid: "56249849"
---
# <a name="tips-for-authoring-template-apps-in-power-bi-preview"></a>Советы по созданию приложений-шаблонов в Power BI (предварительная версия)

Процедура [создания приложения-шаблона](service-template-apps-create.md) в Power BI включает формирование рабочей области, тестирование приложения и перенос его в рабочую среду. Однако другим важным аспектом, естественно, является разработка отчета и панели мониторинга. Процесс разработки затрагивает четыре основных компонента. Работая над ними, вы можете создавать самые мощные и удобные приложения-шаблоны.

* **Запросы** позволяют [подключаться](desktop-connect-to-data.md) к данным и [преобразовывать](desktop-query-overview.md) их, а также определять [параметры](https://powerbi.microsoft.com/blog/deep-dive-into-query-parameters-and-power-bi-templates/). 
* В **модели данных** создаются [связи](desktop-create-and-manage-relationships.md) и [меры](desktop-measures.md), а также адаптируется работа с функцией "Вопросы и ответы".  
* На **[страницах отчетов](desktop-report-view.md)** находятся визуальные элементы и фильтры для анализа данных.  
* **[Панели мониторинга](consumer/end-user-dashboards.md)** и [плитки](service-dashboard-create.md) содержат обзор результатов анализа.  

Эти компоненты могут быть уже знакомы вам как существующая функция Power BI. Создавая приложение-шаблон, следует принимать во внимание ряд дополнительных факторов по каждому из них. Более подробные сведения приводятся в соответствующих разделах ниже.

<a name="queries"></a>

## <a name="queries"></a>Запросы
В приложениях-шаблонах запросы, созданные в Power BI Desktop, используются для подключения к источникам данных и импорта данных. Эти запросы необходимы для получения согласованных схем и поддерживают обновление данных по расписанию (DirectQuery не поддерживается).

### <a name="connect-to-your-api"></a>Подключение к API
Чтобы приступить к созданию запросов, нужно подключиться к API из Power BI Desktop.

Для подключения к API можно использовать стандартные соединители данных, доступные в Power BI Desktop. Вы можете использовать соединитель веб-данных ("Получить данные" -> "Интернет"), чтобы подключиться к REST API, или соединитель OData ("Получить данные" -> "Канал OData"), чтобы подключиться к каналу OData. Эти соединители работают по умолчанию, только если API поддерживает обычную проверку подлинности.

> [!NOTE]
> Если API использует другие типы проверки подлинности (например, с использованием OAuth 2.0 или ключа веб-API), вам нужно разработать собственный соединитель данных, чтобы решение Power BI Desktop могло подключаться к API и проходить проверку подлинности. Дополнительные сведения о том, как разработать собственный соединитель данных для приложения-шаблона, см. в [документации по соединителям данных](https://aka.ms/DataConnectors). 
>
>

### <a name="consider-the-source"></a>Зависимость от источника
Запросы определяют, какие данные включаются в модель данных. В зависимости от размера вашей системы такие запросы также должны включать фильтры, гарантирующие, что ваши клиенты будут работать с контролируемым размером, соответствующим вашему бизнес-сценарию.

Приложения-шаблоны Power BI могут параллельно выполнять множество запросов для множества пользователей.  Заранее продумайте стратегию регулирования и параллелизма, а также получите у нас рекомендации, как сделать приложение-шаблон отказоустойчивым.

### <a name="schema-enforcement"></a>Применение схемы
Убедитесь, что ваши запросы устойчивы к изменениям в системе, так как изменения в схеме в момент обновления могут нарушить модель. Если в ответ на некоторые запросы источник может выдавать пустой результат или сообщать об отсутствии схемы, можно настроить возврат пустой таблицы или понятных сообщений об ошибках.

### <a name="parameters"></a>Параметры
[Параметры](https://powerbi.microsoft.com/blog/deep-dive-into-query-parameters-and-power-bi-templates/) в Power BI Desktop позволяют пользователям указывать входные значения для настройки извлекаемых данных. Заранее продумайте параметры, чтобы после трудоемкого создания подробных запросов и отчетов не требовалась их переработка.

> [!NOTE]
> Приложения-шаблоны поддерживают все параметры, за исключением Any и Binary.
>

### <a name="additional-query-tips"></a>Дополнительные рекомендации по запросам

* Убедитесь, что все столбцы корректно типизированы.
* Столбцы имеют информативные имена (см. [Вопросы и ответы](#qa)).  
* Подумайте об использовании функций или запросов для совместно используемой логики.  
* В настоящее время служба не поддерживает уровни конфиденциальности. При получении запроса об уровнях конфиденциальности может потребоваться переписать запрос для использования относительных путей.  

## <a name="data-models"></a>Модели данных

Четко определенная модель данных позволяет клиентам легко и удобно взаимодействовать с приложением-шаблоном. Создайте модель данных в Power BI Desktop.

> [!NOTE]
> Основное моделирование (типизация, имена столбцов) должно осуществляться преимущественно с использованием [запросов](#queries).
>


### <a name="qa"></a>Вопросы и ответы
От моделирования также зависит, насколько хорошие результаты предоставляет вашим клиентам функция "Вопросы и ответы". Добавьте синонимы к часто используемым столбцам и следите за тем, чтобы имена столбцов были верно указаны в [запросах](#queries).

### <a name="additional-data-model-tips"></a>Дополнительные рекомендации по модели данных

Убедитесь, что выполнены следующие задачи:
* Применено форматирование ко всем столбцам значений. Применены типы в запросах.  
* Применено форматирование ко всем мерам. 
* Задан способ вычисления итогового значения по умолчанию. Особенно важно указать "Не вычислять итоговое значение", когда это необходимо (например, для уникальных значений).  
* Заданы категории данных, если применимо.  
* Заданы необходимые связи.  

## <a name="reports"></a>Отчеты
Страницы отчета позволяют получить более глубокий анализ данных, включенных в приложение-шаблон. Они ответят на ключевые бизнес-вопросы, для решения которых и создавалось приложение. Создайте отчет с помощью Power BI Desktop.

> [!NOTE]
> В приложение-шаблон можно включить только один отчет, поэтому пользуйтесь страницами для рассмотрения конкретных аспектов вашего сценария.
>
>

### <a name="additional-report-tips"></a>Дополнительные рекомендации по отчетам

* Используйте на каждой странице несколько визуальных элементов для перекрестной фильтрации.  
* Тщательно выравнивайте визуальные элементы (избегайте наложения).  
* Макет страницы может иметь режим "4:3" или "16:9".  
* Все представленные агрегаты должны иметь смысл в числовом виде (средние, уникальные значения).  
* Срезы должны давать рациональные результаты.  
* Логотип должен присутствовать как минимум на главном отчете.  
* По возможности элементы должны быть представлены в цветовой схеме клиента.  

<a name="dashboard"></a>

## <a name="dashboards"></a>Панели мониторинга
Основным инструментом взаимодействия клиентов с приложением-шаблоном служит панель мониторинга. Она должна содержать обзор содержимого пакета, особенно меры, играющие важную роль в вашем бизнес-сценарии.

Чтобы создать панель мониторинга для приложения-шаблона, просто отправьте PBIX-файл через меню "Получить данные" > "Файлы" или опубликуйте его непосредственно из Power BI Desktop.

> [!NOTE]
> Сейчас в каждое приложение-шаблон должен входить один отчет и один набор данных. Не закрепляйте на панели мониторинга, используемой в приложении-шаблоне, содержимое из нескольких отчетов или наборов данных.
>
>

### <a name="additional-dashboard-tips"></a>Дополнительные рекомендации по панелям мониторинга

* Закрепляя плитки на панели мониторинга, придерживайтесь одной общей темы.  
* Прикрепите к теме логотип, чтобы клиенты знали, откуда пакет.  
* Рекомендуется использовать макет шириной в 5–6 небольших плиток, подходящий для большинства разрешений экранов.  
* Все плитки на панели мониторинга должны иметь подходящие заголовки и подзаголовки.  
* Группируйте плитки на панели мониторинга для различных сценариев, вертикально или горизонтально.  

## <a name="known-limitations"></a>Известные ограничения

| Избранное | Известные ограничения |
|---------|---------|
|Содержимое:  наборы данных   | Должен присутствовать строго один набор данных. Разрешены только наборы данных, созданные в Power BI Desktop (PBIX-файлы). <br>Не поддерживаются: наборы данных из других приложений-шаблонов, наборы данных для нескольких рабочих областей, отчеты с разбивкой на страницы (RDL-файлы), книги Excel. |
|Содержимое: отчеты     | Не более одного отчета.    |
| Содержимое: панели мониторинга | Не более одной непустой панели мониторинга. <br>Не поддерживаются: плитки режима реального времени (другими словами, не поддерживаются PushDataset или PubNub). |
| Содержимое: потоки данных | Не поддерживаются: потоки данных |
| Содержимое из файлов | Разрешены только PBIX-файлы. <br>Не поддерживаются: RDL-файлы (отчеты с разбивкой на страницы), книги Excel.   |
| Источники данных | Разрешены источники данных, поддерживаемые для обновления данных по расписанию в облаке. <br>Не поддерживаются: <br>DirectQuery <br>Активные подключения (не Azure AS) <br>Локальные источники данных (личный и корпоративный шлюзы не поддерживаются) <br>Режим реального времени (не поддерживается PushDataset) <br>Составные модели |
| Набор данных: для нескольких рабочих областей | Наборы данных для нескольких рабочих областей недопустимы.  |
| Содержимое: панели мониторинга | Плитки режима реального времени недопустимы (другими словами, не поддерживаются PushDataset или PubNub). |
| Параметры запроса | Не поддерживаются: параметры типа Any или Binary блокируют операцию обновления набора данных. |
| Пользовательские визуальные элементы | Поддерживаются только общедоступные пользовательские визуальные элементы. [Пользовательские визуальные элементы организации](power-bi-custom-visuals-organization.md) не поддерживаются. |

## <a name="next-steps"></a>Дальнейшие действия

[Что такое приложения-шаблоны Power BI (предварительная версия)?](service-template-apps-overview.md)
