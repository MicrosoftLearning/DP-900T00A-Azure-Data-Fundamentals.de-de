---
title: Online gehostete Anweisungen
permalink: index.html
layout: home
---

# <a name="azure-data-fundamentals-exercises"></a>Übungen zu Azure Data Fundamentals

Diese Praxisübungen sind dafür konzipiert, die Schulungsinhalte auf [Microsoft Learn](https://docs.microsoft.com/training/) zu ergänzen.

Sie benötigen ein Microsoft Azure-Abonnement mit Administratorberechtigungen für diese Übungen. Sie können sich unter [https://azure.microsoft.com](https://azure.microsoft.com) für eine kostenlose Testversion registrieren.

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" %}
| Übung |
| --- |
{% for activity in labs  %}| [{{ activity.lab.title }}{% if activity.lab.type %} – {{ activity.lab.type }}{% endif %}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
