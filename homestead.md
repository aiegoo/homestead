<article>
		<h1>Laravel Homestead</h1>
<ul>
<li><a href="#introduction">Introduction</a></li>
<li><a href="#installation-and-setup">Installation &amp; Setup</a>
<ul>
<li><a href="#first-steps">First Steps</a></li>
<li><a href="#configuring-homestead">Configuring Homestead</a></li>
<li><a href="#launching-the-vagrant-box">Launching The Vagrant Box</a></li>
<li><a href="#per-project-installation">Per Project Installation</a></li>
<li><a href="#installing-mariadb">Installing MariaDB</a></li>
<li><a href="#installing-mongodb">Installing MongoDB</a></li>
<li><a href="#installing-elasticsearch">Installing Elasticsearch</a></li>
<li><a href="#installing-neo4j">Installing Neo4j</a></li>
<li><a href="#aliases">Aliases</a></li>
</ul></li>
<li><a href="#daily-usage">Daily Usage</a>
<ul>
<li><a href="#accessing-homestead-globally">Accessing Homestead Globally</a></li>
<li><a href="#connecting-via-ssh">Connecting Via SSH</a></li>
<li><a href="#connecting-to-databases">Connecting To Databases</a></li>
<li><a href="#database-backups">Database Backups</a></li>
<li><a href="#database-snapshots">Database Snapshots</a></li>
<li><a href="#adding-additional-sites">Adding Additional Sites</a></li>
<li><a href="#environment-variables">Environment Variables</a></li>
<li><a href="#configuring-cron-schedules">Configuring Cron Schedules</a></li>
<li><a href="#configuring-mailhog">Configuring Mailhog</a></li>
<li><a href="#configuring-minio">Configuring Minio</a></li>
<li><a href="#ports">Ports</a></li>
<li><a href="#sharing-your-environment">Sharing Your Environment</a></li>
<li><a href="#multiple-php-versions">Multiple PHP Versions</a></li>
<li><a href="#web-servers">Web Servers</a></li>
<li><a href="#mail">Mail</a></li>
</ul></li>
<li><a href="#debugging-and-profiling">Debugging &amp; Profiling</a>
<ul>
<li><a href="#debugging-web-requests">Debugging Web Requests With Xdebug</a></li>
<li><a href="#debugging-cli-applications">Debugging CLI Applications</a></li>
</ul></li>
<li><a href="#network-interfaces">Network Interfaces</a></li>
<li><a href="#extending-homestead">Extending Homestead</a></li>
<li><a href="#updating-homestead">Updating Homestead</a></li>
<li><a href="#provider-specific-settings">Provider Specific Settings</a>
<ul>
<li><a href="#provider-specific-virtualbox">VirtualBox</a></li>
</ul></li>
</ul>
<p><a name="introduction"></a></p>
<h2><a href="#introduction">Introduction</a></h2>
<p>Laravel strives to make the entire PHP development experience delightful, including your local development environment. <a href="https://www.vagrantup.com">Vagrant</a> provides a simple, elegant way to manage and provision Virtual Machines.</p>
<p>Laravel Homestead is an official, pre-packaged Vagrant box that provides you a wonderful development environment without requiring you to install PHP, a web server, and any other server software on your local machine. No more worrying about messing up your operating system! Vagrant boxes are completely disposable. If something goes wrong, you can destroy and re-create the box in minutes!</p>
<p>Homestead runs on any Windows, Mac, or Linux system, and includes the Nginx web server, PHP 7.3, PHP 7.2, PHP 7.1, MySQL, PostgreSQL, Redis, Memcached, Node, and all of the other goodies you need to develop amazing Laravel applications.</p>
<blockquote class="has-icon">
<p class="note"><div class="flag"><span class="svg"><svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:a="http://ns.adobe.com/AdobeSVGViewerExtensions/3.0/" version="1.1" x="0px" y="0px" width="90px" height="90px" viewBox="0 0 90 90" enable-background="new 0 0 90 90" xml:space="preserve"><path fill="#FFFFFF" d="M45 0C20.1 0 0 20.1 0 45s20.1 45 45 45 45-20.1 45-45S69.9 0 45 0zM45 74.5c-3.6 0-6.5-2.9-6.5-6.5s2.9-6.5 6.5-6.5 6.5 2.9 6.5 6.5S48.6 74.5 45 74.5zM52.1 23.9l-2.5 29.6c0 2.5-2.1 4.6-4.6 4.6 -2.5 0-4.6-2.1-4.6-4.6l-2.5-29.6c-0.1-0.4-0.1-0.7-0.1-1.1 0-4 3.2-7.2 7.2-7.2 4 0 7.2 3.2 7.2 7.2C52.2 23.1 52.2 23.5 52.1 23.9z"></path></svg></span></div> If you are using Windows, you may need to enable hardware virtualization (VT-x). It can usually be enabled via your BIOS. If you are using Hyper-V on a UEFI system you may additionally need to disable Hyper-V in order to access VT-x.</p>
</blockquote>
<p><a name="included-software"></a></p>
<h3>Included Software</h3>
<style>
    #software-list > ul {
        column-count: 3; -moz-column-count: 3; -webkit-column-count: 3;
        column-gap: 5em; -moz-column-gap: 5em; -webkit-column-gap: 5em;
        line-height: 1.9;
    }
</style>
<div id="software-list">
<ul>
<li>Ubuntu 18.04</li>
<li>Git</li>
<li>PHP 7.3</li>
<li>PHP 7.2</li>
<li>PHP 7.1</li>
<li>Nginx</li>
<li>MySQL</li>
<li>lmm for MySQL or MariaDB database snapshots</li>
<li>Sqlite3</li>
<li>PostgreSQL</li>
<li>Composer</li>
<li>Node (With Yarn, Bower, Grunt, and Gulp)</li>
<li>Redis</li>
<li>Memcached</li>
<li>Beanstalkd</li>
<li>Mailhog</li>
<li>avahi</li>
<li>ngrok</li>
<li>Xdebug</li>
<li>XHProf / Tideways / XHGui</li>
<li>wp-cli</li>
<li>Minio</li>
</ul>
</div>
<p><a name="optional-software"></a></p>
<h3>Optional Software</h3>
<style>
    #software-list > ul {
        column-count: 3; -moz-column-count: 3; -webkit-column-count: 3;
        column-gap: 5em; -moz-column-gap: 5em; -webkit-column-gap: 5em;
        line-height: 1.9;
    }
</style>
<div id="software-list">
<ul>
<li>Apache</li>
<li>Crystal &amp; Lucky Framework</li>
<li>Dot Net Core</li>
<li>Elasticsearch</li>
<li>Go</li>
<li>MariaDB</li>
<li>MongoDB</li>
<li>Neo4j</li>
<li>Oh My Zsh</li>
<li>Ruby &amp; Rails</li>
<li>Webdriver &amp; Laravel Dusk Utilities</li>
<li>Zend Z-Ray</li>
</ul>
</div>
<p><a name="installation-and-setup"></a></p>
<h2><a href="#installation-and-setup">Installation &amp; Setup</a></h2>
<p><a name="first-steps"></a></p>
<h3>First Steps</h3>
<p>Before launching your Homestead environment, you must install <a href="https://www.virtualbox.org/wiki/Downloads">VirtualBox</a>, <a href="https://www.vmware.com">VMWare</a>, <a href="https://www.parallels.com/products/desktop/">Parallels</a> or <a href="https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v">Hyper-V</a> as well as <a href="https://www.vagrantup.com/downloads.html">Vagrant</a>. All of these software packages provide easy-to-use visual installers for all popular operating systems.</p>
<p>To use the VMware provider, you will need to purchase both VMware Fusion / Workstation and the <a href="https://www.vagrantup.com/vmware">VMware Vagrant plug-in</a>. Though it is not free, VMware can provide faster shared folder performance out of the box.</p>
<p>To use the Parallels provider, you will need to install <a href="https://github.com/Parallels/vagrant-parallels">Parallels Vagrant plug-in</a>. It is free of charge.</p>
<p>Because of <a href="https://www.vagrantup.com/docs/hyperv/limitations.html">Vagrant limitations</a>, The Hyper-V provider ignores all networking settings.</p>
<h4>Installing The Homestead Vagrant Box</h4>
<p>Once VirtualBox / VMware and Vagrant have been installed, you should add the <code class=" language-php">laravel<span class="token operator">/</span>homestead</code> box to your Vagrant installation using the following command in your terminal. It will take a few minutes to download the box, depending on your Internet connection speed:</p>
<pre class=" language-php"><code class=" language-php">vagrant box add laravel<span class="token operator">/</span>homestead</code></pre>
<p>If this command fails, make sure your Vagrant installation is up to date.</p>
<h4>Installing Homestead</h4>
<p>You may install Homestead by cloning the repository onto your host machine. Consider cloning the repository into a <code class=" language-php">Homestead</code> folder within your "home" directory, as the Homestead box will serve as the host to all of your Laravel projects:</p>
<pre class=" language-php"><code class=" language-php">git clone https<span class="token punctuation">:</span><span class="token operator">/</span><span class="token operator">/</span>github<span class="token punctuation">.</span>com<span class="token operator">/</span>laravel<span class="token operator">/</span>homestead<span class="token punctuation">.</span>git <span class="token operator">~</span><span class="token operator">/</span>Homestead</code></pre>
<p>You should check out a tagged version of Homestead since the <code class=" language-php">master</code> branch may not always be stable. You can find the latest stable version on the <a href="https://github.com/laravel/homestead/releases">GitHub Release Page</a>:</p>
<pre class=" language-php"><code class=" language-php">cd <span class="token operator">~</span><span class="token operator">/</span>Homestead
<span class="token comment" spellcheck="true">
// Clone the desired release...
</span>git checkout v8<span class="token number">.4</span><span class="token punctuation">.</span><span class="token number">0</span></code></pre>
<p>Once you have cloned the Homestead repository, run the <code class=" language-php">bash init<span class="token punctuation">.</span>sh</code> command from the Homestead directory to create the <code class=" language-php">Homestead<span class="token punctuation">.</span>yaml</code> configuration file. The <code class=" language-php">Homestead<span class="token punctuation">.</span>yaml</code> file will be placed in the Homestead directory:</p>
<pre class=" language-php"><code class=" language-php"><span class="token comment" spellcheck="true">// Mac / Linux...
</span>bash init<span class="token punctuation">.</span>sh
<span class="token comment" spellcheck="true">
// Windows...
</span>init<span class="token punctuation">.</span>bat</code></pre>
<p><a name="configuring-homestead"></a></p>
<h3>Configuring Homestead</h3>
<h4>Setting Your Provider</h4>
<p>The <code class=" language-php">provider</code> key in your <code class=" language-php">Homestead<span class="token punctuation">.</span>yaml</code> file indicates which Vagrant provider should be used: <code class=" language-php">virtualbox</code>, <code class=" language-php">vmware_fusion</code>, <code class=" language-php">vmware_workstation</code>, <code class=" language-php">parallels</code> or <code class=" language-php">hyperv</code>. You may set this to the provider you prefer:</p>
<pre class=" language-php"><code class=" language-php">provider<span class="token punctuation">:</span> virtualbox</code></pre>
<h4>Configuring Shared Folders</h4>
<p>The <code class=" language-php">folders</code> property of the <code class=" language-php">Homestead<span class="token punctuation">.</span>yaml</code> file lists all of the folders you wish to share with your Homestead environment. As files within these folders are changed, they will be kept in sync between your local machine and the Homestead environment. You may configure as many shared folders as necessary:</p>
<pre class=" language-php"><code class=" language-php">folders<span class="token punctuation">:</span>
    <span class="token operator">-</span> map<span class="token punctuation">:</span> <span class="token operator">~</span><span class="token operator">/</span>code
      to<span class="token punctuation">:</span> <span class="token operator">/</span>home<span class="token operator">/</span>vagrant<span class="token operator">/</span>code</code></pre>
<p>If you are only creating a few sites, this generic mapping will work just fine. However, as the number of sites continue to grow, you may begin to experience performance problems. This problem can be painfully apparent on low-end machines or projects that contain a very large number of files. If you are experiencing this issue, try mapping every project to its own Vagrant folder:</p>
<pre class=" language-php"><code class=" language-php">folders<span class="token punctuation">:</span>
    <span class="token operator">-</span> map<span class="token punctuation">:</span> <span class="token operator">~</span><span class="token operator">/</span>code<span class="token operator">/</span>project1
      to<span class="token punctuation">:</span> <span class="token operator">/</span>home<span class="token operator">/</span>vagrant<span class="token operator">/</span>code<span class="token operator">/</span>project1

    <span class="token operator">-</span> map<span class="token punctuation">:</span> <span class="token operator">~</span><span class="token operator">/</span>code<span class="token operator">/</span>project2
      to<span class="token punctuation">:</span> <span class="token operator">/</span>home<span class="token operator">/</span>vagrant<span class="token operator">/</span>code<span class="token operator">/</span>project2</code></pre>
<p>To enable <a href="https://www.vagrantup.com/docs/synced-folders/nfs.html">NFS</a>, you only need to add a simple flag to your synced folder configuration:</p>
<pre class=" language-php"><code class=" language-php">folders<span class="token punctuation">:</span>
    <span class="token operator">-</span> map<span class="token punctuation">:</span> <span class="token operator">~</span><span class="token operator">/</span>code
      to<span class="token punctuation">:</span> <span class="token operator">/</span>home<span class="token operator">/</span>vagrant<span class="token operator">/</span>code
      type<span class="token punctuation">:</span> <span class="token string">"nfs"</span></code></pre>
<blockquote class="has-icon">
<p class="note"><div class="flag"><span class="svg"><svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:a="http://ns.adobe.com/AdobeSVGViewerExtensions/3.0/" version="1.1" x="0px" y="0px" width="90px" height="90px" viewBox="0 0 90 90" enable-background="new 0 0 90 90" xml:space="preserve"><path fill="#FFFFFF" d="M45 0C20.1 0 0 20.1 0 45s20.1 45 45 45 45-20.1 45-45S69.9 0 45 0zM45 74.5c-3.6 0-6.5-2.9-6.5-6.5s2.9-6.5 6.5-6.5 6.5 2.9 6.5 6.5S48.6 74.5 45 74.5zM52.1 23.9l-2.5 29.6c0 2.5-2.1 4.6-4.6 4.6 -2.5 0-4.6-2.1-4.6-4.6l-2.5-29.6c-0.1-0.4-0.1-0.7-0.1-1.1 0-4 3.2-7.2 7.2-7.2 4 0 7.2 3.2 7.2 7.2C52.2 23.1 52.2 23.5 52.1 23.9z"></path></svg></span></div> When using NFS on Windows, you should consider installing the <a href="https://github.com/winnfsd/vagrant-winnfsd">vagrant-winnfsd</a> plug-in. This plug-in will maintain the correct user / group permissions for files and directories within the Homestead box.</p>
</blockquote>
<p>You may also pass any options supported by Vagrant's <a href="https://www.vagrantup.com/docs/synced-folders/basic_usage.html">Synced Folders</a> by listing them under the <code class=" language-php">options</code> key:</p>
<pre class=" language-php"><code class=" language-php">folders<span class="token punctuation">:</span>
    <span class="token operator">-</span> map<span class="token punctuation">:</span> <span class="token operator">~</span><span class="token operator">/</span>code
      to<span class="token punctuation">:</span> <span class="token operator">/</span>home<span class="token operator">/</span>vagrant<span class="token operator">/</span>code
      type<span class="token punctuation">:</span> <span class="token string">"rsync"</span>
      options<span class="token punctuation">:</span>
          rsync__args<span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token string">"--verbose"</span><span class="token punctuation">,</span> <span class="token string">"--archive"</span><span class="token punctuation">,</span> <span class="token string">"--delete"</span><span class="token punctuation">,</span> <span class="token string">"-zz"</span><span class="token punctuation">]</span>
          rsync__exclude<span class="token punctuation">:</span> <span class="token punctuation">[</span><span class="token string">"node_modules"</span><span class="token punctuation">]</span></code></pre>
<h4>Configuring Nginx Sites</h4>
<p>Not familiar with Nginx? No problem. The <code class=" language-php">sites</code> property allows you to easily map a "domain" to a folder on your Homestead environment. A sample site configuration is included in the <code class=" language-php">Homestead<span class="token punctuation">.</span>yaml</code> file. Again, you may add as many sites to your Homestead environment as necessary. Homestead can serve as a convenient, virtualized environment for every Laravel project you are working on:</p>
<pre class=" language-php"><code class=" language-php">sites<span class="token punctuation">:</span>
    <span class="token operator">-</span> map<span class="token punctuation">:</span> homestead<span class="token punctuation">.</span>test
      to<span class="token punctuation">:</span> <span class="token operator">/</span>home<span class="token operator">/</span>vagrant<span class="token operator">/</span>code<span class="token operator">/</span>my<span class="token operator">-</span>project<span class="token operator">/</span><span class="token keyword">public</span></code></pre>
<p>If you change the <code class=" language-php">sites</code> property after provisioning the Homestead box, you should re-run <code class=" language-php">vagrant reload <span class="token operator">--</span>provision</code>  to update the Nginx configuration on the virtual machine.</p>
<p><a name="hostname-resolution"></a></p>
<h4>Hostname Resolution</h4>
<p>Homestead publishes hostnames over <code class=" language-php">mDNS</code> for automatic host resolution. If you set <code class=" language-php">hostname<span class="token punctuation">:</span> homestead</code> in your <code class=" language-php">Homestead<span class="token punctuation">.</span>yaml</code> file, the host will be available at <code class=" language-php">homestead<span class="token punctuation">.</span>local</code>. MacOS, iOS, and Linux desktop distributions include <code class=" language-php">mDNS</code> support by default. Windows requires installing <a href="https://support.apple.com/kb/DL999?viewlocale=en_US&amp;locale=en_US">Bonjour Print Services for Windows</a>.</p>
<p>Using automatic hostnames works best for "per project" installations of Homestead. If you host multiple sites on a single Homestead instance, you may add the "domains" for your web sites to the <code class=" language-php">hosts</code> file on your machine. The <code class=" language-php">hosts</code> file will redirect requests for your Homestead sites into your Homestead machine. On Mac and Linux, this file is located at <code class=" language-php"><span class="token operator">/</span>etc<span class="token operator">/</span>hosts</code>. On Windows, it is located at <code class=" language-php">C<span class="token punctuation">:</span>\<span class="token package">Windows<span class="token punctuation">\</span>System32<span class="token punctuation">\</span>drivers<span class="token punctuation">\</span>etc<span class="token punctuation">\</span>hosts</span></code>. The lines you add to this file will look like the following:</p>
<pre class=" language-php"><code class=" language-php"><span class="token number">192.168</span><span class="token punctuation">.</span><span class="token number">10.10</span>  homestead<span class="token punctuation">.</span>test</code></pre>
<p>Make sure the IP address listed is the one set in your <code class=" language-php">Homestead<span class="token punctuation">.</span>yaml</code> file. Once you have added the domain to your <code class=" language-php">hosts</code> file and launched the Vagrant box you will be able to access the site via your web browser:</p>
<pre class=" language-php"><code class=" language-php">http<span class="token punctuation">:</span><span class="token operator">/</span><span class="token operator">/</span>homestead<span class="token punctuation">.</span>test</code></pre>
<p><a name="launching-the-vagrant-box"></a></p>
<h3>Launching The Vagrant Box</h3>
<p>Once you have edited the <code class=" language-php">Homestead<span class="token punctuation">.</span>yaml</code> to your liking, run the <code class=" language-php">vagrant up</code> command from your Homestead directory. Vagrant will boot the virtual machine and automatically configure your shared folders and Nginx sites.</p>
<p>To destroy the machine, you may use the <code class=" language-php">vagrant destroy <span class="token operator">--</span>force</code> command.</p>
<p><a name="per-project-installation"></a></p>
<h3>Per Project Installation</h3>
<p>Instead of installing Homestead globally and sharing the same Homestead box across all of your projects, you may instead configure a Homestead instance for each project you manage. Installing Homestead per project may be beneficial if you wish to ship a <code class=" language-php">Vagrantfile</code> with your project, allowing others working on the project to <code class=" language-php">vagrant up</code>.</p>
<p>To install Homestead directly into your project, require it using Composer:</p>
<pre class=" language-php"><code class=" language-php">composer <span class="token keyword">require</span> laravel<span class="token operator">/</span>homestead <span class="token operator">--</span>dev</code></pre>
<p>Once Homestead has been installed, use the <code class=" language-php">make</code> command to generate the <code class=" language-php">Vagrantfile</code> and <code class=" language-php">Homestead<span class="token punctuation">.</span>yaml</code> file in your project root. The <code class=" language-php">make</code> command will automatically configure the <code class=" language-php">sites</code> and <code class=" language-php">folders</code> directives in the <code class=" language-php">Homestead<span class="token punctuation">.</span>yaml</code> file.</p>
<p>Mac / Linux:</p>
<pre class=" language-php"><code class=" language-php">php vendor<span class="token operator">/</span>bin<span class="token operator">/</span>homestead make</code></pre>
<p>Windows:</p>
<pre class=" language-php"><code class=" language-php">vendor\<span class="token package"><span class="token punctuation">\</span>bin<span class="token punctuation">\</span><span class="token punctuation">\</span>homestead</span> make</code></pre>
<p>Next, run the <code class=" language-php">vagrant up</code> command in your terminal and access your project at <code class=" language-php">http<span class="token punctuation">:</span><span class="token operator">/</span><span class="token operator">/</span>homestead<span class="token punctuation">.</span>test</code> in your browser. Remember, you will still need to add an <code class=" language-php"><span class="token operator">/</span>etc<span class="token operator">/</span>hosts</code> file entry for <code class=" language-php">homestead<span class="token punctuation">.</span>test</code> or the domain of your choice if you are not using automatic <a href="#hostname-resolution">hostname resolution</a>.</p>
<p><a name="installing-mariadb"></a></p>
<h3>Installing MariaDB</h3>
<p>If you prefer to use MariaDB instead of MySQL, you may add the <code class=" language-php">mariadb</code> option to your <code class=" language-php">Homestead<span class="token punctuation">.</span>yaml</code> file. This option will remove MySQL and install MariaDB. MariaDB serves as a drop-in replacement for MySQL so you should still use the <code class=" language-php">mysql</code> database driver in your application's database configuration:</p>
<pre class=" language-php"><code class=" language-php">box<span class="token punctuation">:</span> laravel<span class="token operator">/</span>homestead
ip<span class="token punctuation">:</span> <span class="token string">"192.168.10.10"</span>
memory<span class="token punctuation">:</span> <span class="token number">2048</span>
cpus<span class="token punctuation">:</span> <span class="token number">4</span>
provider<span class="token punctuation">:</span> virtualbox
mariadb<span class="token punctuation">:</span> <span class="token boolean">true</span></code></pre>
<p><a name="installing-mongodb"></a></p>
<h3>Installing MongoDB</h3>
<p>To install MongoDB Community Edition, update your <code class=" language-php">Homestead<span class="token punctuation">.</span>yaml</code> file with the following configuration option:</p>
<pre class=" language-php"><code class=" language-php">mongodb<span class="token punctuation">:</span> <span class="token boolean">true</span></code></pre>
<p>The default MongoDB installation will set the database username to <code class=" language-php">homestead</code> and the corresponding password to <code class=" language-php">secret</code>.</p>
<p><a name="installing-elasticsearch"></a></p>
<h3>Installing Elasticsearch</h3>
<p>To install Elasticsearch, add the <code class=" language-php">elasticsearch</code> option to your <code class=" language-php">Homestead<span class="token punctuation">.</span>yaml</code> file and specify a supported version, which may be a major version or an exact version number (major.minor.patch). The default installation will create a cluster named 'homestead'. You should never give Elasticsearch more than half of the operating system's memory, so make sure your Homestead machine has at least twice the Elasticsearch allocation:</p>
<pre class=" language-php"><code class=" language-php">box<span class="token punctuation">:</span> laravel<span class="token operator">/</span>homestead
ip<span class="token punctuation">:</span> <span class="token string">"192.168.10.10"</span>
memory<span class="token punctuation">:</span> <span class="token number">4096</span>
cpus<span class="token punctuation">:</span> <span class="token number">4</span>
provider<span class="token punctuation">:</span> virtualbox
elasticsearch<span class="token punctuation">:</span> <span class="token number">6</span></code></pre>
<blockquote class="has-icon">
<p class="tip"><div class="flag"><span class="svg"><svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:a="http://ns.adobe.com/AdobeSVGViewerExtensions/3.0/" version="1.1" x="0px" y="0px" width="56.6px" height="87.5px" viewBox="0 0 56.6 87.5" enable-background="new 0 0 56.6 87.5" xml:space="preserve"><path fill="#FFFFFF" d="M28.7 64.5c-1.4 0-2.5-1.1-2.5-2.5v-5.7 -5V41c0-1.4 1.1-2.5 2.5-2.5s2.5 1.1 2.5 2.5v10.1 5 5.8C31.2 63.4 30.1 64.5 28.7 64.5zM26.4 0.1C11.9 1 0.3 13.1 0 27.7c-0.1 7.9 3 15.2 8.2 20.4 0.5 0.5 0.8 1 1 1.7l3.1 13.1c0.3 1.1 1.3 1.9 2.4 1.9 0.3 0 0.7-0.1 1.1-0.2 1.1-0.5 1.6-1.8 1.4-3l-2-8.4 -0.4-1.8c-0.7-2.9-2-5.7-4-8 -1-1.2-2-2.5-2.7-3.9C5.8 35.3 4.7 30.3 5.4 25 6.7 14.5 15.2 6.3 25.6 5.1c13.9-1.5 25.8 9.4 25.8 23 0 4.1-1.1 7.9-2.9 11.2 -0.8 1.4-1.7 2.7-2.7 3.9 -2 2.3-3.3 5-4 8L41.4 53l-2 8.4c-0.3 1.2 0.3 2.5 1.4 3 0.3 0.2 0.7 0.2 1.1 0.2 1.1 0 2.2-0.8 2.4-1.9l3.1-13.1c0.2-0.6 0.5-1.2 1-1.7 5-5.1 8.2-12.1 8.2-19.8C56.4 12 42.8-1 26.4 0.1zM43.7 69.6c0 0.5-0.1 0.9-0.3 1.3 -0.4 0.8-0.7 1.6-0.9 2.5 -0.7 3-2 8.6-2 8.6 -1.3 3.2-4.4 5.5-7.9 5.5h-4.1H28h-0.5 -3.6c-3.5 0-6.7-2.4-7.9-5.7l-0.1-0.4 -1.8-7.8c-0.4-1.1-0.8-2.1-1.2-3.1 -0.1-0.3-0.2-0.5-0.2-0.9 0.1-1.3 1.3-2.1 2.6-2.1H41C42.4 67.5 43.6 68.2 43.7 69.6zM37.7 72.5H26.9c-4.2 0-7.2 3.9-6.3 7.9 0.6 1.3 1.8 2.1 3.2 2.1h4.1 0.5 0.5 3.6c1.4 0 2.7-0.8 3.2-2.1L37.7 72.5z"></path></svg></span></div> Check out the <a href="https://www.elastic.co/guide/en/elasticsearch/reference/current">Elasticsearch documentation</a> to learn how to customize your configuration.</p>
</blockquote>
<p><a name="installing-neo4j"></a></p>
<h3>Installing Neo4j</h3>
<p><a href="https://neo4j.com/">Neo4j</a> is a graph database management system. To install Neo4j Community Edition, update your <code class=" language-php">Homestead<span class="token punctuation">.</span>yaml</code> file with the following configuration option:</p>
<pre class=" language-php"><code class=" language-php">neo4j<span class="token punctuation">:</span> <span class="token boolean">true</span></code></pre>
<p>The default Neo4j installation will set the database username to <code class=" language-php">homestead</code> and corresponding password to <code class=" language-php">secret</code>. To access the Neo4j browser, visit <code class=" language-php">http<span class="token punctuation">:</span><span class="token operator">/</span><span class="token operator">/</span>homestead<span class="token punctuation">.</span>test<span class="token punctuation">:</span><span class="token number">7474</span></code> via your web browser. The ports <code class=" language-php"><span class="token number">7687</span></code> (Bolt), <code class=" language-php"><span class="token number">7474</span></code> (HTTP), and <code class=" language-php"><span class="token number">7473</span></code> (HTTPS) are ready to serve requests from the Neo4j client.</p>
<p><a name="aliases"></a></p>
<h3>Aliases</h3>
<p>You may add Bash aliases to your Homestead machine by modifying the <code class=" language-php">aliases</code> file within your Homestead directory:</p>
<pre class=" language-php"><code class=" language-php">alias c<span class="token operator">=</span><span class="token string">'clear'</span>
alias <span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token operator">=</span><span class="token string">'cd ..'</span></code></pre>
<p>After you have updated the <code class=" language-php">aliases</code> file, you should re-provision the Homestead machine using the <code class=" language-php">vagrant reload <span class="token operator">--</span>provision</code> command. This will ensure that your new aliases are available on the machine.</p>
<p><a name="daily-usage"></a></p>
<h2><a href="#daily-usage">Daily Usage</a></h2>
<p><a name="accessing-homestead-globally"></a></p>
<h3>Accessing Homestead Globally</h3>
<p>Sometimes you may want to <code class=" language-php">vagrant up</code> your Homestead machine from anywhere on your filesystem. You can do this on Mac / Linux systems by adding a Bash function to your Bash profile. On Windows, you may accomplish this by adding a "batch" file to your <code class=" language-php"><span class="token constant">PATH</span></code>. These scripts will allow you to run any Vagrant command from anywhere on your system and will automatically point that command to your Homestead installation:</p>
<h4>Mac / Linux</h4>
<pre class=" language-php"><code class=" language-php"><span class="token keyword">function</span> <span class="token function">homestead<span class="token punctuation">(</span></span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token punctuation">(</span> cd <span class="token operator">~</span><span class="token operator">/</span>Homestead <span class="token operator">&amp;&amp;</span> vagrant $<span class="token operator">*</span> <span class="token punctuation">)</span>
<span class="token punctuation">}</span></code></pre>
<p>Make sure to tweak the <code class=" language-php"><span class="token operator">~</span><span class="token operator">/</span>Homestead</code> path in the function to the location of your actual Homestead installation. Once the function is installed, you may run commands like <code class=" language-php">homestead up</code> or <code class=" language-php">homestead ssh</code> from anywhere on your system.</p>
<h4>Windows</h4>
<p>Create a <code class=" language-php">homestead<span class="token punctuation">.</span>bat</code> batch file anywhere on your machine with the following contents:</p>
<pre class=" language-php"><code class=" language-php">@<span class="token keyword">echo</span> off

set cwd<span class="token operator">=</span><span class="token operator">%</span>cd<span class="token operator">%</span>
set homesteadVagrant<span class="token operator">=</span>C<span class="token punctuation">:</span>\<span class="token package">Homestead</span>

cd <span class="token operator">/</span>d <span class="token operator">%</span>homesteadVagrant<span class="token operator">%</span> <span class="token operator">&amp;&amp;</span> vagrant <span class="token operator">%</span><span class="token operator">*</span>
cd <span class="token operator">/</span>d <span class="token operator">%</span>cwd<span class="token operator">%</span>

set cwd<span class="token operator">=</span>
set homesteadVagrant<span class="token operator">=</span></code></pre>
<p>Make sure to tweak the example <code class=" language-php">C<span class="token punctuation">:</span>\<span class="token package">Homestead</span></code> path in the script to the actual location of your Homestead installation. After creating the file, add the file location to your <code class=" language-php"><span class="token constant">PATH</span></code>. You may then run commands like <code class=" language-php">homestead up</code> or <code class=" language-php">homestead ssh</code> from anywhere on your system.</p>
<p><a name="connecting-via-ssh"></a></p>
<h3>Connecting Via SSH</h3>
<p>You can SSH into your virtual machine by issuing the <code class=" language-php">vagrant ssh</code> terminal command from your Homestead directory.</p>
<p>But, since you will probably need to SSH into your Homestead machine frequently, consider adding the "function" described above to your host machine to quickly SSH into the Homestead box.</p>
<p><a name="connecting-to-databases"></a></p>
<h3>Connecting To Databases</h3>
<p>A <code class=" language-php">homestead</code> database is configured for both MySQL and PostgreSQL out of the box. For even more convenience, Laravel's <code class=" language-php"><span class="token punctuation">.</span>env</code> file configures the framework to use this database out of the box.</p>
<p>To connect to your MySQL or PostgreSQL database from your host machine's database client, you should connect to <code class=" language-php"><span class="token number">127.0</span><span class="token punctuation">.</span><span class="token number">0.1</span></code> and port <code class=" language-php"><span class="token number">33060</span></code> (MySQL) or <code class=" language-php"><span class="token number">54320</span></code> (PostgreSQL). The username and password for both databases is <code class=" language-php">homestead</code> / <code class=" language-php">secret</code>.</p>
<blockquote class="has-icon">
<p class="note"><div class="flag"><span class="svg"><svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:a="http://ns.adobe.com/AdobeSVGViewerExtensions/3.0/" version="1.1" x="0px" y="0px" width="90px" height="90px" viewBox="0 0 90 90" enable-background="new 0 0 90 90" xml:space="preserve"><path fill="#FFFFFF" d="M45 0C20.1 0 0 20.1 0 45s20.1 45 45 45 45-20.1 45-45S69.9 0 45 0zM45 74.5c-3.6 0-6.5-2.9-6.5-6.5s2.9-6.5 6.5-6.5 6.5 2.9 6.5 6.5S48.6 74.5 45 74.5zM52.1 23.9l-2.5 29.6c0 2.5-2.1 4.6-4.6 4.6 -2.5 0-4.6-2.1-4.6-4.6l-2.5-29.6c-0.1-0.4-0.1-0.7-0.1-1.1 0-4 3.2-7.2 7.2-7.2 4 0 7.2 3.2 7.2 7.2C52.2 23.1 52.2 23.5 52.1 23.9z"></path></svg></span></div> You should only use these non-standard ports when connecting to the databases from your host machine. You will use the default 3306 and 5432 ports in your Laravel database configuration file since Laravel is running <em>within</em> the virtual machine.</p>
</blockquote>
<p><a name="database-backups"></a></p>
<h3>Database Backups</h3>
<p>Homestead can automatically backup your database when your Vagrant box is destroyed. To utilize this feature, you must be using Vagrant 2.1.0 or greater. Or, if you are using an older version of Vagrant, you must install the <code class=" language-php">vagrant<span class="token operator">-</span>triggers</code> plug-in. To enable automatic database backups, add the following line to your <code class=" language-php">Homestead<span class="token punctuation">.</span>yaml</code> file:</p>
<pre class=" language-php"><code class=" language-php">backup<span class="token punctuation">:</span> <span class="token boolean">true</span></code></pre>
<p>Once configured, Homestead will export your databases to <code class=" language-php">mysql_backup</code> and <code class=" language-php">postgres_backup</code> directories when the <code class=" language-php">vagrant destroy</code> command is executed. These directories can be found in the folder where you cloned Homestead or in the root of your project if you are using the <a href="#per-project-installation">per project installation</a> method.</p>
<p><a name="database-snapshots"></a></p>
<h3>Database Snapshots</h3>
<p>Homestead supports freezing the state of MySQL and MariaDB databases and branching between them using <a href="https://github.com/Lullabot/lmm">Logical MySQL Manager</a>. For example, imagine working on a site with a multi-gigabyte database. You can import the database and take a snapshot. After doing some work and creating some test content locally, you may quickly restore back to the original state.</p>
<p>Under the hood, LMM uses LVM's thin snapshot functionality with copy-on-write support. In practice, this means that changing a single row in a table will only cause the changes you made to be written to disk, saving significant time and disk space during restores.</p>
<p>Since <code class=" language-php">lmm</code> interacts with LVM, it must be run as <code class=" language-php">root</code>. To see all available commands, run <code class=" language-php">sudo lmm</code> inside your Vagrant box. A common workflow looks like the following:</p>
<ol>
<li>Import a database into the default <code class=" language-php">master</code> lmm branch.</li>
<li>Save a snapshot of the unchanged database using <code class=" language-php">sudo lmm branch prod<span class="token operator">-</span><span class="token constant">YYYY</span><span class="token operator">-</span><span class="token constant">MM</span><span class="token operator">-</span><span class="token constant">DD</span></code>.</li>
<li>Modify the database.</li>
<li>Run <code class=" language-php">sudo lmm merge prod<span class="token operator">-</span><span class="token constant">YYYY</span><span class="token operator">-</span><span class="token constant">MM</span><span class="token operator">-</span><span class="token constant">DD</span></code> to undo all changes.</li>
<li>Run <code class=" language-php">sudo lmm delete <span class="token markup"><span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>branch</span><span class="token punctuation">&gt;</span></span></span></code> to delete unneeded branches.</li>
</ol>
<p><a name="adding-additional-sites"></a></p>
<h3>Adding Additional Sites</h3>
<p>Once your Homestead environment is provisioned and running, you may want to add additional Nginx sites for your Laravel applications. You can run as many Laravel installations as you wish on a single Homestead environment. To add an additional site, add the site to your <code class=" language-php">Homestead<span class="token punctuation">.</span>yaml</code> file:</p>
<pre class=" language-php"><code class=" language-php">sites<span class="token punctuation">:</span>
    <span class="token operator">-</span> map<span class="token punctuation">:</span> homestead<span class="token punctuation">.</span>test
      to<span class="token punctuation">:</span> <span class="token operator">/</span>home<span class="token operator">/</span>vagrant<span class="token operator">/</span>code<span class="token operator">/</span>my<span class="token operator">-</span>project<span class="token operator">/</span><span class="token keyword">public</span>
    <span class="token operator">-</span> map<span class="token punctuation">:</span> another<span class="token punctuation">.</span>test
      to<span class="token punctuation">:</span> <span class="token operator">/</span>home<span class="token operator">/</span>vagrant<span class="token operator">/</span>code<span class="token operator">/</span>another<span class="token operator">/</span><span class="token keyword">public</span></code></pre>
<p>If Vagrant is not automatically managing your "hosts" file, you may need to add the new site to that file as well:</p>
<pre class=" language-php"><code class=" language-php"><span class="token number">192.168</span><span class="token punctuation">.</span><span class="token number">10.10</span>  homestead<span class="token punctuation">.</span>test
<span class="token number">192.168</span><span class="token punctuation">.</span><span class="token number">10.10</span>  another<span class="token punctuation">.</span>test</code></pre>
<p>Once the site has been added, run the <code class=" language-php">vagrant reload <span class="token operator">--</span>provision</code> command from your Homestead directory.</p>
<p><a name="site-types"></a></p>
<h4>Site Types</h4>
<p>Homestead supports several types of sites which allow you to easily run projects that are not based on Laravel. For example, we may easily add a Symfony application to Homestead using the <code class=" language-php">symfony2</code> site type:</p>
<pre class=" language-php"><code class=" language-php">sites<span class="token punctuation">:</span>
    <span class="token operator">-</span> map<span class="token punctuation">:</span> symfony2<span class="token punctuation">.</span>test
      to<span class="token punctuation">:</span> <span class="token operator">/</span>home<span class="token operator">/</span>vagrant<span class="token operator">/</span>code<span class="token operator">/</span>my<span class="token operator">-</span>symfony<span class="token operator">-</span>project<span class="token operator">/</span>web
      type<span class="token punctuation">:</span> <span class="token string">"symfony2"</span></code></pre>
<p>The available site types are: <code class=" language-php">apache</code>, <code class=" language-php">apigility</code>, <code class=" language-php">expressive</code>, <code class=" language-php">laravel</code> (the default), <code class=" language-php">proxy</code>, <code class=" language-php">silverstripe</code>, <code class=" language-php">statamic</code>, <code class=" language-php">symfony2</code>, <code class=" language-php">symfony4</code>, and <code class=" language-php">zf</code>.</p>
<p><a name="site-parameters"></a></p>
<h4>Site Parameters</h4>
<p>You may add additional Nginx <code class=" language-php">fastcgi_param</code> values to your site via the <code class=" language-php">params</code> site directive. For example, we'll add a <code class=" language-php"><span class="token constant">FOO</span></code> parameter with a value of <code class=" language-php"><span class="token constant">BAR</span></code>:</p>
<pre class=" language-php"><code class=" language-php">sites<span class="token punctuation">:</span>
    <span class="token operator">-</span> map<span class="token punctuation">:</span> homestead<span class="token punctuation">.</span>test
      to<span class="token punctuation">:</span> <span class="token operator">/</span>home<span class="token operator">/</span>vagrant<span class="token operator">/</span>code<span class="token operator">/</span>my<span class="token operator">-</span>project<span class="token operator">/</span><span class="token keyword">public</span>
      params<span class="token punctuation">:</span>
          <span class="token operator">-</span> key<span class="token punctuation">:</span> <span class="token constant">FOO</span>
            value<span class="token punctuation">:</span> <span class="token constant">BAR</span></code></pre>
<p><a name="environment-variables"></a></p>
<h3>Environment Variables</h3>
<p>You can set global environment variables by adding them to your <code class=" language-php">Homestead<span class="token punctuation">.</span>yaml</code> file:</p>
<pre class=" language-php"><code class=" language-php">variables<span class="token punctuation">:</span>
    <span class="token operator">-</span> key<span class="token punctuation">:</span> <span class="token constant">APP_ENV</span>
      value<span class="token punctuation">:</span> local
    <span class="token operator">-</span> key<span class="token punctuation">:</span> <span class="token constant">FOO</span>
      value<span class="token punctuation">:</span> bar</code></pre>
<p>After updating the <code class=" language-php">Homestead<span class="token punctuation">.</span>yaml</code>, be sure to re-provision the machine by running <code class=" language-php">vagrant reload <span class="token operator">--</span>provision</code>. This will update the PHP-FPM configuration for all of the installed PHP versions and also update the environment for the <code class=" language-php">vagrant</code> user.</p>
<p><a name="configuring-cron-schedules"></a></p>
<h3>Configuring Cron Schedules</h3>
<p>Laravel provides a convenient way to <a href="/docs/5.8/scheduling">schedule Cron jobs</a> by scheduling a single <code class=" language-php">schedule<span class="token punctuation">:</span>run</code> Artisan command to be run every minute. The <code class=" language-php">schedule<span class="token punctuation">:</span>run</code> command will examine the job schedule defined in your <code class=" language-php">App\<span class="token package">Console<span class="token punctuation">\</span>Kernel</span></code> class to determine which jobs should be run.</p>
<p>If you would like the <code class=" language-php">schedule<span class="token punctuation">:</span>run</code> command to be run for a Homestead site, you may set the <code class=" language-php">schedule</code> option to <code class=" language-php"><span class="token boolean">true</span></code> when defining the site:</p>
<pre class=" language-php"><code class=" language-php">sites<span class="token punctuation">:</span>
    <span class="token operator">-</span> map<span class="token punctuation">:</span> homestead<span class="token punctuation">.</span>test
      to<span class="token punctuation">:</span> <span class="token operator">/</span>home<span class="token operator">/</span>vagrant<span class="token operator">/</span>code<span class="token operator">/</span>my<span class="token operator">-</span>project<span class="token operator">/</span><span class="token keyword">public</span>
      schedule<span class="token punctuation">:</span> <span class="token boolean">true</span></code></pre>
<p>The Cron job for the site will be defined in the <code class=" language-php"><span class="token operator">/</span>etc<span class="token operator">/</span>cron<span class="token punctuation">.</span>d</code> folder of the virtual machine.</p>
<p><a name="configuring-mailhog"></a></p>
<h3>Configuring Mailhog</h3>
<p>Mailhog allows you to easily catch your outgoing email and examine it without actually sending the mail to its recipients. To get started, update your <code class=" language-php"><span class="token punctuation">.</span>env</code> file to use the following mail settings:</p>
<pre class=" language-php"><code class=" language-php"><span class="token constant">MAIL_DRIVER</span><span class="token operator">=</span>smtp
<span class="token constant">MAIL_HOST</span><span class="token operator">=</span>localhost
<span class="token constant">MAIL_PORT</span><span class="token operator">=</span><span class="token number">1025</span>
<span class="token constant">MAIL_USERNAME</span><span class="token operator">=</span><span class="token keyword">null</span>
<span class="token constant">MAIL_PASSWORD</span><span class="token operator">=</span><span class="token keyword">null</span>
<span class="token constant">MAIL_ENCRYPTION</span><span class="token operator">=</span><span class="token keyword">null</span></code></pre>
<p>Once Mailhog has been configured, you may access the Mailhog dashboard at <code class=" language-php">http<span class="token punctuation">:</span><span class="token operator">/</span><span class="token operator">/</span>localhost<span class="token punctuation">:</span><span class="token number">8025</span></code>.</p>
<p><a name="configuring-minio"></a></p>
<h3>Configuring Minio</h3>
<p>Minio is an open source object storage server with an Amazon S3 compatible API. To install Minio, update your <code class=" language-php">Homestead<span class="token punctuation">.</span>yaml</code> file with the following configuration option:</p>
<pre class=" language-php"><code class=" language-php">minio<span class="token punctuation">:</span> <span class="token boolean">true</span></code></pre>
<p>By default, Minio is available on port 9600. You may access the Minio control panel by visiting <code class=" language-php">http<span class="token punctuation">:</span><span class="token operator">/</span><span class="token operator">/</span>homestead<span class="token punctuation">:</span><span class="token number">9600</span><span class="token operator">/</span></code>. The default access key is <code class=" language-php">homestead</code>, while the default secret key is <code class=" language-php">secretkey</code>. When accessing Minio, you should always use region <code class=" language-php">us<span class="token operator">-</span>east<span class="token number">-1</span></code>.</p>
<p>In order to use Minio you will need to adjust the S3 disk configuration in your <code class=" language-php">config<span class="token operator">/</span>filesystems<span class="token punctuation">.</span>php</code> configuration file. You will need to add the <code class=" language-php">use_path_style_endpoint</code> option to the disk configuration, as well as change the <code class=" language-php">url</code> key to <code class=" language-php">endpoint</code>:</p>
<pre class=" language-php"><code class=" language-php"><span class="token string">'s3'</span> <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token punctuation">[</span>
    <span class="token string">'driver'</span> <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token string">'s3'</span><span class="token punctuation">,</span>
    <span class="token string">'key'</span> <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token function">env<span class="token punctuation">(</span></span><span class="token string">'AWS_ACCESS_KEY_ID'</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
    <span class="token string">'secret'</span> <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token function">env<span class="token punctuation">(</span></span><span class="token string">'AWS_SECRET_ACCESS_KEY'</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
    <span class="token string">'region'</span> <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token function">env<span class="token punctuation">(</span></span><span class="token string">'AWS_DEFAULT_REGION'</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
    <span class="token string">'bucket'</span> <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token function">env<span class="token punctuation">(</span></span><span class="token string">'AWS_BUCKET'</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
    <span class="token string">'endpoint'</span> <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token function">env<span class="token punctuation">(</span></span><span class="token string">'AWS_URL'</span><span class="token punctuation">)</span><span class="token punctuation">,</span>
    <span class="token string">'use_path_style_endpoint'</span> <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token boolean">true</span>
<span class="token punctuation">]</span></code></pre>
<p>Finally, ensure your <code class=" language-php"><span class="token punctuation">.</span>env</code> file has the following options:</p>
<pre class=" language-php"><code class=" language-php"><span class="token constant">AWS_ACCESS_KEY_ID</span><span class="token operator">=</span>homestead
<span class="token constant">AWS_SECRET_ACCESS_KEY</span><span class="token operator">=</span>secretkey
<span class="token constant">AWS_DEFAULT_REGION</span><span class="token operator">=</span>us<span class="token operator">-</span>east<span class="token number">-1</span>
<span class="token constant">AWS_URL</span><span class="token operator">=</span>http<span class="token punctuation">:</span><span class="token operator">/</span><span class="token operator">/</span>homestead<span class="token punctuation">:</span><span class="token number">9600</span></code></pre>
<p>To provision buckets, add a <code class=" language-php">buckets</code> directive to your Homestead configuration file:</p>
<pre class=" language-php"><code class=" language-php">buckets<span class="token punctuation">:</span>
    <span class="token operator">-</span> name<span class="token punctuation">:</span> your<span class="token operator">-</span>bucket
      policy<span class="token punctuation">:</span> <span class="token keyword">public</span>
    <span class="token operator">-</span> name<span class="token punctuation">:</span> your<span class="token operator">-</span><span class="token keyword">private</span><span class="token operator">-</span>bucket
      policy<span class="token punctuation">:</span> none</code></pre>
<p>Supported <code class=" language-php">policy</code> values include: <code class=" language-php">none</code>, <code class=" language-php">download</code>, <code class=" language-php">upload</code>, and <code class=" language-php"><span class="token keyword">public</span></code>.</p>
<p><a name="ports"></a></p>
<h3>Ports</h3>
<p>By default, the following ports are forwarded to your Homestead environment:</p>
<div class="content-list">
<ul>
<li><strong>SSH:</strong> 2222 → Forwards To 22</li>
<li><strong>ngrok UI:</strong> 4040 → Forwards To 4040</li>
<li><strong>HTTP:</strong> 8000 → Forwards To 80</li>
<li><strong>HTTPS:</strong> 44300 → Forwards To 443</li>
<li><strong>MySQL:</strong> 33060 → Forwards To 3306</li>
<li><strong>PostgreSQL:</strong> 54320 → Forwards To 5432</li>
<li><strong>MongoDB:</strong> 27017 → Forwards To 27017</li>
<li><strong>Mailhog:</strong> 8025 → Forwards To 8025</li>
<li><strong>Minio:</strong> 9600 → Forwards To 9600</li>
</ul>
</div>
<h4>Forwarding Additional Ports</h4>
<p>If you wish, you may forward additional ports to the Vagrant box, as well as specify their protocol:</p>
<pre class=" language-php"><code class=" language-php">ports<span class="token punctuation">:</span>
    <span class="token operator">-</span> send<span class="token punctuation">:</span> <span class="token number">50000</span>
      to<span class="token punctuation">:</span> <span class="token number">5000</span>
    <span class="token operator">-</span> send<span class="token punctuation">:</span> <span class="token number">7777</span>
      to<span class="token punctuation">:</span> <span class="token number">777</span>
      protocol<span class="token punctuation">:</span> udp</code></pre>
<p><a name="sharing-your-environment"></a></p>
<h3>Sharing Your Environment</h3>
<p>Sometimes you may wish to share what you're currently working on with coworkers or a  client. Vagrant has a built-in way to support this via <code class=" language-php">vagrant share</code>; however, this will not work if you have multiple sites configured in your <code class=" language-php">Homestead<span class="token punctuation">.</span>yaml</code> file.</p>
<p>To solve this problem, Homestead includes its own <code class=" language-php">share</code> command. To get started, SSH into your Homestead machine via <code class=" language-php">vagrant ssh</code> and run <code class=" language-php">share homestead<span class="token punctuation">.</span>test</code>. This will share the <code class=" language-php">homestead<span class="token punctuation">.</span>test</code> site from your <code class=" language-php">Homestead<span class="token punctuation">.</span>yaml</code> configuration file. You may substitute any of your other configured sites for <code class=" language-php">homestead<span class="token punctuation">.</span>test</code>:</p>
<pre class=" language-php"><code class=" language-php">share homestead<span class="token punctuation">.</span>test</code></pre>
<p>After running the command, you will see an Ngrok screen appear which contains the activity log and the publicly accessible URLs for the shared site. If you would like to specify a custom region, subdomain, or other Ngrok runtime option, you may add them to your <code class=" language-php">share</code> command:</p>
<pre class=" language-php"><code class=" language-php">share homestead<span class="token punctuation">.</span>test <span class="token operator">-</span>region<span class="token operator">=</span>eu <span class="token operator">-</span>subdomain<span class="token operator">=</span>laravel</code></pre>
<blockquote class="has-icon">
<p class="note"><div class="flag"><span class="svg"><svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:a="http://ns.adobe.com/AdobeSVGViewerExtensions/3.0/" version="1.1" x="0px" y="0px" width="90px" height="90px" viewBox="0 0 90 90" enable-background="new 0 0 90 90" xml:space="preserve"><path fill="#FFFFFF" d="M45 0C20.1 0 0 20.1 0 45s20.1 45 45 45 45-20.1 45-45S69.9 0 45 0zM45 74.5c-3.6 0-6.5-2.9-6.5-6.5s2.9-6.5 6.5-6.5 6.5 2.9 6.5 6.5S48.6 74.5 45 74.5zM52.1 23.9l-2.5 29.6c0 2.5-2.1 4.6-4.6 4.6 -2.5 0-4.6-2.1-4.6-4.6l-2.5-29.6c-0.1-0.4-0.1-0.7-0.1-1.1 0-4 3.2-7.2 7.2-7.2 4 0 7.2 3.2 7.2 7.2C52.2 23.1 52.2 23.5 52.1 23.9z"></path></svg></span></div> Remember, Vagrant is inherently insecure and you are exposing your virtual machine to the Internet when running the <code class=" language-php">share</code> command.</p>
</blockquote>
<p><a name="multiple-php-versions"></a></p>
<h3>Multiple PHP Versions</h3>
<p>Homestead 6 introduced support for multiple versions of PHP on the same virtual machine. You may specify which version of PHP to use for a given site within your <code class=" language-php">Homestead<span class="token punctuation">.</span>yaml</code> file. The available PHP versions are: "7.1", "7.2" and "7.3" (the default):</p>
<pre class=" language-php"><code class=" language-php">sites<span class="token punctuation">:</span>
    <span class="token operator">-</span> map<span class="token punctuation">:</span> homestead<span class="token punctuation">.</span>test
      to<span class="token punctuation">:</span> <span class="token operator">/</span>home<span class="token operator">/</span>vagrant<span class="token operator">/</span>code<span class="token operator">/</span>my<span class="token operator">-</span>project<span class="token operator">/</span><span class="token keyword">public</span>
      php<span class="token punctuation">:</span> <span class="token string">"7.1"</span></code></pre>
<p>In addition, you may use any of the supported PHP versions via the CLI:</p>
<pre class=" language-php"><code class=" language-php">php7<span class="token number">.1</span> artisan list
php7<span class="token number">.2</span> artisan list
php7<span class="token number">.3</span> artisan list</code></pre>
<p><a name="web-servers"></a></p>
<h3>Web Servers</h3>
<p>Homestead uses the Nginx web server by default. However, it can install Apache if <code class=" language-php">apache</code> is specified as a site type. While both web servers can be installed at the same time, they cannot both be <em>running</em> at the same time. The <code class=" language-php">flip</code> shell command is available to ease the process of switching between web servers. The <code class=" language-php">flip</code> command automatically determines which web server is running, shuts it off, and then starts the other server. To use this command, SSH into your Homestead machine and run the command in your terminal:</p>
<pre class=" language-php"><code class=" language-php">flip</code></pre>
<p><a name="mail"></a></p>
<h3>Mail</h3>
<p>Homestead includes the Postfix mail transfer agent, which is listening on port <code class=" language-php"><span class="token number">1025</span></code> by default. So, you may instruct your application to use the <code class=" language-php">smtp</code> mail driver on <code class=" language-php">localhost</code> port <code class=" language-php"><span class="token number">1025</span></code>. Then, all sent mail will be handled by Postfix and caught by Mailhog. To view your sent emails, open <a href="http://localhost:8025">http://localhost:8025</a> in your web browser.</p>
<p><a name="debugging-and-profiling"></a></p>
<h2><a href="#debugging-and-profiling">Debugging &amp; Profiling</a></h2>
<p><a name="debugging-web-requests"></a></p>
<h3>Debugging Web Requests With Xdebug</h3>
<p>Homestead includes support for step debugging using <a href="https://xdebug.org">Xdebug</a>. For example, you can load a web page from a browser, and PHP will connect to your IDE to allow inspection and modification of the running code.</p>
<p>To enable debugging, run the following commands inside your Vagrant box:</p>
<pre class=" language-php"><code class=" language-php">sudo phpenmod xdebug
<span class="token comment" spellcheck="true">
# Update this command to match your PHP version...
</span>sudo systemctl restart php7<span class="token number">.3</span><span class="token operator">-</span>fpm </code></pre>
<p>Next, follow your IDE's instructions to enable debugging. Finally, configure your browser to trigger Xdebug with an extension or <a href="https://www.jetbrains.com/phpstorm/marklets/">bookmarklet</a>.</p>
<blockquote class="has-icon">
<p class="note"><div class="flag"><span class="svg"><svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:a="http://ns.adobe.com/AdobeSVGViewerExtensions/3.0/" version="1.1" x="0px" y="0px" width="90px" height="90px" viewBox="0 0 90 90" enable-background="new 0 0 90 90" xml:space="preserve"><path fill="#FFFFFF" d="M45 0C20.1 0 0 20.1 0 45s20.1 45 45 45 45-20.1 45-45S69.9 0 45 0zM45 74.5c-3.6 0-6.5-2.9-6.5-6.5s2.9-6.5 6.5-6.5 6.5 2.9 6.5 6.5S48.6 74.5 45 74.5zM52.1 23.9l-2.5 29.6c0 2.5-2.1 4.6-4.6 4.6 -2.5 0-4.6-2.1-4.6-4.6l-2.5-29.6c-0.1-0.4-0.1-0.7-0.1-1.1 0-4 3.2-7.2 7.2-7.2 4 0 7.2 3.2 7.2 7.2C52.2 23.1 52.2 23.5 52.1 23.9z"></path></svg></span></div> Xdebug causes PHP to run significantly slower. To disable Xdebug, run <code class=" language-php">sudo phpdismod xdebug</code> within your Vagrant box and restart the FPM service.</p>
</blockquote>
<p><a name="debugging-cli-applications"></a></p>
<h3>Debugging CLI Applications</h3>
<p>To debug a PHP CLI application, use the <code class=" language-php">xphp</code> shell alias inside your Vagrant box:</p>
<pre class=" language-php"><code class=" language-php">xphp path<span class="token operator">/</span>to<span class="token operator">/</span>script</code></pre>
<h4>Autostarting Xdebug</h4>
<p>When debugging functional tests that make requests to the web server, it is easier to autostart debugging rather than modifying tests to pass through a custom header or cookie to trigger debugging. To force Xdebug to start automatically, modify <code class=" language-php"><span class="token operator">/</span>etc<span class="token operator">/</span>php<span class="token operator">/</span><span class="token number">7</span><span class="token comment" spellcheck="true">.#/fpm/conf.d/20-xdebug.ini</span></code> inside your Vagrant box and add the following configuration:</p>
<pre class=" language-php"><code class=" language-php"><span class="token punctuation">;</span> <span class="token keyword">If</span> Homestead<span class="token punctuation">.</span>yml contains a different subnet <span class="token keyword">for</span> the <span class="token constant">IP</span> address<span class="token punctuation">,</span> this address may be different<span class="token punctuation">.</span><span class="token punctuation">.</span><span class="token punctuation">.</span>
xdebug<span class="token punctuation">.</span>remote_host <span class="token operator">=</span> <span class="token number">192.168</span><span class="token punctuation">.</span><span class="token number">10.1</span>
xdebug<span class="token punctuation">.</span>remote_autostart <span class="token operator">=</span> <span class="token number">1</span></code></pre>
<h3>Profiling PHP Performance Using XHGui</h3>
<p><a href="https://www.github.com/perftools/xhgui">XHGui</a> is a user interface for exploring the performance of your PHP applications. To enable XHGui, add <code class=" language-php">xhgui<span class="token punctuation">:</span> <span class="token string">'true'</span></code> to your site configuration:</p>
<pre class=" language-php"><code class=" language-php">sites<span class="token punctuation">:</span>
    <span class="token operator">-</span>
        map<span class="token punctuation">:</span> your<span class="token operator">-</span>site<span class="token punctuation">.</span>test
        to<span class="token punctuation">:</span> <span class="token operator">/</span>home<span class="token operator">/</span>vagrant<span class="token operator">/</span>code<span class="token operator">/</span>web
        type<span class="token punctuation">:</span> <span class="token string">"apache"</span>
        xhgui<span class="token punctuation">:</span> <span class="token string">'true'</span></code></pre>
<p>If the site already exists, make sure to run <code class=" language-php">vagrant provision</code> after updating your configuration.</p>
<p>To profile a web request, add <code class=" language-php">xhgui<span class="token operator">=</span>on</code> as a query parameter to a request. XHGui will automatically attach a cookie to the response so that subsequent requests do not need the query string value. You may view your application profile results by browsing to <code class=" language-php">http<span class="token punctuation">:</span><span class="token operator">/</span><span class="token operator">/</span>your<span class="token operator">-</span>site<span class="token punctuation">.</span>test<span class="token operator">/</span>xhgui</code>.</p>
<p>To profile a CLI request using XHGui, prefix the command with <code class=" language-php"><span class="token constant">XHGUI</span><span class="token operator">=</span>on</code>:</p>
<pre class=" language-php"><code class=" language-php"><span class="token constant">XHGUI</span><span class="token operator">=</span>on path<span class="token operator">/</span>to<span class="token operator">/</span>script</code></pre>
<p>CLI profile results may be viewed in the same way as web profile results.</p>
<p>Note that the act of profiling slows down script execution, and absolute times may be as much as twice as real-world requests. Therefore, always compare percentage improvements and not absolute numbers. Also, be aware the execution time includes any time spent paused in a debugger.</p>
<p>Since performance profiles take up significant disk space, they are deleted automatically after a few days.</p>
<p><a name="network-interfaces"></a></p>
<h2><a href="#network-interfaces">Network Interfaces</a></h2>
<p>The <code class=" language-php">networks</code> property of the <code class=" language-php">Homestead<span class="token punctuation">.</span>yaml</code> configures network interfaces for your Homestead environment. You may configure as many interfaces as necessary:</p>
<pre class=" language-php"><code class=" language-php">networks<span class="token punctuation">:</span>
    <span class="token operator">-</span> type<span class="token punctuation">:</span> <span class="token string">"private_network"</span>
      ip<span class="token punctuation">:</span> <span class="token string">"192.168.10.20"</span></code></pre>
<p>To enable a <a href="https://www.vagrantup.com/docs/networking/public_network.html">bridged</a> interface, configure a <code class=" language-php">bridge</code> setting and change the network type to <code class=" language-php">public_network</code>:</p>
<pre class=" language-php"><code class=" language-php">networks<span class="token punctuation">:</span>
    <span class="token operator">-</span> type<span class="token punctuation">:</span> <span class="token string">"public_network"</span>
      ip<span class="token punctuation">:</span> <span class="token string">"192.168.10.20"</span>
      bridge<span class="token punctuation">:</span> <span class="token string">"en1: Wi-Fi (AirPort)"</span></code></pre>
<p>To enable <a href="https://www.vagrantup.com/docs/networking/public_network.html">DHCP</a>, just remove the <code class=" language-php">ip</code> option from your configuration:</p>
<pre class=" language-php"><code class=" language-php">networks<span class="token punctuation">:</span>
    <span class="token operator">-</span> type<span class="token punctuation">:</span> <span class="token string">"public_network"</span>
      bridge<span class="token punctuation">:</span> <span class="token string">"en1: Wi-Fi (AirPort)"</span></code></pre>
<p><a name="extending-homestead"></a></p>
<h2><a href="#extending-homestead">Extending Homestead</a></h2>
<p>You may extend Homestead using the <code class=" language-php">after<span class="token punctuation">.</span>sh</code> script in the root of your Homestead directory. Within this file, you may add any shell commands that are necessary to properly configure and customize your virtual machine.</p>
<p>When customizing Homestead, Ubuntu may ask you if you would like to keep a package's original configuration or overwrite it with a new configuration file. To avoid this, you should use the following command when installing packages to avoid overwriting any configuration previously written by Homestead:</p>
<pre class=" language-php"><code class=" language-php">sudo apt<span class="token operator">-</span>get <span class="token operator">-</span>y \
    <span class="token operator">-</span>o <span class="token scope">Dpkg<span class="token punctuation">::</span></span><span class="token scope">Options<span class="token punctuation">::</span></span><span class="token operator">=</span><span class="token string">"--force-confdef"</span> \
    <span class="token operator">-</span>o <span class="token scope">Dpkg<span class="token punctuation">::</span></span><span class="token scope">Options<span class="token punctuation">::</span></span><span class="token operator">=</span><span class="token string">"--force-confold"</span> \
    install your<span class="token operator">-</span>package</code></pre>
<p><a name="updating-homestead"></a></p>
<h2><a href="#updating-homestead">Updating Homestead</a></h2>
<p>You can update Homestead in a few simple steps. First, you should update the Vagrant box using the <code class=" language-php">vagrant box update</code> command:</p>
<pre class=" language-php"><code class=" language-php">vagrant box update</code></pre>
<p>Next, you need to update the Homestead source code. If you cloned the repository you can run the following commands at the location you originally cloned the repository:</p>
<pre class=" language-php"><code class=" language-php">git fetch

git checkout v8<span class="token number">.2</span><span class="token punctuation">.</span><span class="token number">0</span></code></pre>
<p>These commands pull the latest Homestead code from the GitHub repository, fetches the latest tags, and then checks out the latest tagged release. You can find the latest stable release version on the <a href="https://github.com/laravel/homestead/releases">GitHub releases page</a>.</p>
<p>If you have installed Homestead via your project's <code class=" language-php">composer<span class="token punctuation">.</span>json</code> file, you should ensure your <code class=" language-php">composer<span class="token punctuation">.</span>json</code> file contains <code class=" language-php"><span class="token string">"laravel/homestead"</span><span class="token punctuation">:</span> <span class="token string">"^8"</span></code> and update your dependencies:</p>
<pre class=" language-php"><code class=" language-php">composer update</code></pre>
<p>Finally, you will need to destroy and regenerate your Homestead box to utilize the latest Vagrant installation. To accomplish this, run the following commands in your Homestead directory:</p>
<pre class=" language-php"><code class=" language-php">vagrant destroy

vagrant up</code></pre>
<p><a name="provider-specific-settings"></a></p>
<h2><a href="#provider-specific-settings">Provider Specific Settings</a></h2>
<p><a name="provider-specific-virtualbox"></a></p>
<h3>VirtualBox</h3>
<h4><code class=" language-php">natdnshostresolver</code></h4>
<p>By default, Homestead configures the <code class=" language-php">natdnshostresolver</code> setting to <code class=" language-php">on</code>. This allows Homestead to use your host operating system's DNS settings. If you would like to override this behavior, add the following lines to your <code class=" language-php">Homestead<span class="token punctuation">.</span>yaml</code> file:</p>
<pre class=" language-php"><code class=" language-php">provider<span class="token punctuation">:</span> virtualbox
natdnshostresolver<span class="token punctuation">:</span> <span class="token string">'off'</span></code></pre>
<h4>Symbolic Links On Windows</h4>
<p>If symbolic links are not working properly on your Windows machine, you may need to add the following block to your <code class=" language-php">Vagrantfile</code>:</p>
<pre class=" language-php"><code class=" language-php">config<span class="token punctuation">.</span>vm<span class="token punctuation">.</span>provider <span class="token string">"virtualbox"</span> <span class="token keyword">do</span> <span class="token operator">|</span>v<span class="token operator">|</span>
    v<span class="token punctuation">.</span>customize <span class="token punctuation">[</span><span class="token string">"setextradata"</span><span class="token punctuation">,</span> <span class="token punctuation">:</span>id<span class="token punctuation">,</span> <span class="token string">"VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root"</span><span class="token punctuation">,</span> <span class="token string">"1"</span><span class="token punctuation">]</span>
end</code></pre>
	</article>
