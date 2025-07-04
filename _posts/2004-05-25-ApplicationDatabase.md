---
title: アプリケーションデータベース
tags: [application integration, database]
---

https://martinfowler.com/bliki/ApplicationDatabase.html

私は、単一のアプリケーションによって制御され、アクセスされるデータベースのことを（[IntegrationDatabase](/IntegrationDatabase)とは対照的に）アプリケーションデータベースと呼んでいます。データベースにアクセスするアプリケーションはひとつなので、アプリケーション要求を簡単に満たせるよう、データベースを具体的に定義することが出来ます。これにより、データベーススキーマはより具体的となり、理解しやすくなりますし、[IntegrationDatabase](/IntegrationDatabase)よりも複雑ではなくなります。

他のアプリケーションとデータベースを共有化するには、アプリケーションコントローラーがサービスを提供すればよいのです。[ReportingDatabase](/ReportingDatabase)を広く、読み取り専用で配布してもよいでしょう。

アプリケーションデータベースが非常に有利なのは、アプリケーションによってデータベースへのアクセスがカプセル化されているため、変更が簡単だという点です。[データベースの進化的設計とデータベースリファクタリング](http://www.objectclub.jp/community/XP-jp/xp_relate/evodb-jp)は、アプリケーションデータベースの設計を大幅に変更する際に使用することができます。データベースが運用され始めた後でもそれは可能です。

アプリケーションデータベースのスキーマは、アプリケーションチーム自身がうまく設計し、管理しています。経験豊富なデータベース専門家がアプリケーションチームのメンバとして参加していることもよくあります。データベース専門家は、他のアプリケーション開発者と密に連携し、アプリケーションの要求に近づけるようデータベースを最適化していく必要があります。

SOAについて議論する際、よく出てくるのが「自律アプリケーション」という言葉です。これは、データがアプリケーションデータベースにストアされているアプリケーションのことを意味します。
