---
layout: default
group: release-notes
title: Release Notes
menu_title: Highlights
menu_order: 1
menu_node: 
github_link: release-notes/bk-release-notes.md
redirect_from: /guides/v1.0/release-notes/bk-release-notes.html
---

<h2 id="highlights">ハイライト</h2>

ようこそMagento2.0のドキュメントへ！そしてようこそMagento2.0へ！

以下は2014年12月から開始されたディベロッパーベータのMagento2のすべての重要な特徴をまとめたものです。

<h3 id="highlights-devrc">このリリースのハイライト</h3>

*   サービスは変更可能 
    *   Builders から Factory Patternに変更しました
    *   インターフェイスにはsettersがあります
    *   Repository Objectsは変更して受け渡しすることができます
*   サービスは拡張した属性をアレイではなくオブジェクトとして受け渡しすることができます
    *   既存オブジェクトと追加のデータオブジェクトを簡単に展開します
    *   ジェネレーティッドコードなし
*   Varnish 4のサポート
*   サービスは<a href="{{ site.gdeurl }}extension-dev-guide/service-contracts/service-to-web-service.html">web API</a>としてSOAPとRESTをサポートして公開できます
*   SOAPについて:
    *   WSDLエンドポイントURLのサービス名はサービスインターフェイス名から派生しています。以下のルールを使用します:
    *   CamelCaseはサービス命名に使われます
    *   `Service`, `Magento` 接頭辞 と `Interface` 接尾辞を削除
    *   もしサービス名がモジュール名と同じ場合、モジュール名は削除されます(例えば、もしCustomerモジュールにカスタマーサービスインターフェイスある場合、文言`customer`はサービス名で一度のみ使われます).
    サービス名変更例は以下です:
        *   `\Magento\Customer\Service\V1\CustomerInterface` は今回から `customerV1` 
        *   `\Magento\Customer\Service\V1\CustomerAccountServiceInterface` は今回から `customerCustomerAccountServiceV1`
        *   `\Enterprise\Customer\Service\V3\Customer\AddressInterface` は今回から `enterpriseCustomerAddressV3`
    *   拡張属性オブジェクトはWSDLではオプションとしてマークされます
*   <a href="{{ site.gdeurl }}release-notes/changes.html#change-devrc-unit">Unit tests</a>は今回モジュールのディレクトリに配置されています
*   後方互換ポリシー; 次4半期にはPublic APIをマークした
    *   Semanticバージョニング2.0.0に準拠
    *   `@api`で注釈されるクラスとメソッドのための後方互換
    *   マイナーとパッチコアアップデート内のすべてのクライアントユーザーのための後方互換
    *   次の大きな変更にて削除ををお知らせするために`@deprecated`を使用します
*   `Magento_Core`モジュールを削除; ファンクションを他のモジュールに移動しました


<h3 id="highlights-tech">テクノロジースタック</h3>

-   PHPとMySQL。 Magento 2 は PHP 5.5と5.6, MySQL 5.6をサポートします。[System
    requirements][1] を御覧ください.

    [1]: <{{ site.gdeurl }}install-gde/system-requirements.html>

-   HTML5. ボックスから提供される参照テーマはレスポンシブでHTML5ベースです。 [Themes][2] と [Responsive web design][3]　を参照してください。

    [2]: <{{ site.gdeurl }}frontend-dev-guide/themes/theme-general.html>

    [3]: <{{ site.gdeurl }}frontend-dev-guide/responsive-web-design/rwd_overview.html>

-   CSS3をCSSプロセスする。 参照テーマはCSS3を使用します。 Magento 2はLESS CSSプリプロセッサーを使用します、またSassとCompassのサポートを追加することができます。
    [Cascading style sheets][4]　と [CSS pre-processor.][5]　を御覧ください。

    [4]: <{{ site.gdeurl }}frontend-dev-guide/css-topics/css-overview.html>

    [5]: <{{ site.gdeurl }}frontend-dev-guide/css-topics/css-preprocess.html>

-   jQuery. Magento 2 はjQueryをプライマリーの JavaScript ライブラリーとして使います。 Magento
    jQueryウィジェットの拡張セットと配布されます。  [Magento JQuery widgets][6] を御覧ください。

    [6]: <{{ site.gdeurl }}frontend-dev-guide/javascript/jquery-widgets-about.html>
-   RequireJS. RequireJSライブラリーJSリソースをオンデマンドでロードしてページのロードタイムを向上させます。 またフロントエンドコンポーネントのモジュラーデザインを推奨する目的もあります。 [JavaScript resources][6]　を御覧ください。

    [6]: <{{ site.gdeurl }}config-guide/config/js-resources.html>

-   PSR コンプライアンス. PSRコンプライアンスはPHPの使用を標準化して異なるコードのライブラリのセットと使用可能にします。 [PHP coding
    standard][7]を御覧ください。

    [7]: <{{ site.gdeurl }}coding-standards/code-standard-php.html>

-   モジュールアーキテクチャー。自身のモジュールのセットを定義して下さい。クロスモジュール依存が減りますし、複数のエクステンション間でのインターフェイスが美麗で簡潔です。 [What is Magento?][8], [Magento as a modular
    system][9]　と [Service contracts][10]　を御覧ください。

    [8]: <{{ site.gdeurl }}architecture/arch_whatis.html>

    [9]: <{{ site.gdeurl }}architecture/arch_asmodsys.html>

    [10]: <{{ site.gdeurl }}extension-dev-guide/service-contracts/service-contracts.html>

-   テスティングフレームワーク。 Magento 2はパッケージ化されたテストスクリプト群を含みます。テストスクリプトはインテグレーション、ユニット、static環境、ファンクショナルエリア、パフォーマンスクライテリアのテストを含みます。[Magento Test Framework][11]　と
    [JavaScript unit tests][12]　を御覧ください。

    [11]: <https://github.com/magento/mtf/blob/master/docs/install-config.md>

    [12]: <{{ site.gdeurl }}extension-dev-guide/test/test_js-unit.html>



<h2 id="help">このドキュメントの改善にご協力ください</h2>

Magento2.0製品ドキュメントはGitHubに配置してあります。フィードバックをいただけると幸いです。

このドキュメントページトップにある **Edit this page on GitHub** リンクをクリックしてGitHubのレポジトリーにあるファイルを開き、
pullリクエストにより変更を提案またはイシューを作成してディスカッションを開いていただくことができます。

ドキュメントチームに直接コンタクトも以下より可能です
<a href="mailto:DL-Magento-Doc-Feedback@ebay.com">DL-Magento-Doc-Feedback@ebay.com</a>
