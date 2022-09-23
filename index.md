---
title: Online gehostete Anweisungen
permalink: index.html
layout: home
ms.openlocfilehash: 928f59a9cdc6a3f70d5ad651fb1b5a45b405cee8
ms.sourcegitcommit: 1117342052bce0bbd5a703bd1f763862b9129807
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/16/2022
ms.locfileid: "140682425"
---
# <a name="azure-data-fundamentals-exercises"></a>Übungen zu Azure Data Fundamentals

Verwenden Sie die nachstehenden Links, um die Übungen für das Praxislab zum Microsoft-Kurs [DP-900 *Microsoft Azure Data Fundamentals*](https://docs.microsoft.com/learn/certifications/courses/dp-900t00) durchzuführen.

Sie benötigen ein Microsoft Azure-Abonnement für diese Übungen. Falls Sie kein Abonnement von Ihrem Kursleiter erhalten haben, können Sie sich unter [https://azure.microsoft.com](https://azure.microsoft.com) für eine kostenlose Testversion registrieren.

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" %}
| Modul | Labor |
| --- | --- | 
{% for activity in labs  %}| {{ activity.lab.module }} | [{{ activity.lab.title }}{% if activity.lab.type %} – {{ activity.lab.type }}{% endif %}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
