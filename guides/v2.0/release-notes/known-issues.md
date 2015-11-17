---
layout: default
group: release-notes
title: Release Notes
menu_title: Known issues
menu_node: 
menu_order: 2
github_link: release-notes/known-issues.md
redirect_from: /guides/v1.0/release-notes/known-issues.html
---

<h2 id="known-devbeta">既知の問題</h2>
このページは2014年12月に始まったMagento2ディベロッパーベータでの既知の問題について記述してあります。

現在このリリースでは以下の既知の問題が検知されています：

<!-- *   <a href="#known-devbeta-sampledata">Magento sample data is available only if you edit composer.json</a>
 -->
*   <a href="known-composer-clear-cache">Composerキャッシュをクリアしなければならないかもしれない</a>
*   <a href="#known-devrc-php">特定PHPバージョンでタイムゾーンの既知の問題</a>
*   <a href="#known-devbeta-xdebug">xdebugの既知の問題</a>
*   <a href="#known-devbeta-storefront-err">アクセスエラー</a>
*   <a href="#known-devbeta-wiz-fail-bogus">セットアップウィザード失敗の誤報</a>
*   <a href="#known-devbeta-wiz-fail-installog">インストールログがないためにセットアップウィザードが失敗する</a>
<!-- *   <a href="#known-devbeta-wiz-fail-session-save">session.save_path issue</a> -->

<!-- <h3 id="known-issue-sample">Issue installing optional sample data</h3> -->
<!-- https://jira.corp.x.com/browse/MAGETWO-32879 -->
<!-- Errors display when you attempt to install optional Magento sample data. We are working on this issue and expect a resolution in the near future. -->

<h3 id="known-composer-clear-cache">Composerキャッシュをクリアしなければならないかもしれない</h3>
{% include install/composer-clear-cache.html %}

<h3 id="known-devrc-php">特定PHPバージョンでタイムゾーンの既知の問題</h3>
この問題は0.74beta10ビルド以前のみに影響します。以降のビルドをお使いの場合はこの問題は無視してください。

<a href="https://bugs.php.net/bug.php?id=66985" target="_blank">known PHP issue</a>が次のバージョンにあります:

*   5.5.10&ndash;5.5.16
*   5.6.0

この問題はユーザーから自身のタイムゾーンをグリニッジ標準時やその他のタイムゾーンに設定することできなくします。

この問題を回避するためにMagento2ソフトウェアをインストール後に以下のファイルを編集してください:

*   `app/code/Magento/Config/Model/Config/Backend/Locale/Timezone.php`
*   `lib/internal/Magento/Framework/Locale/Lists.php`
*   `setup/src/Magento/Setup/Model/Lists.php`

各ファイルにて`$zones`の値を以下の様に変更してください：

編集前

    $zones = \DateTimeZone::listIdentifiers(\DateTimeZone::ALL_WITH_BC);

編集後

    $zones = \DateTimeZone::listIdentifiers(\DateTimeZone::ALL);


<h3 id="known-devbeta-xdebug">xdebugの既知の問題</h3>
もしオプショナルPHPエクステンション`xdebug`をお使いの場合、エクセプションに遭遇するかもしれません:

*   インストール中 
*   Magento Adminあるいはストアフロントのどちらかにインストール成功後にアクセスした場合 

サンプルエクセプション:

    Fatal error: Maximum function nesting level of '100' reached, aborting!

この問題を解決するためには:

*   `xdebug`エクステンションを無効化
*  `xdebug.max_nesting_level`の値を200か以上に設定してください。 更なる情報のためには、 <a href="http://xdebug.org/docs/basic#max_nesting_level" target="_blank">xdebug documentation</a>を御覧ください。


After you change the configuration of or disable `xdebug`, restart Apache:
コンフィギュレーションを変更か`xdebug`を無効化した後に, Apacheを再起動してください:

*   CentOS: `sudo service httpd restart`
*   Ubuntu: `sudo service apache2 restart`

<h3 id="known-devbeta-storefront-err">アクセスエラー</h3>

インストール後にMagentoストアフロントかMagento Adminにアクセスしようとするとエラーが表示されることがあります:

ストアフロント:

    "Can't create directory /var/www/html/m/var/generation/Magento/Framework/App/PageCache/Identifier/."
    #0 /var/www/html/m/lib/internal/Magento/Framework/Code/Generator/Autoloader.php(34): Magento\Framework\Code\Generator->generateClass('Magento\\Framewo...')
    #1 [internal function]: Magento\Framework\Code\Generator\Autoloader->load('Magento\\Framewo...')
    #2 [internal function]: spl_autoload_call('Magento\\Framewo...')
    ... more

Magento Admin:

    "Class Magento\Logging\Model\FlagFactory does not exist"
    "#0 /var/www/html/ui/lib/internal/Magento/Framework/ObjectManager/Definition/Runtime.php(46): Magento\Framework\Code\Reader\ClassReader->getConstructor('Magento\\Logging...')
    #1 /var/www/html/ui/lib/internal/Magento/Framework/ObjectManager/Factory/Factory.php(170): Magento\Framework\ObjectManager\Definition\Runtime->getParameters('Magento\\Logging...')
    #2 /var/www/html/ui/lib/internal/Magento/Framework/ObjectManager/ObjectManager.php(71): Magento\Framework\ObjectManager\Factory\Factory->create('Magento\\Logging...')
    ... more

どちらのケースでもストアフロントかMagento Adminに再度アクセスしてみてください。

<h3 id="known-devbeta-wiz-fail-bogus">セットアップウィザード失敗の誤報</h3>

まれにセットアップウィザードが実際には失敗してないのに失敗したように表示されることがあります。 

事象例:

*   以下のメッセージが最後のページのブラウザーのトップに表示されます: `Installation is incomplete. Check the console log for errors before trying again.`
*   コンソールを開いて成功のメッセージがページの最後に表示されエラーやエクセプションが表示されない。 

この場合インストールは成功です。 <a href="{{ site.gdeurl }}install-gde/install/verify.html">Verify the installation</a>で述べられたようにストアフロントとMagento Adminにアクセスすることが可能です。

Magento生成の暗号キーにアクセスするには:

1.  `root`権限のあるユーザーでMagentoサーバーにログインしてください。
2.  以下のどちらかをおこなってください:

    *   Build 0.74-beta9 あるいはそれ以前: `<your Magento install dir>/app/etc/config.php`をテキストエディターで開く。 
    *   Build 0.74-beta10 あるいはそれ以降: `<your Magento install dir>/app/etc/env.php`をテキストエディターで開く。 
    
3.  `'key' =>`の値を見つける
        
これが暗号キーです。

<h3 id="known-devbeta-wiz-fail-installog">インストールログがないためにセットアップウィザードが失敗する</h3>

まれに (例えばセットアップウィザードを同時に２つのブラウザウィンドウで走らせたり、タブで開いたりすると), `install.log`が生成されずインストールが失敗することがあります。 

この問題を回避するには <a href="{{ site.gdeurl }}install-gde/trouble/tshoot_install-log.html">Installation fails; cannot create install.log</a>を御覧ください。

<!-- <h3 id="known-devbeta-wiz-fail-session-save">session.save_path issue</h3>

<!-- <a href="https://jira.corp.x.com/browse/MAGETWO-31851">MAGETWO-31851</a> and <a href="https://github.com/magento/magento2/issues/792">GitHub issue 792</a> --><!-- There is a known issue that prevents the usage of <a href="http://php.net/manual/en/configuration.changes.php" target="_blank">php_admin_value</a> for some session configuration settings. Specifically, we are aware that the <a href="http://php.net/manual/en/session.configuration.php#ini.session.save-path" target="_blank">session.save_path</a> cannot be set with `php_admin_value` at this time.

Workarounds:

*   If you're using a hosting provider that does not allow you to change the value of `php_admin_value`, there is no workaround currently. However, the only known instance that we are aware of at this time is ISPManager/ISPConfig which appears to have a <a href="http://www.howtoforge.com/forums/showthread.php?t=61127" target="_blank">method of disabling</a> the `php_admin_value` setting.


*   If you're running the Magento software on your own server and you can log in as a user with `root` privileges, you can replace the `session.save_path` setting with a dependency injection call as follows:

1.  Log in to your Magento server as a user with `root` privileges.
2.  Open `php.ini` in a text editor.
3.  Search for `session.save_path`.
4.  Comment it out.
5.  Save your changes to `php.ini` and exit the text editor.
6.  Restart your web server.
7.  Open `<your Magento install dir>/app/etc/config.php` in a text editor.
8.  Add the following:

        ‘session’ => [
            ‘save_path’ => ‘<your session save path>'

1.  Save your changes and exit the text editor.
2.  Restart Apache.

    Ubuntu: `sudo service apache2 restart`
    CentOS: `sudo service httpd restart`

The Magento system now uses dependency injection for session save settings.

<h4>Finding php.ini</h4>

If you don't know where `php.ini` is located, use the following steps:

1.  If you haven't already done so, create <a href="{{ site.gdeurl }}install-gde/prereq/optional.html#install-optional-phpinfo">phpinfo.php</a>.
2.  Enter the following URL in your browser's address or location field:

    <code>http://&lt;your web server IP or host name>/&lt;path to docroot>/phpinfo.php</code>

3.  Look for the location of `php.ini`.

    `php.ini` is typically specified as **Loaded Configuration File** in the displayed results.

4.  As a user with <code>root</code> privileges, open `php.ini` in a text editor.
5.  Locate the value of `open_basedir` and change it.
6.  Save your changes to `php.ini`.
7.  Restart the web server. -->
