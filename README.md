<h1>This page is under construction!!!</h1>
<p>Rukovoditel is free Open Source Project Management developed by Sergey Kharchishin</p>
<h1>Supported tags and respective <code>Dockerfile</code> links</h1>
<li><a href="https://github.com/filipmil-Rukovodiltel-In-Docker/Rukovoditel/blob/master/Dockerfile"><code>2.6.1 latest</code></a></li>
<h1>Quick reference</h1>
<li><b>Where to get help: </b><a href="https://forum.rukovoditel.net">Rukovoditel forum</a></li>
<li><b>Where to file issues: </b><a href="https://github.com/filipmil-Rukovodiltel-In-Docker/Rukovoditel/issues">https://github.com/filipmil-Rukovodiltel-In-Docker/Rukovoditel/issues</a></li>
<li><b>Repository maintained by: </b><a href="https://github.com/filipmil-Rukovodiltel-In-Docker/Rukovoditel">Filip Milašinoivć</a></li>
<li><b>Official website: </b><a href="https://www.rukovoditel.net/">Rukovoditel.net</a></li>
<li><b>Documentation: </b><a href="https://docs.rukovoditel.net/">Official Rukovoditel documentation</a></li>
<h1>How to use this image</h1>
<p>To use Rukovoditel you need a web server with Rukovoditel website, a database, storage for your data and a way to connect those.</p>
<li><b>First: </b>You need a Docker network - see Creating the Network;</a>
<li><b>Second: </b>You need a database container - see Creating the Database Container;</a>
<li><b>Third: </b>You need a Rukovoditel container - see Creating the Rukovoditel Container;</a>
<p>All database data and all Rukovoditel files will be placed in separate Docker volumes. Volumes are created at first start of the theirs respective container and serves as <b>permanent</b> storage for the database and Rukovoditel files. After stopping the containers, your data remans safe in those volumes. For backing up the data in volumes - see Backing Up Data.</p>
<h2>Creating the Network:</h2>
<p>Before creating any containers you need a common netwok for web server and database containers to communicate on.</p>
<p>Create local Docker network:</p>
<div class="highlight highlight-text-shell-session"><pre>$ docker network create some-network</pre></div>
<h2>Creating the Database Container:</h2>
<p>To manage data, you need a database and to store data you need a permanet storage. In this case these are MariaDB and Docker Volume. You may chose different database, MySql for example or to store data in host machine folder.</p>
<p>Create MariaDB database container and Docker volume to store data:</p>
<div class="highlight highlight-text-shell-session"><pre>$ docker run -d --rm --name some-mariadb --network some-netvork --mount 'type=volume,source=some-volume,destination=/var/lib/mysql' -e MYSQL_ROOT_PASSWORD=root-secret -e MYSQL_USER=some-user -e MYSQL_PASSWORD=secret -e MYSQL_DATABASE=some-db-name mariadb</pre></div>
<p>...where <code>some-mariadb</code> is the name for your database container. Example <code>rukovoditeldb</code>. <code>some-network</code> is the name for your network. Network must be created before use. Example <code>rukovoditelnet</code>. <code>some-volume</code> is the name of Docker volume for storing database data. Example <code>rukovoditeldbvol</code>. <code>root-secret</code> is database root user password. <code>some-user</code> is username for Rukovoditel database system account. Example: <code>ruser</code>. <code>secret</code> is Rukovoditel account database password. <code>some-db-name</code> is the name of database for Rukovoditel data. Example: <code>rukovoditel</code>.</p>
<h2>Creating the Rukovoditel Container:</h2>
<p>Create Rukovoditel container, Docker volume to store Rukovoditel data and connect it to network:</p>
<div class="highlight highlight-text-shell-session"><pre>$ docker run -dit --rm --name some-rukovoditel --network some-network --mount 'type=volume,source=some-volume,destination=/var/www/html' -p 80:80 filipmil/rukovoditel</pre></div>
<h2>Removing install folder:</h2>
<p>To remove install folder AFTER installation of Rukovoditel run this command::</p>
<div class="highlight highlight-text-shell-session"><pre>$ docker exec some-rukovoditel /bin/bash rm -r /var/www/html/install</pre></div>
<h1>Port Mapping</h1>
<p>If you'd like to be able to access the instance from the host without the container's IP, standard port mappings can be used. Just add -p 80:80 to the docker run arguments and then access either http://localhost or http://host-ip in a browser. If your hosts port 80 is used, use some other port. 
Example: -p 8080:80 will map containers port 80 to hosts port 8080 so you can access app either with http://localhost:8080 or http://host-ip:8080 in a browser.</p>
<h1>License</h1>
<p><a href="https://www.rukovoditel.net/download.php">Rukovoditel</a> is open source and released under the terms of the <a href="https://www.gnu.org/licenses/old-licenses/gpl-2.0.html"> GNU General Public License v2 (GPL).</a> <a href="https://tldrlegal.com/license/gnu-general-public-license-v2">Quick GPL-2.0 Summary.</a></p>
<p>Main version of <a href="https://www.rukovoditel.net/download.php">Rukovoditel</a>  is free and  fully functional software without any restrictions. <a href="https://www.rukovoditel.net/extension.php">Extension</a>  is commercial product and it is not included in this image.</p>
<p>As with all Docker images, these likely also contain other software which may be under other licenses (such as Bash, etc from the base distribution, along with any direct or indirect dependencies of the primary software being contained).</p>
<p>As for any pre-built image usage, it is the image user's responsibility to ensure that any use of this image complies with any relevant licenses for all software contained within.</p>
