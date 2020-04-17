<h1>This page is under construction!!!</h1>
<p>Rukovoditel is free Open Source Project Management developed by Sergey Kharchishin</p>
<h1>Quick reference</h1>
<li><b>Where to get help: </b><a href="https://forum.rukovoditel.net">Rukovoditel forum</a>
</li><li><b>Official website: </b><a href="https://www.rukovoditel.net/">Rukovoditel.net</a></li>
</li><li><b>Documentation: </b><a href="https://docs.rukovoditel.net/">Official Rukovoditel documentation</a></li>
<h1>How to use this image</h1>

<li><b>First: </b>You need a Docker network;</a>
<li><b>Second: </b>You need a database container;</a>
<li><b>Third: </b>You need a Rukovoditel container;</a>
<p>All database data and all Rukovoditel files will be placed in separate Docker volumes (automatically created)
<h2>Creating network:</h2>
<p>Create local Docker network:</p>
<div class="highlight highlight-text-shell-session"><pre>$ docker network create some-network</pre></div>
<h2>Creating database container:</h2>
<p>Create MariaDB database container and Docker volume to store data:</p>
<div class="highlight highlight-text-shell-session"><pre>$ docker run -d --rm --name some-mariadb --network some-netvork --mount 'type=volume,source=some-volume,destination=/var/lib/mysql' -e MYSQL_ROOT_PASSWORD=secret -e MYSQL_USER=some-user -e MYSQL_PASSWORD=secret -e MYSQL_DATABASE=rukovoditel mariadb</pre></div>
<h2>Creating Rukovoditel container:</h2>
<p>Create Rukovoditel container, Docker volume to store Rukovoditel data and connect it to network:</p>
<div class="highlight highlight-text-shell-session"><pre>$ docker run -dit --rm --name some-rukovoditel --network some-network --mount 'type=volume,source=some-volume,destination=/var/www/html' -p 80:80 filipmil/rukovoditel</pre></div>
<h2>Removing install folder:</h2>
<p>To remove install folder AFTER installation of Rukovoditel run this command::</p>
<div class="highlight highlight-text-shell-session"><pre>$ docker exec some-rukovoditel /bin/bash rm -r /var/www/html/install</pre></div>

<h1>License</h1>
<p><a href="https://www.rukovoditel.net/download.php">Rukovoditel</a> is open source and released under the terms of the <a href="https://www.gnu.org/licenses/old-licenses/gpl-2.0.html"> GNU General Public License v2 (GPL).</a> <a href="https://tldrlegal.com/license/gnu-general-public-license-v2">Quick GPL-2.0 Summary.</a></p>
<p>Main version of <a href="https://www.rukovoditel.net/download.php">Rukovoditel</a>  is free and  fully functional software without any restrictions. <a href="https://www.rukovoditel.net/extension.php">Extension</a>  is commercial product and it is not included in this image.</p>
<p>As with all Docker images, these likely also contain other software which may be under other licenses (such as Bash, etc from the base distribution, along with any direct or indirect dependencies of the primary software being contained).</p>
<p>As for any pre-built image usage, it is the image user's responsibility to ensure that any use of this image complies with any relevant licenses for all software contained within.</p>
