 SSL

Resource

    What is HTTPS?
    What are the 2 main elements that SSL is providing
    HAProxy SSL termination on Ubuntu16.04
    SSL termination
    Bash function
    How to Secure HAProxy with Let's Encrypt on Ubuntu 14.04
    HAProxy SSL Termination

Tasks
0. World wide web
1. HAproxy SSL termination
2. No loophole in your website traffic
"""
Fabric script based on the file 2-do_deploy_web_static.py that creates and
distributes an archive to the web servers
execute: fab -f 3-deploy_web_static.py deploy -i ~/.ssh/id_rsa -u ubuntu
"""

from fabric.api import env, local, put, run
from datetime import datetime
from os.path import exists, isdir
env.hosts = ['100.25.152.183', '100.26.142.197']


def do_pack():
    """generates a tgz archive"""
    try:
        date = datetime.now().strftime("%Y%m%d%H%M%S")
        if isdir("versions") is False:
            local("mkdir versions")
        file_name = "versions/web_static_{}.tgz".format(date)
        local("tar -cvzf {} web_static".format(file_name))
        return file_name
    except:
        return None

