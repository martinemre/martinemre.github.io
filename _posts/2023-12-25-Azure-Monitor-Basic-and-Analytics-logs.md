---
title: "Azure Monitor Temel Günlükler vs Analitik Günlükler"
classes: wide
author_profile: true
categories:
  - Azure
tags:
  - Azure Monitor
  - Log Analytics
---
  <img src="https://github.com/martinemre/martinemre.github.io/blob/main/assets/images/azure-basic-logs-analytics-logs.png?raw=true" width="100%" height="100%" />

  Azure Monitor maliyetlerini etkileyen iki ana etken bulunmaktadır. Bu faktörler; hangi günlüklerin **(Logs)** toplanacağı **(Ingestion)** ve bu günlüklerin Log Analytics Workspace üzerinde ne kadar süre **(Retention)** saklanacağıdır. Log Analytics Workspace'te, günlüklerin toplama ve saklama maliyetleri ile doğrudan ilişkili, Temel ve Analitik Günlükler **(Basic & Analytics)** olmak üzere iki farklı günlük veri planı bulunmaktadır.
 
**Analitik Günlükler**, varsayılan olarak toplanan tüm günlükler için kullanılan veri planıdır. Toplanan günlükler analiz amacıyla kullanılabilir; istediğiniz kadar KQL sorgusu çalıştırabilir, uyarılar oluşturabilirsiniz. Bu veri planında toplanan günlükler, varsayılan olarak 30 güne kadar ücretsiz olarak saklanır.

**Temel Günlükler**, sadece hata ayıklama, sorun giderme ve denetim amacıyla kullanılan bir günlük veri planıdır. Bu veri planında toplanan günlüklerle uyarılar oluşturmak mümkün değildir ve günlükler üzerinde analiz yapma şansınız sınırlıdır, çünkü limitli sayıda KQL desteği bulunmaktadır.

**Temel Günlükler ile Kullanılabilecek KQL Sorguları:**

* where
* extend
* project
* roject-away
* project-keep
* project-rename
* project-reorder
* parse
* parse-where

**Özetlemek Gerekirse:**

<table>
<thead>
<tr>
<th>Kategori</th>
<th>Analytics Logs</th>
<th>Basic Logs</th>
</tr>
</thead>
<tbody>
<tr>
<td>&nbsp;G&uuml;nl&uuml;k Toplama (Ingestion)</td>
<td>&nbsp;Standard &uuml;cretlendirme. GB Başına $2.76</td>
<td>
<p>Azaltılmış maliyet.</p>
<p>GB başına $0.60</p>
</td>
</tr>
<tr>
<td>&nbsp;G&uuml;nl&uuml;k sorguları</td>
<td>Ekstra maliyet olmadan tam sorgu yetenekleri</td>
<td>
<p>Temel sorgu yetenekleri.</p>
<p>Sorgu başına $0.006</p>
</td>
</tr>
<tr>
<td>&nbsp;Saklama (Retention)</td>
<td>Saklamayı 30 g&uuml;nden iki yıla kadar yapılandırılabilir</td>
<td>
<p>Saklama s&uuml;resi sekiz g&uuml;n</p>
<p>(Arşivleme ile 12 yıla kadar uzatılabilir)</p>
</td>
</tr>
<tr>
<td>&nbsp;Uyarılar(Alerts)</td>
<td>&nbsp;Destekleniyor</td>
<td>&nbsp;Desteklenmiyor</td>
</tr>
</tbody>
</table>


**Bir Tablonun Temel Günlük olarak Değiştirilmesi**

Bir tablo için günlük veri planı Analitik’ten Temel olarak değiştirildiğinde o tabloya ait 8 günden eski olan günlükler silinir yada arşivlenir. Günlük veri planı haftada sadece bir kez değiştirebilir. Bir tablo için günlük veri planını Azure Portal, CLI, API yada PowerShell ile değiştrebilirsiniz.

<img src="https://github.com/martinemre/martinemre.github.io/blob/main/assets/images/azure-log-plans-basic.png?raw=true" width="100%" height="100%" />

Temel Günlükler ile desteklenen tabloların listesine [**Buradan**](https://learn.microsoft.com/en-ie/azure/azure-monitor/logs/basic-logs-configure?tabs=portal-1#supported-tables) erişebilirsiniz.
 