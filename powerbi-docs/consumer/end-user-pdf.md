---
title: Экспорт отчетов в формат PDF
description: Узнайте, как экспортировать отчет из Power BI в формат PDF.
author: mihart
manager: kvivek
ms.custom: ''
ms.reviewer: cmfinlan
ms.service: powerbi
ms.subservice: powerbi-service
ms.topic: conceptual
ms.date: 02/04/2019
ms.author: mihart
LocalizationGroup: Share your work
ms.openlocfilehash: c18257f1f4e4e3f325c8d4d895e3b6abf88e900c
ms.sourcegitcommit: 54d44deb6e03e518ad6378656c769b06f2a0b6dc
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/07/2019
ms.locfileid: "55795009"
---
# <a name="export-reports-from-power-bi-to-pdf"></a>Экспорт отчетов из Power BI в формат PDF
В Power BI можно опубликовать отчет в формате PDF и без труда создать на его основе документ. При **экспорте в формат PDF** каждая страница отчета Power BI становится в документе PDF отдельной страницей.

## <a name="how-to-export-your-power-bi-report-to-pdf"></a>Экспорт отчета из Power BI в формат PDF
В службе Power BI выберите отчет, чтобы он отобразился на холсте. Можно также выбрать отчет на главной странице, в разделе "Приложения" или в любом другом разделе в области навигации слева.

1. В строке меню выберите **Файл** > **Экспорт в PDF**.

    ![Выберите "Файл" в строке меню и щелкните "Экспорт в PDF"](media/end-user-pdf/power-bi-export-pdf.png)

    В правом верхнем углу появится индикатор выполнения. Экспорт может занять несколько минут. Пока он выполняется, вы можете продолжать работать в Power BI.

    ![Сообщение о ходе экспорта](media/end-user-pdf/power-bi-export-message.png)

    Когда экспорт завершится, баннер уведомления изменится, сообщая, что служба Power BI завершила экспортирование.

2. После этого ваш файл станет доступным для скачивания в браузере. На рисунке ниже показано сообщение в нижней части браузера, предлагающее скачать файл.

    ![Расположение со скачанным файлом](media/end-user-pdf/power-bi-save-file.png)

Вот, собственно, и все. Вы можете скачать файл и открыть его в любом средстве просмотра PDF-файлов, в том числе имеющемся в Microsoft Edge.


## <a name="limitations-and-considerations"></a>Рекомендации и ограничения
При работе с функцией **Экспорт в PDF** следует учитывать ряд рекомендаций и ограничений.

- Интерактивные возможности сеанса, такие как выделение и фильтрация, детализация и т. д., пока не поддерживаются при экспорте в PDF. В экспортированном файле PDF исходные визуальные элементы отображаются так, как они были сохранены в отчете. Если вы применили фильтры и срезы, которые нужно сохранить при экспорте, сохраните отчет, а затем выполните экспорт.

* **Визуальные элементы R** пока не поддерживаются. В файле PDF эти элементы будут пустыми, и будет выведено сообщение об ошибке.  

* **Пользовательские визуальные элементы**, которые прошли **сертификацию**, поддерживаются. Дополнительные сведения о сертифицированных пользовательских визуальных элементах, включая способы получения сертификации, см. в статье [Получение сертификации для пользовательского визуального элемента](../power-bi-custom-visuals-certified.md). Пользовательские визуальные элементы, которые не прошли сертификацию, не поддерживаются. В файле PDF вместо них будет выведено сообщение об ошибке.   

* Экспорт отчетов, в которых больше 30 страниц, пока не поддерживается.

* Процесс экспорта отчета в формат PDF может занять несколько минут, поэтому наберитесь терпения. На продолжительность экспорта могут влиять такие факторы, как структура отчета и текущая нагрузка на службу Power BI.

* Если в службе Power BI в меню нет пункта **Экспорт в PDF**, вероятно, эта функция отключена администратором клиента. Обратитесь к администратору клиента за подробными сведениями.

* Фоновые изображения будут обрезаны по ограничивающей области диаграммы. Настоятельно рекомендуем удалить фоновые рисунки перед экспортом в PDF.

* Отчеты, принадлежащие пользователям вне домена клиента Power BI (например, отчет, принадлежащий пользователю не из вашей организации, к которому он предоставил вам доступ), нельзя опубликовать в PDF.

* Если вы совместно используете панель мониторинга с кем-либо не из вашей организации (то есть этот пользователь находится вне клиента Power BI), этот пользователь не сможет экспортировать отчеты, связанные с общей панелью мониторинга, в формат PDF. Например, если вы aaron@contoso.com, вы сможете предоставить общий доступ cassie@cohowinery.com. Однако cassie@cohowinery.com не может экспортировать связанные отчеты в PDF.

* Служба Power BI использует параметр языка Power BI в качестве языка для экспорта в формат PDF. Чтобы просмотреть или настроить параметры языка, щелкните значок шестеренки и выберите **Параметры** > **Общие** > **Язык**.

## <a name="next-steps"></a>Дальнейшие действия
[Печать отчета](end-user-print.md)